리액트 네이티브 윈도우 개발 환경 설정하기
=

Step 1. JDK
-
JDK 8 버전 설치 권장 [링크](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

Step 2. Node.js
-
리액트 네이티브는 노드 환경에서 돌아간다. 설치하자. [링크](https://nodejs.org/en/)

설치가 완료되면 다음 콘솔 명령어를 통해 잘 설치되었는지 확인해보자.

```console
PS> node --version
v8.11.4
```

Step 2-1. npm / yarn
-
노드를 설치하면 자동으로 **npm** (node package manager)가 설치된다.

마찬가지로 잘 설치되어 있는지 다음 콘솔 명령어를 통해 확인하자.

```console
PS> npm --version
5.6.0
```

노드의 패키지 관리자는 npm만 있는건 아니다. 페이스북과 구글 등의 회사가 합작해 새로 만든 **yarn**도 있다. 아무래도 리액트 네이티브도 페이스북에서 만든 것이니 왠지 좀 더 친화적으로 보인다. yarn을 사용해보고 싶다면 다음 명령어를 통해 설치하면 된다.

```console
PS> npm install --global yarn
```

설치 확인은 마찬가지로 콘솔 명령어를 통해 확인 할 수 있다.

```console
PS> yarn --version
1.10.1
```

Step 3. Visual Studio Code
-
여러가지 코드 에디터가 존재하지만 필자는 비주얼 스튜디오 코드(이하 VSCode)를 선호한다. 설치해주자. [링크](https://code.visualstudio.com/)

Step 4. Android Studio
-
윈도우에서 리액트 네이티브를 테스트하기 위해선 안드로이드 에뮬레이터가 필요하다. 때문에 안드로이드 스튜디오를 설치하자. [링크](https://developer.android.com/studio/)

설치 후에는  리액트 네이티브에서 사용 할 수 있도록 `ANDROID_HOME` 환경변수도 설정해줘야한다. 윈도우에서는 보통 `C:\Users\<user-name>\AppData\Local\Android\Sdk`에 설치되니 해당 경로를 연결해주면 된다.

Step 5. 리액트 네이티브 모듈 설치
-
```console
PS> npm install -g react-native-cli
```

또는

```console
PS> yarn global add react-native-cli
```

Step 5-1. 리액트 네이티브 프로젝트 생성
-
리액트 최신 버전 프로젝트 생성은 간단하다. 다음 명령어를 이용하자.

```console
PS> react-native init 'project-name'
```

프로젝트 생성 후 프로젝트 폴더로 이동해 다음 명령어를 통해 프로젝트를 실행한다.

```console
PS> cd 'project-name';
PS 'project-name'> react-native run-android
```

문제는 그냥 프로젝트를 생성하면 윈도우에서 실행시 에러가 난다. 그나마 `0.55.4` 버전이 제일 안정적이다.

```console
PS> react-native init 'project-name' --version 0.55.4
```

Step 6. Expo
-
리액트 네이티브만으로 개발해도 상관 없지만 Expo는 좀더 강력한 개발 환경을 지원한다.
사실 순수하게 react-native로 프로젝트를 생성 하는 것보다 추천한다.

설치해주자.

위와 마찬가지 이유로 Expo도 리엑트 네이티브는 `0.55.4`버전으로 설치가 된다.

```console
PS> npm install -g expo-cli
```

또는

```console
PS> yarn global add expo-cli
```

명령어를 이용해 설치 할 수 있다.

Step 6-1. CRNA (create-react-native-app)
-
```console
PS> npm install -g create-react-native-app
```

또는

```console
PS> yarn global add create-react-native-app
```
```console
PS> create-react-native-app 'project-name'
PS> cd 'project-name'
```

```console
PS> npm install
PS> npm start
```

Step 6-2. Expo 프로젝트 생성
-
```console
PS> expo init 'project-name'
PS> cd 'project-name'
PS> expo start
```
