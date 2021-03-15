## apk decompile

### 1. Tools Set-up

- ApkTool
  - 	https://ibotpeaches.github.io/Apktool/
- Dex2Jar
  - https://github.com/pxb1988/dex2jar
- JD-GUI

#### (1) ApkTool

##### Install Instructions

https://ibotpeaches.github.io/Apktool/

##### Quick Check

1. Is at least Java 1.8 installed?
2. Does executing java -version on command line / command prompt return 1.8 or greater?
3. If not, please install Java 8+ and make it the default. (Java 7 will also work at this time)

##### Installation for Apktool

- Windows:

  1. Download Windows [wrapper script](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/windows/apktool.bat) (Right click, Save Link As `apktool.bat`)
  2. Download apktool-2 ([find newest here](https://bitbucket.org/iBotPeaches/apktool/downloads/))
  3. Rename downloaded jar to `apktool.jar`
  4. Move both files (`apktool.jar` & `apktool.bat`) to your Windows directory (Usually `C://Windows`)
  5. If you do not have access to `C://Windows`, you may place the two files anywhere then add that directory to your Environment Variables System PATH variable.
  6. Try running apktool via command prompt

- Linux:

  1. Download Linux [wrapper script](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool) (Right click, Save Link As `apktool`)
  2. Download apktool-2 ([find newest here](https://bitbucket.org/iBotPeaches/apktool/downloads/))
  3. Rename downloaded jar to `apktool.jar`
  4. Move both files (`apktool.jar` & `apktool`) to `/usr/local/bin` (root needed)
  5. Make sure both files are executable (`chmod +x`)
  6. Try running apktool via cli

- macOS:

  1. Download Mac [wrapper script](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/osx/apktool) (Right click, Save Link As `apktool`)
  2. Download apktool-2 ([find newest here](https://bitbucket.org/iBotPeaches/apktool/downloads/))
  3. Rename downloaded jar to `apktool.jar`
  4. Move both files (`apktool.jar` & `apktool`) to `/usr/local/bin` (root needed)
  5. Make sure both files are executable (`chmod +x`)
  6. Try running apktool via cli

  Or you can install apktool via *Homebrew*:

  1. Install Homebrew as described [in this page](https://brew.sh/)
  2. Execute command `brew install apktool` in terminal (no root needed). The latest version will be installed in `/usr/local/Cellar/apktool/[version]/` and linked to `/usr/local/bin/apktool`.
  3. Try running apktool via cli

**Note** - Wrapper scripts are not needed, but helpful so you don’t have to type java -jar apktool.jar over and over.

#### (2) dex2jar

https://github.com/pxb1988/dex2jar

앱의 `.dex` 파일을 `.jar` 파일로 바꿀 수 있다. jar는 `.class` 파일들이 압축되어 있는 형식이다. 즉, 앱을 빌드하기 위해 만들어진 클래스 파일 모음인 jar로 변환하는 작업을 해준다.

dex2jar-2.0.zip 로 압축되어 있으며 [여기서 다운로드](https://github.com/pxb1988/dex2jar/releases) 받을 수 있다.

#### (3) JD-GUI

http://java-decompiler.github.io/

Java 5 버전 및 그 이후의 `byte code`를 디컴파일 및 분석하기 위한 도구이다. 디컴파일한 자바 클래스 파일을 소스 코드로 보도록 도와준다. 위의 dex2jar를 통해 생성한 클래스들을 간편하게 볼 때 사용할 것이다.

홈페이지의 JD-GUI 탭-다운로드를 통해 운영 체제에 맞게 다운로드 해준다.

1.6.6 버전 - [윈도우용](https://github.com/java-decompiler/jd-gui/releases/download/v1.6.6/jd-gui-windows-1.6.6.zip) [맥용](https://github.com/java-decompiler/jd-gui/releases/download/v1.6.6/jd-gui-osx-1.6.6.tar)

### 2. Build Test app

### 3. Decompile

#### 1. 내부 파일을 확인만 해볼 경우

- apk -> jar 파일 변환
- jar 파일 확인

#### 2. 파일을 수정하고 앱 재빌드 하는 경우

- Apk 압축 풀기
- dex -> jar 파일 변환
- jar 파일 확인
- 파일 수정
- 다시 빌드하기
- 서명 및 설치

참고) 본 포스트의 예제는 Mac OS 환경에서 진행되었다.

#### (1) apk / dex -> jar 파일 변환

다운로드 받은 d2j~.zip 압축을 풀고 해당 폴더로 이동한다.

`chmod` 명령어를 통해 d2j의 권한을 허가한다.

```
sudo chmod +x d2j_invoke.sh
```



sudo로 d2j-dex2jar.sh를 사용한다.

```
sudo sh d2j-dex2jar.sh [apk 또는 dex 파일 위치]
```

예시)

```
sudo sh d2j-dex2jar.sh ../app-debug.apk    
```

만약 버전 에러가 난다면 dex2jar 깃헙 페이지에서 최신 버전이 맞는 지 확인하자. 2020년 2월 확인했을 때에는 2018년 3월 버전이 최신 버전이었다.

```
dex2jar ../app-debug.apk -> ./app-debug-dex2jar.jar
com.googlecode.d2j.DexException: not support version.
	at com.googlecode.d2j.reader.DexFileReader.<init>(DexFileReader.java:151)
	at com.googlecode.d2j.reader.DexFileReader.<init>(DexFileReader.java:211)
	at com.googlecode.dex2jar.tools.Dex2jarCmd.doCommandLine(Dex2jarCmd.java:104)
	at com.googlecode.dex2jar.tools.BaseCmd.doMain(BaseCmd.java:288)
	at com.googlecode.dex2jar.tools.Dex2jarCmd.main(Dex2jarCmd.java:32)
```



앱-이름-dex2jar.jar 파일이 생성되었다면 성공.


#### (2) jar 파일 확인

이 jar 파일은 JD-GUI 툴을 통해 확인할 수 있다. 뭔가 수상한 파일처럼 보이는지 실행하려고 하면 맥에서 그냥 휴지통으로 버려 버리려고 한다.



![img](https://blog.yena.io/assets/post-img20/200210-05.png)



시스템 설정 - 보안 및 개인 설정으로 들어가 ‘어쨌든 열라고’를 클릭하자.

![img](https://blog.yena.io/assets/post-img20/200210-06.png)



회색 화면의 JD-GUI를 볼 수 있다. 버튼 혹은 드래그앤드롭을 통해 jar 파일을 열자.

~~JD-GUI와 같은 경로에 있지 않으면 아래와 같은 에러가 발생할 수도 있다.~~
jar 파일에 권한이 없을 때에 아래처럼 ‘Invalid input fileloader’ 라는 에러가 발생하는 것 같다. 에러 발생 시 `chmod` 명령어로 권한을 부여해준다.

```
sudo chmod +xr [jar 파일 위치]
```

![img](https://blog.yena.io/assets/post-img20/200210-08.png)



제대로 오픈이 되면 이런 화면을 볼 수 있다.

![img](https://blog.yena.io/assets/post-img20/200210-09.png)



오. Kotlin 클래스들이 Java로 변환되었다. 자바로 코딩했을 때에는 원본 클래스 파일 거의 그대로 표시됐는데, 코틀린으로 개발하니 컴파일된 자바 파일을 볼 수 있었다.

약간 번거롭긴 하지만 코틀린 코드에서 어떤 것을 처리했는지 알 수는 있었다. 변수 이름이나 String 값 등도 알아볼 수 있었다.



#### (3) Apk 압축 풀기

파일을 수정하고 재빌드 할 계획이라면 apk 파일의 압축을 먼저 풀어준다. 여담이지만 몰랐던 사실이 있는데, .apk 파일의 확장자를 .zip 으로 이름을 변경한 후 압축을 풀어도 dex 파일이 나오긴 나온다. 다만 매니페스트를 비롯한 다른 리소스 파일이 깨져버린다. 그래서 앱을 빌드 했던 방식을 토대로 디컴파일 하는 apktool을 사용해서 풀어야 제대로된 결과를 얻을 수 있다.

apk 파일은 안드로이드 스튜디오에서 빌드에 성공한 후, `프로젝트 위치` - `app` - `build` - `outputs` - `apk` - `debug/release` 에 들어가면 찾을 수 있다. 터미널을 열고 apktool을 사용해 apk 파일 압축을 해제한다.

```
apktool d -f -s -o [결과 폴더] [apk파일 위치]
```

예시)

```
apktool d -f -s -o /Users/yenachoi/Desktop/0211/result /Users/yenachoi/Desktop/0211/app-debug.apk
```

데스크탑에 0211 폴더 안에 다시 result 라는 하위 폴더를 만들고 여기에 디컴파일을 진행했다. 새 폴더를 만들지 않았더니 다른 파일들과 충돌하는지 파일들이 완전 지워져버리는 사태가 발생했다.



![img](https://blog.yena.io/assets/post-img20/200210-03.png)



이런이런게 터미널에 찍히고 결과 폴더에 파일들이 여럿 만들어진다.



![img](https://blog.yena.io/assets/post-img20/200210-04.png)



`AndroidManifest`, `res` 폴더 등등 익숙한 이름도 눈에 띈다. 에디터를 통해 파일을 열어 매니페스트나 레이아웃, 리소스 등 xml 코드를 확인할 수 있다.

그리고 `classes.dex`는 위에서 본 것 같이 `dex2jar`를 이용해 내부 클래스 코드를 볼 수 있다.


#### (4) 파일 수정

임의의 파일을 수정해보자. Manifest 파일을 열어서 `android:label="REBUILT"`로 속성을 바꿔 앱 이름을 변경해보았다.



#### (5) 다시 빌드하기

apktool을 이용해 위에서 디컴파일 했던 폴더를 선택하고 재빌드할 apk 파일의 이름도 지정해준다.

```
apktool b [결과 폴더] -o [결과.apk]
```

예시)

```
apktool b /Users/yenachoi/Desktop/0211/result -o /Users/yenachoi/Desktop/0211/rebuilt.apk
```



#### (6) 서명 및 설치

새로 빌드한 앱에 서명을 다시 해야 설치할 수 있다. 새로 사인하는 방법은 여러가지가 있지만, 그 중에서 `jarsigner` 명령어를 통해 해주었다.

맥)

```bash
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore ~/.android/debug.keystore [앱 이름.apk] androiddebugkey -storepass android
```

윈도우)

```
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore %USERPROFILE%/.android/debug.keystore [앱 이름.apk] androiddebugkey -storepass android
```

마지막으로 디바이스에 설치할 때에는 `adb` 툴을 사용했다. ([Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) 문서 참고)

이전에 앱이 설치되어 있다면 서명키가 달라서 설치할 수 없다는 오류가 나 기존 앱을 삭제하고 재설치했다.

```basic
adb install -r [앱 이름.apk]
```



------

### 4. 결론

몇 단계만 거쳐 앱의 원본 코드를 볼 수 있다는 사실이 놀라웠고, 이 방법이 나름 흔한(?) 방법이라 많은 사람들이 쓰고 있다는 것도 알았다. 여러 테스트를 하면서 보안 적용을 한 앱도 디컴파일 해봤는데, 리소스 이름이 난독화되어서 재빌드 후 리소스 파일명 매칭이 안되어 크래쉬가 나는 것을 볼 수 있었다. 번거롭고 머리 아프더라도 가능한 한 보안에 신경 써야겠다는 생각이 드는 테스트였다.

------

###  References

- https://ibotpeaches.github.io/Apktool/install/
- https://github.com/pxb1988/dex2jar/
- https://dnight.tistory.com/entry/Android-Decompile-Setting?category=843230
- https://stackoverflow.com/questions/10930331/how-to-sign-an-already-compiled-apk





