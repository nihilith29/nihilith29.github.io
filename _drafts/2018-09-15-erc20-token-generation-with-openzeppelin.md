OpenZeppelin을 활용한 ERC20 토큰 생성하기
=

Step 0. Remix IDE와 Metamask
-
### **Remix IDE**

이더리움의 스마트 컨트랙트를 작성하기 위한 가장 쉬운 방법은 이더리움 제단에서 제공하는 [Remix IDE](https://remix.ehtereum.org/)를 사용하는 것입니다. Remix IDE는 웹브라우저를 통해 실행되며 원한다면 오프라인으로 다운받아 사용 할 수 있습니다.

하지만 저희는 OpenZeppelin 라이브러리를 활용하여 ERC20 토큰을 작성하려 하기 때문에 추후 기능 테스트를 하기위한 용도로만 Remix IDE를 사용 하도록 하겠습니다.

### **Metamask**

Metamask는 이더리움 지갑을 관리 할 수 있는 브라우저 확장 프로그램 지갑으로, Remix IDE 및 뒤에 소개될 Truffle 프레임워크와 연동되어 사용됩니다.

이 문서에서는 크롬 확장 프로그램으로 설치해 사용하도록 하겠습니다. 설치방법은 크롬 웹스토어를 검색하거나 [Metamask 홈페이지](https://metamask.io/)를 통해 설치하시면 됩니다.

![Alt text](./images/metamask-homepage.png "Metamask 홈페이지")

확장 프로그램이 설치되면 새로운 지갑을 생성하거나 니모닉*Mnemonic*을 통해 지갑을 복구하시면 됩니다. 이때 만약 새로운 지갑을 생성했다면 생성시 사용된 니모닉을 잘 기억하고 있어야 합니다. 이 니모닉은 추후 테스넷 및 메인넷에 올릴때 사용됩니다.

설치된 Metamask는 다음과 같습니다.

<p align="center">
    <img src="./images/metamask-installed.png">
</p>

Step 1. Node.js와 npm
-
Truffle을 사용하기 위해서는 먼저 Node.js와 npm (node package manager)가 설치되어 있어야 합니다. npm의 경우 Node.js를 설치하면 같이 설치됩니다.

그럼 이제 Node.js를 설치해 봅시다. [Node.js 홈페이지](https://nodejs.org/)로 가서 플랫폼에 맞는 최신 버전을 다운로드 받아 설치하시면 됩니다. 이 문서에서는 2018년 9월 18일 최신 버전인 8.12.0 LTS 버전으로 설치하도록 하겠습니다.

![Alt text](./images/node-js-windows-download.png "Node.js 다운로드 페이지")

다운로드 받은 설치 파일을 실행합니다.

인스톨 후 Node.js가 설치가 잘 되었는지 확인하려면 커맨드창에서 버전 정보를 확인하면 됩니다.

```
PS> node --version
v8.12.0
```

마찬가지로 npm도 설치가 되었는지 확인해봅시다.

```
PS> npm --version
5.6.0
```

이제 토큰 생성을 위한 첫번째 준비가 완료되었습니다!

Step 2. Truffle
-
OpenZeppelin을 사용하기 위해선 [Truffle 프레임워크](https://truffleframework.com)가 필요합니다. 이전 단계에서 설치한 npm을 이용해 Truffle을 설치해보도록 합니다.

아래의 명령어를 커맨드창에 입력합니다.

```
PS> npm install -g truffle
```

###### ```-g``` 옵션은 글로벌 패키지에 추가하는 옵션으로 해당 프로젝트 뿐 아니라 다른 프로젝트를 만들때도 해당 패키지를 사용 할 수 있도록 하는 옵션입니다. 기회가 된다면 자세한 내용은 다른 문서에서 다루도록 하겠습니다.

Truffle 설치가 완료되었다면 이제 프로젝트 폴더에 Truffle을 적용해보도록 하겠습니다. 프로젝트 폴더를 생성하고 해당 위치에서 다음 명령어를 입력하면 됩니다.

```
PS> D:\workspace\ico\our-token> truffle init
```

설치후 기본적인 Truffle의 파일 구조는 다음과 같습니다.

이미지 추가

이제 다음 단계로 OpenZeppelin-Solidity를 설치해보도록 하겠습니다.

Step 3. Ganache
-
Ganache는 이더리움 노드 에뮬레이션 앱으로, 테스트넷이나 메인넷을 이용해 확인하는 것보다는 훨씬 빠르게 테스트를 진행할 수 있습니다.

사실 기본적으로 Truffle을 설치하면 콘솔 모드인 ganache-cli가 같이 설치됩니다. 하지만 명령창에서 확인하는 것보다는 GUI로 만들어진 Ganache를 사용하는 것이 보기 좋으므로 Ganache를 따로 설치하도록 하겠습니다.

Step 4. OpenZeppelin-Solidity
-
```
PS> npm init -y
PS> npm i -E openzeppelin-solidity
```

Dotenv
-
```
PS> npm i dotenv --save
```

Truffle-flattener
-
```
PS> npm i truffle-flattener
```

Infura
-
[인푸라](https://infura.io)

Truffle HDWalletProvider
-
```
PS> npm i tuffle-hdwallet-provider --save
```