---
layout: post
title:  "Foundry forge로 이더리움 스마트 컨트랙트 분석하기"
date:   2024-11-24 01:30:00 +0900
tags: ethereum smart-contract foundry
---

Foundry forge를 이용해 이더리움 스마트 컨트랙트를 테스트하고 스크립트를 돌려봅시다.

## 도입
원래는 이더리움 스마트 컨트랙트 배포 및 테스트를 위해 [Remix IDE](https://remix.ethereum.org/)를 사용했었다.
하지만 속도와 기능에서 아쉬울 때가 많았고, 이에 [Foundry](https://github.com/foundry-rs/foundry)를 사용하고 있다.

## 설치
[공식 문서](https://book.getfoundry.sh/getting-started/installation)

```bash
curl -L https://foundry.paradigm.xyz | bash
```

```bash
foundryup
```

## 프로젝트 생성

```bash
forge init project-name
```

init을 하면 프로젝트 폴더 안에 `src`, `test`, `script` 폴더 등이 생성된다.

src에 컨트랙트 파일을 두고, test에서  testcase를 작성한다. script에는 솔버 등 스크립트를 작성한다.

## 테스팅
[공식 문서](https://book.getfoundry.sh/reference/forge/forge-test)
```bash
forge test
```
forge test를 이용해 테스트를 실행할 수 있다. 

```bash
forge test -vvvvv
```
verbose를 추가해 내부 트랜잭션과 호출, 리턴값 등을 확인할 수 있다.

## 스크립팅
[공식 문서](https://book.getfoundry.sh/reference/forge/forge-script)
```bash
forge script script-name.s.sol
```
forge script를 이용해 스크립트를 실행할 수 있다.

```bash
forge script script-name.s.sol --rpc-url <RPC_URL>
```
특정 RPC URL을 지정해 스크립트를 실행할 수 있다.

```bash
forge script script-name.s.sol --broadcast
```
스크립트를 브로드캐스트해 트랜잭션을 전송할 수 있다. 안쓰면 (마치 테스트처럼) 되는지 확인만 된다.

`Failed to get EIP-1559 fees` 가 뜨면 `--legacy` 옵션을 추가한다.

```bash
forge script script-name.s.sol --broadcast --legacy
```


## Foundry용 함수
대부분이 기존 js 문법과 동일하게 작성되지만, 테스트 및 스크립팅을 위해 몇 가지 사용할 새 함수들이 있다.

### vm.addr
[공식 문서](https://book.getfoundry.sh/cheatcodes/addr)
```js
address vm.addr(uint256 _privateKey)
```
private key로부터 주소를 생성한다.

### vm.deal
[공식 문서](https://book.getfoundry.sh/cheatcodes/deal)
```js
vm.deal(address _address, uint256 _amount)
```
해당 주소에 이더를 할당한다.

### vm.prank
[공식 문서](https://book.getfoundry.sh/cheatcodes/prank)
```js
vm.prank(address _address)
```
다음 함수 호출(vm.뭐시기 제외)이 해당 주소로부터 실행된다.

### vm.load
[공식 문서](https://book.getfoundry.sh/cheatcodes/load)
```js
vm.load(address _address, bytes32 _slot)
```
해당 주소(컨트랙트)의 해당 슬롯 값을 반환한다.

## console.log
[공식 문서](https://book.getfoundry.sh/reference/forge-std/console-log)
```js
console.logInt(int i)
console.logUint(uint i)
console.logString(string memory s)
console.logBool(bool b)
console.logAddress(address a)
console.logBytes(bytes memory b)
console.logBytes1(bytes1 b)
console.logBytes2(bytes2 b)
…
console.logBytes32(bytes32 b)
```

### vm.record
[공식 문서](https://book.getfoundry.sh/cheatcodes/record)
```js
vm.record()
```
storage에 대한 읽기와 쓰기를 기록하기 시작한다. 확인은 vm.accesses()를 사용한다.

### vm.accesses
[공식 문서](https://book.getfoundry.sh/cheatcodes/accesses)
```js
(bytes32[] memory reads, bytes32[] memory writes) = vm.accesses(
  address
);
```
vm.record()에 의해 기록된 내용을 확인한다.
인자로는 컨트랙트 주소를 주면 된다.

### vm.broadcast
[공식 문서](https://book.getfoundry.sh/cheatcodes/broadcast)
```js
vm.broadcast(address or uint256)
```
직후 트랜잭션을 실행할 주체를 선택한다.
주소를 줘도 되고 프라이빗키를 줘도 된다.
한번 트랜잭션을 보내고 나면 초기화되니, 계속 유지하고 싶다면 vm.startBroadcast를 써야 한다.

### vm.startBroadcast
[공식 문서](https://book.getfoundry.sh/cheatcodes/start-broadcast)
```js
vm.startBroadcast(address or uint256)
```
트랜잭션을 브로드캐스트할 때 사용할 주체를 지정한다. vm.stopBroadcast()를 쓸 때까지는 계속 유지된다.

### vm.stopBroadcast
[공식 문서](https://book.getfoundry.sh/cheatcodes/stop-broadcast)
```js
vm.stopBroadcast()
```
vm.startBroadcast()에 의해 지정된 주체를 초기화한다.
