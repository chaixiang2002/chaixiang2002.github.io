```
src_files := $(shell ls $(LOCAL_PATH)/source/app )

PRODUCT_COPY_FILES += $(foreach file, $(src_files), $(LOCAL_PATH)/source/app/$(file):system/app/$(file))
```


[用PRODUCT_COPY_FILES拷贝文件夹 - leo21sun - 博客园 (cnblogs.com)](https://www.cnblogs.com/codeking100/p/10309929.html)
