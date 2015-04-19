# 包名和类名整理记录 #
  * com.lives3.android -> com.lives3.maingui
    * 入口AndroidClient -> MainActivity
  * com.lives3.android.LiveS3Widget -> com.lives3.widgets.LiveS3Widget
  * com.lives3.android.PreloadContactsLoader -> com.lives3.common.ContactsLoader
  * com.lives3.ContactViewer -> com.lives3.common.ContactViewerActivity

# Bug List #
  * 从Viewer更新联系人状态 (能更新到结果,但是无法保存)
  * 添加公共群组  (状态有的显示出来了,有的没有)(也可能是正好发生了一次同步?)
  * TODO Test: 添加私密群组 （出现一次随机Exception）
```
12-05 04:29:57.390: ERROR/AndroidRuntime(24700): FATAL EXCEPTION: Thread-22
12-05 04:29:57.390: ERROR/AndroidRuntime(24700): java.lang.NullPointerException: one of arguments is null
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.text.RuleBasedCollator.compare(RuleBasedCollator.java:411)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.text.Collator.compare(Collator.java:233)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at com.lives3.common.ContactsLoader$1.compare(ContactsLoader.java:41)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at com.lives3.common.ContactsLoader$1.compare(ContactsLoader.java:1)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.util.TimSort.binarySort(TimSort.java:261)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.util.TimSort.sort(TimSort.java:204)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.util.TimSort.sort(TimSort.java:169)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.util.Arrays.sort(Arrays.java:1907)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.util.Collections.sort(Collections.java:1972)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at com.lives3.common.ContactsLoader.refreshSortedList(ContactsLoader.java:250)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at com.lives3.common.ContactsLoader.preload(ContactsLoader.java:203)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at com.lives3.maingui.GetOpenGroupBackgroundWorker.worker(GetOpenGroupBackgroundWorker.java:153)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at com.lives3.maingui.components.BackgroundWorker$2.run(BackgroundWorker.java:90)
12-05 04:29:57.390: ERROR/AndroidRuntime(24700):     at java.lang.Thread.run(Thread.java:1096)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891): FATAL EXCEPTION: Timer-0
12-05 04:30:05.180: ERROR/AndroidRuntime(24891): java.lang.NullPointerException: one of arguments is null
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.text.RuleBasedCollator.compare(RuleBasedCollator.java:411)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.text.Collator.compare(Collator.java:233)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at com.lives3.common.ContactsLoader$1.compare(ContactsLoader.java:41)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at com.lives3.common.ContactsLoader$1.compare(ContactsLoader.java:1)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.util.TimSort.binarySort(TimSort.java:261)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.util.TimSort.sort(TimSort.java:204)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.util.TimSort.sort(TimSort.java:169)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.util.Arrays.sort(Arrays.java:1907)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.util.Collections.sort(Collections.java:1972)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at com.lives3.common.ContactsLoader.refreshSortedList(ContactsLoader.java:250)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at com.lives3.common.ContactsLoader.preload(ContactsLoader.java:203)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at com.lives3.syncadapter.SyncAdapter.performSync(SyncAdapter.java:75)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at com.lives3.syncadapter.BackgroundSyncService$SyncTask.run(BackgroundSyncService.java:53)
12-05 04:30:05.180: ERROR/AndroidRuntime(24891):     at java.util.Timer$TimerImpl.run(Timer.java:289)
```
  * 无法同步Exchange账户；用系统通讯录添加的就可以同步

# Tested and passed #
  * 从二维码添加群组
  * 从二维码添加单个联系人
  * 添加到“无账户”

# To be tested #
  * 从Sync Adapter更新联系人