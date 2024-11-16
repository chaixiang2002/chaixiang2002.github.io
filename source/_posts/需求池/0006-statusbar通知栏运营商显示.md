[statusbar--通知栏运营商显示（一）_updatecarriertext未显示-CSDN博客](https://blog.csdn.net/yunwuhuxin/article/details/17266501)

[Android 状态栏显示运营商名称_android systemui运营商-CSDN博客aaaaaa](https://blog.csdn.net/tq501501/article/details/132368932)

[运营商名称 是如何显示到 手机通知栏上的？_国内运营商plmn对照表-CSDN博客](https://xiaxl.blog.csdn.net/article/details/137563711?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-4-137563711-blog-117347878.235^v43^pc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-4-137563711-blog-117347878.235^v43^pc_blog_bottom_relevance_base7&utm_relevant_index=9)

---

### 有线的图标如何添加

**frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/StatusBarSignalPolicy.java**

mSlotEthernet = mContext.getString(com.android.internal.R.string.status_bar_ethernet);

private final String mSlotEthernet;

public void setEthernetIndicators(IconState state)

- mIconController.setIcon(mSlotEthernet, resId, description);
- mIconController.setIconVisibility(mSlotEthernet, true);

frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/policy/NetworkControllerImpl.java

mEthernetSignalController = new EthernetSignalController(mContext, mCallbackHandler, this);



---

移动数据的图标是如何添加的
**frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/StatusBarIconController.java**

**frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/StatusBarMobileView.java**

  private TextView mOperatorNameTextView;

```java
        // 获取运营商名称
        TelephonyManager telephonyManager = (TelephonyManager) getContext().getSystemService(Context.TELEPHONY_SERVICE);
        String SimOperatorName = telephonyManager.getSimOperatorName(); // 获取运营商名称
        // 11-06 15:49:55.241   421   421 D statusbar: mOperatorNameTextView start11111CHT

        // 找到 TextView 控件，并设置运营商名称
        if (mOperatorNameTextView == null) {
            mOperatorNameTextView = findVi	ewById(R.id.operator_name); // 获取控件实例
        }
        // Log.d("statusbar", "mOperatorNameTextView == null: " + (mOperatorNameTextView == null));
        if (mOperatorNameTextView != null) {
            mOperatorNameTextView.setText(SimOperatorName); // 设置运营商名称
        }
```

frameworks/base/packages/SystemUI/res/layout/status_bar_mobile_signal_group.xml

```xml
        <TextView
            android:id="@+id/operator_name"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textColor="@android:color/white"
            android:textSize="12sp"
            android:layout_gravity="center_vertical"
            android:paddingEnd="4dp"
            android:text="运营商名称" />
```

---

## Statusbar图标显示顺序

[添加并客制化Statusbar中图标显示顺序_statusbar 信号icon显示顺序-CSDN博客](https://blog.csdn.net/sex_baby/article/details/105659189)