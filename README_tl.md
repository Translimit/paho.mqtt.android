# ビルド方法

```
./gradlew build
./gradlew generateLibraryJar
```

以下のファイルが生成される。

```
org.eclipse.paho.android.service/build/libs/org.eclipse.paho.android.service-1.1.2-SNAPSHOT.jar
```

# ビルド環境

## JDK

JDKはOpenJDK8を使う。OpenJDK13だとビルド通らず。
https://qiita.com/t-motoki/items/e015950f89e0d17d22d0

```
 brew tap AdoptOpenJDK/openjdk
 brew cask install adoptopenjdk8
```
でOpenJDK8をインストール。

bash_profileを編集してPathを通す。

例
```
export JAVA_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
export PATH=$JAVA_HOME:$PATH
```

## NDK

NDKはandroid-ndk-r16bを使う。android-ndk-r20bだとビルド通らず。

ちなみにr20bでビルドすると以下のようなエラーがでる。
```
A problem occurred configuring project ':org.eclipse.paho.android.sample'.
> Could not resolve all dependencies for configuration ':org.eclipse.paho.android.sample:_debugApk'.
   > A problem occurred configuring project ':org.eclipse.paho.android.service'.
      > No toolchains found in the NDK toolchains folder for ABI with prefix: mips64el-linux-android
```

`mips64el-linux-android`がないらしい。これはr16bには含まれてるのでr16を使うように変更する。

例
```
export ANDROID_NDK_HOME=/Users/senakuzuoka/Library/Android/android-ndk-r16b
export PATH=$ANDROID_NDK_HOME:$PATH

export NDK_ROOT=/Users/senakuzuoka/Library/Android/android-ndk-r16b
export PATH=$NDK_ROOT:$PATH
```

# その他

設定が正しくても変なエラーを吐くことがある。キャッシュを削除すると解決することがある。
```
$ ./gradlew clean cleanBuildCache
```
