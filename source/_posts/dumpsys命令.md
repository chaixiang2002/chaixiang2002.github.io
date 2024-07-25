### 获取当前聚焦的app的包名

```
 dumpsys window | grep -E 'mCurrentFocus|mFocusedApp'
  mCurrentFocus=null
  mFocusedApp=null
  mCurrentFocus=Window{4523d26 u0 com.instagram.android/com.instagram.modal.ModalActivity}
  mFocusedApp=AppWindowToken{e98838b token=Token{8d7255a ActivityRecord{2ad0105 u0 com.instagram.android/com.instagram.modal.ModalActivity t21}}}
    mFocusedApp=Token{8d7255a ActivityRecord{2ad0105 u0 com.instagram.android/com.instagram.modal.ModalActivity t21}}
ec39b5f23ce0:/ #
```
