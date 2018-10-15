# 윈도우10에서 리액트 네이티브에 Web3 1.0.0-beta 설치하기

Step 0. 들어가기
-
리액트 네이티브(혹은 노드)에서 버전 관리는 아주 중요하다.

최신 버전 모듈을 그냥 막 설치하면 반드시라고 해도 좋을 만큼 항상(!) 문제가 생긴다.

모듈의 버전 관리를 하는  `package.json` 파일에서 상위 버전을 허용하는 `^` 마크는 의존성 문제의 시발점이 될 수 있다. `--save-exact` 또는 `-E` 옵션을 활용하자. 참고로 `-E` 옵션은 `--save-exact`의 축약형이다.

일단, 리액트 네이티브 설치는 이미 기본으로 되있다고 가정한다.

그리고 이 글은 2018년 10월 12일을 기준으로 작성된 문서임에 유의하자.

```
node v8.11.4
npm 5.6.0
react-native-cli 2.0.1
```

Step 1. 리액트 네이티브 프로젝트 생성하기
-
윈도우10에서 개발시에 가장 안정적인 리액트 네이티브 버전은 `0.55.x` 버전인듯 하다. 정확하게 리액트 네이티브 버전을 지정해 설치하자.

```console
PS> react-native init 'project-name' --version 0.55.3
```

물론 생성된 프로젝터로 이동해야 한다.

```console
PS> cd 'project-name'
```

Step 2. `node-libs-browser` 설치
-
그 다음으로 리액트 네이티브에서 삭제된 노드 코어 라이브러리를 사용 할 수 있도록 [`node-libs-browser`]()가 필요하다.

```console
PS> npm install -E node-libs-browser@2.1.0
```

Step 3. `rn-cli.config.js` 파일 생성 및 작성
-
이제 `node-libs-browser`를 리액트 네이티브에서 알아 먹을 수 있도록 루트 디렉토리에 `rn-cli.config.js` 파일를 생성해 내용을 좀 채눠 넣자

```javascript
const extraNodeModules = require('node-libs-browser');

module.exports = {
    extraNodeModules
};
```

Step 4. `global.js` 파일 생성 및 작성
-
   
리엑트 네이티브의 전역 영역에 노드의 전역 영역 내용을 인젝션하기 위해 `global.js` 파일도 하나 생성해서 다음 내용을 좀 채우자. 그리고 대소문자에 주의하자.

```javascript
// Inject node globals into React Native global scope
global.Buffer = require('buffer').Buffer;
global.process = require('process');

if (typeof btoa === 'undefined') {
    global.btoa = function (str) {
        return new Buffer(str, 'binary').toString('base64')
    };
}

if (typeof atob === 'undefined') {
    global.atob = function (base64Encoded) {
        return new Buffer(base64Encoded, 'base64').toString('binary')
    };
}
```

Step 5. `global.js` 임포트하기
-
`Apps.js` 파일 상단에 생성한 `global.js` 파일을 임포트 하자.

```javascript
import './global'
```

Step 6. `babel-cli`와 `babel-preset-es2015` 설치하기
-
`web3`는 es2015 문법을 필요로 한다. [`babel-cli`]()와 [`babel-preset-es2015`]()를 설치하자. 이 두가지 모듈은 개발 단계에서만 사용된다. `--save-dev` 또는 `-D` 옵션을 붙이자. 마찬가지로 `-D`는 `--save-dev`의 축약형이다.

```console
PS> npm install -D -E babel-cli@6.26.0 babel-preset-es2015@6.24.1
```

Step 7. `web3` 설치하기
-
   
이제 우리의 최종 목적인 `web3` 모듈을 설치하자.

```console
npm install -E web3@1.0.0-beta.34
```

Step 8. 의존성 모듈 설치하기
-
거의 다 됐다. 위에서 설치한 모듈들은 당연히 각자 의존성 모듈들이 있다. 다 설치하자.

```console
PS> npm install
```

Step 9. 이제, 리액트 프로젝트를 실행해 에러가 없는지 확인해보자.
-
```console
PS> react-native run-android
```

Step 10. `web3` 코드 작성!
-
여기까지 왔으면 거의 다 된거다. `web3`를 사용해보자! `Apps.js`의 `App` 클래스에 약간의 코드를 추가해 테스트하자.

```javascript
const Web3 = require('web3');
```

```javascript
componentWillMount() {
    const web3 = new Web3(
        new Web3.providers.HttpProvider('https://mainnet.infura.io/<api-key>')
    );

    web3.eth.getBlock('latest').then(console.log);
}
```

Step 11. 완료
-
실행해보자.

```console
PS> react-native run-android
```

길지는 않지만 고생했다!

참고자료
-
https://gist.github.com/dougbacelar/29e60920d8fa1982535247563eb63766
https://heropy.blog/2018/02/18/node-js-npm/