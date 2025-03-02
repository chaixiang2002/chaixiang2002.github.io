获取IPhoneSubInfo 

frameworks/base/telephony/java/android/telephony/TelephonyManager.java

- public String getSimSerialNumber(int subId) {
  - IPhoneSubInfo info = getSubscriberInfo();
  - return info.getIccSerialNumberForSubscriber(subId, mContext.getOpPackageName());

- private IPhoneSubInfo getSubscriberInfo() {
  - IPhoneSubInfo.Stub.asInterface(ServiceManager.getService("iphonesubinfo"));

frameworks/opt/telephony/src/java/com/android/internal/telephony/PhoneSubInfoController.java

- ServiceManager.addService("iphonesubinfo", this);





frameworks/opt/telephony/src/java/com/android/internal/telephony/PhoneSubInfoController.java

- public String getIccSerialNumberForSubscriber(int subId, String callingPackage) {

  - return callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(subId, callingPackage,

  ​        "getIccSerialNumber", (phone) -> phone.getIccSerialNumber());

- private <T> T callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(int subId

  - return callPhoneMethodWithPermissionCheck(subId, callingPackage, message, callMethodHelper,

    ​        (aContext, aSubId, aCallingPackage, aMessage)->

    ​            TelephonyPermissions.checkCallingOrSelfReadSubscriberIdentifiers(

    ​                aContext, aSubId, aCallingPackage, aMessage));

      }

- private <T> T callPhoneMethodWithPermissionCheck(int subId, String callingPackage,

  - final long identity = Binder.clearCallingIdentity();
  - Binder.restoreCallingIdentity(identity);

```java
//frameworks/opt/telephony/src/java/com/android/internal/telephony/PhoneSubInfoController.java
	//class PhoneSubInfoController extends IPhoneSubInfo.Stub
	/**
     * Retrieves the serial number of the ICC, if applicable.
     */
    public String getIccSerialNumber(String callingPackage) {
        return getIccSerialNumberForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getIccSerialNumberForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(subId, callingPackage,
                "getIccSerialNumber", (phone) -> phone.getIccSerialNumber());
    }

    public String getLine1Number(String callingPackage) {
        return getLine1NumberForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getLine1NumberForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadPhoneNumberCheck(
                subId, callingPackage, "getLine1Number",
                (phone)-> phone.getLine1Number());
    }

    public String getLine1AlphaTag(String callingPackage) {
        return getLine1AlphaTagForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getLine1AlphaTagForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadCheck(subId, callingPackage, "getLine1AlphaTag",
                (phone)-> phone.getLine1AlphaTag());
    }

    public String getMsisdn(String callingPackage) {
        return getMsisdnForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getMsisdnForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadCheck(subId, callingPackage, "getMsisdn",
                (phone)-> phone.getMsisdn());
    }

    public String getVoiceMailNumber(String callingPackage) {
        return getVoiceMailNumberForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getVoiceMailNumberForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadCheck(subId, callingPackage,
                "getVoiceMailNumber", (phone)-> {
                    String number = PhoneNumberUtils.extractNetworkPortion(
                            phone.getVoiceMailNumber());
                    if (VDBG) log("VM: getVoiceMailNUmber: " + number);
                    return number;
                });
    }

    public String getVoiceMailAlphaTag(String callingPackage) {
        return getVoiceMailAlphaTagForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getVoiceMailAlphaTagForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadCheck(subId, callingPackage,
                "getVoiceMailAlphaTag", (phone)-> phone.getVoiceMailAlphaTag());
    }
```



```java
//frameworks/opt/telephony/src/java/com/android/internal/telephony/PhoneSubInfoController.java
	public String getIccSerialNumberForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(subId, callingPackage,
                "getIccSerialNumber", (phone) -> phone.getIccSerialNumber());
    }

    private <T> T callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(int subId,
            String callingPackage, String message, CallPhoneMethodHelper<T> callMethodHelper) {
        return callPhoneMethodWithPermissionCheck(subId, callingPackage, message, callMethodHelper,
                (aContext, aSubId, aCallingPackage, aMessage)->
                        TelephonyPermissions.checkCallingOrSelfReadSubscriberIdentifiers(
                                aContext, aSubId, aCallingPackage, aMessage));
    }

    private <T> T callPhoneMethodWithPermissionCheck(int subId, String callingPackage,
            String message, CallPhoneMethodHelper<T> callMethodHelper,
            PermissionCheckHelper permissionCheckHelper) {
        if (!permissionCheckHelper.checkPermission(mContext, subId, callingPackage, message)) {
            return null;
        }

        final long identity = Binder.clearCallingIdentity();
        try {
            Phone phone = getPhone(subId);//!!!!!!!!!
            if (phone != null) {
                return callMethodHelper.callMethod(phone);//!!!!!!!!!!!!
            } else {
                loge(message + " phone is null for Subscription:" + subId);
                return null;
            }
        } finally {
            Binder.restoreCallingIdentity(identity);
        }
    }

    private Phone getPhone(int subId) {
        int phoneId = SubscriptionManager.getPhoneId(subId);
        if (!SubscriptionManager.isValidPhoneId(phoneId)) {
            phoneId = 0;
        }
        if (mPhone.length < 1) return null;
        return mPhone[phoneId];//!!!!!!!!!
    }


//frameworks/opt/telephony/src/java/com/android/internal/telephony/Phone.java
    public String getIccSerialNumber() {
        IccRecords r = mIccRecords.get();//!!!!!!
        return (r != null) ? r.getIccId() : null;//!!!!!!!
    }


//frameworks/opt/telephony/src/java/com/android/internal/telephony/uicc/IccRecords.java
    public String getIccId() {
        if (mCarrierTestOverride.isInTestMode() && mCarrierTestOverride.getFakeIccid() != null) {
            return mCarrierTestOverride.getFakeIccid();
        } else {
            return mIccId;
        }
    }



```









frameworks/opt/telephony/src/java/com/android/internal/telephony/uicc/IsimUiccRecords.java







```java
// frameworks/base/telephony/java/android/telephony/TelephonyManager.java
    public String getSimSerialNumber(int subId) {
        try {
            IPhoneSubInfo info = getSubscriberInfo();//!!!!!!!!!!
            if (info == null)
                return null;
            return info.getIccSerialNumberForSubscriber(subId, mContext.getOpPackageName());//!!!!!!!!!!
        } catch (RemoteException ex) {
            return null;
        } catch (NullPointerException ex) {
            // This could happen before phone restarts due to crashing
            return null;
        }
    }
    private IPhoneSubInfo getSubscriberInfo() {
        // get it each time because that process crashes a lot
        return IPhoneSubInfo.Stub.asInterface(ServiceManager.getService("iphonesubinfo"));//!!!!!!!!!!
    }

//frameworks/opt/telephony/src/java/com/android/internal/telephony/PhoneSubInfoController.java
    public String getIccSerialNumber(String callingPackage) {
        return getIccSerialNumberForSubscriber(getDefaultSubscription(), callingPackage);
    }

    public String getIccSerialNumberForSubscriber(int subId, String callingPackage) {
        return callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(subId, callingPackage,
                "getIccSerialNumber", (phone) -> phone.getIccSerialNumber());//!!!!!!!!!!
    }
    private <T> T callPhoneMethodForSubIdWithReadSubscriberIdentifiersCheck(int subId,
            String callingPackage, String message, CallPhoneMethodHelper<T> callMethodHelper) {
        return callPhoneMethodWithPermissionCheck(subId, callingPackage, message, callMethodHelper,//!!!!!!!!!
                (aContext, aSubId, aCallingPackage, aMessage)->
                        TelephonyPermissions.checkCallingOrSelfReadSubscriberIdentifiers(
                                aContext, aSubId, aCallingPackage, aMessage));
    }
    private <T> T callPhoneMethodWithPermissionCheck(int subId, String callingPackage,
            String message, CallPhoneMethodHelper<T> callMethodHelper,
            PermissionCheckHelper permissionCheckHelper) {
        if (!permissionCheckHelper.checkPermission(mContext, subId, callingPackage, message)) {
            return null;
        }

        final long identity = Binder.clearCallingIdentity();
        try {
            Phone phone = getPhone(subId);
            if (phone != null) {
                return callMethodHelper.callMethod(phone);//!!!!!!!!!!!!!!!!!!!!!!
            } else {
                loge(message + " phone is null for Subscription:" + subId);
                return null;
            }
        } finally {
            Binder.restoreCallingIdentity(identity);
        }
    }
//frameworks/opt/telephony/src/java/com/android/internal/telephony/Phone.java
    public String getIccSerialNumber() {
        IccRecords r = mIccRecords.get();
        return (r != null) ? r.getIccId() : null;
    }

//frameworks/opt/telephony/src/java/com/android/internal/telephony/uicc/IccRecords.java
    public String getIccId() {
        if (mCarrierTestOverride.isInTestMode() && mCarrierTestOverride.getFakeIccid() != null) {
            return mCarrierTestOverride.getFakeIccid();
        } else {
            return mIccId;
        }
    }	

```

### 为什么没有涉及到 `ril.java`？

通过你的代码分析，我们注意到最终获取 ICCID 的方法链并没有直接与 `ril.java` 的方法进行交互。原因是：

- `PhoneSubInfoController` 的 `getIccSerialNumberForSubscriber()` 方法最终调用了 `Phone` 对象的 `getIccSerialNumber()` 方法。

- 在 `Phone` 类中，`getIccSerialNumber()` 方法会访问 `IccRecords` 对象，通过 `IccRecords.getIccId()` 获取 ICCID。

  这并不直接涉及到 `ril.java`，因为 `getIccId()` 方法实际上是访问已经加载的 `IccRecords`（即 SIM 卡信息）。而 `IccRecords` 通常是在设备初始化时通过与基带通信获取的，但这个过程发生在更早的阶段，不是在你当前获取 ICCID 时发生。