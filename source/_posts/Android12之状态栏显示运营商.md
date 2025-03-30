

```xml
packages/apps/Settings/res/values-zh-rCN/strings.xml

  <string name="status_number_sim_status" product="default" msgid="2772745542921910086">"SIM 卡上的电话号码"</string>


packages/apps/Settings/src/com/android/settings/deviceinfo/simstatus/SimStatusPreferenceController.java
        final List<SubscriptionInfo> subscriptionInfoList =
                mSubscriptionManager.getActiveSubscriptionInfoList();
        if (subscriptionInfoList != null) {
            for (SubscriptionInfo info : subscriptionInfoList) {
                if (info.getSimSlotIndex() == simSlot) {
                    return info.getCarrierName();
                }
            }
        }










```

