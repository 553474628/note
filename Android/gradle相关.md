##### compileSdkVersion, minSdkVersion 和 targetSdkVersion

+ minSdkVersion：app运行所需的最低sdk版本.低于minSdkVersion的手机将无法安装
+ compileSdkVersion：告诉 Gradle 用哪个 Android SDK 版本编译你的应用，比如当前版本sdk是28，使用了29中新增的方法，那么就会报编译错误（用反射是不是可以避免错误而抛异常？）
+ targetSdkVersion：向前兼容的主要依据。随着 Android 系统的升级，某个系统的 API 或者模块的行为可能会发生改变，但是为了保证老 APK 的行为还是和以前兼容。只要 APK 的 targetSdkVersion 不变，即使这个 APK 安装在新 Android 系统上，其行为还是保持老的系统上的行为，这样就保证了系统对老应用的前向兼容性。
+ 理想上，在稳定状态下三者的关系应该更像这样：
  minSdkVersion (lowest possible) <= targetSdkVersion == compileSdkVersion (latest SDK)
  用较低的 minSdkVersion 来覆盖最大的人群，用最新的 SDK 设置 target 和 compile 来获得新版本最好的效果。
