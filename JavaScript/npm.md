## Dependencies vs devDependencies

### Dependencies

- production에서 필요한 패키지들
- npm package 다운 시 함께 설치됨

### devDependencies

- 로컬 개발이나 테스팅 환경에서 필요한 패키지들
- npm package 다운 시 무시됨

> 사용하지 않는 패키지  
> `import`를 찾지 못해 최종 번들에는 포함이 되지 않는다. 즉, 번들 크기에는 영향이 없다.  
> 하지만 제거해 주는 것이 좋다.

## lock file

해당 파일이 없을 때에는 어떤 버전의 패키지가 설치될 것인지 확신할 수 없었다.  
`package.json`에서 정확히 명시되어 있지 않은 패키지 버전들이 lock 파일에 명시되어있다.  
lock file이 있을 경우 동일한 버전을 다운받게 되어 다른 개발환경으로 인해 발생하는 문제를 방지할 수 있다.

## 버전

[Semantic Versioning](https://semver.org/)(SemVer)을 따르고 있으며 `MAJOR.MINOR.PATCH`의 형태이다. 의미는 다음과 같다.

- MAJOR version when you make incompatible API changes
- MINOR version when you add functionality in a backward compatible manner
- PATCH version when you make backward compatible bug fixes

| 상태                             | 단계          | 규칙                                                        | 예시  |
| -------------------------------- | ------------- | ----------------------------------------------------------- | ----- |
| 출시                             | New product   | 1.0.0으로 시작                                              | 1.0.0 |
| 이전 버전과 호환되는 버그 수정   | Patch release | 세 번째 자리의 숫자를 증가                                  | 1.0.1 |
| 이전 버전과 호환되는 새로운 기능 | Minor release | 가운데 숫자를 증가하고 마지막 숫자를 0으로 초기화           | 1.1.0 |
| 이전 버전과 호환성이 깨진 변경   | Major release | 첫 번째 자리의 숫자를 증가하고 나머지 숫자들을 0으로 초기화 | 2.0.0 |

### 범위 지정

❶ **`X`, `x`, `*`**

MAJOR, MINOR, PATCH의 숫자 값 중 하나를 대체할 수 있다.

- `*`: >=0.0.0
- `1.x`: >=1.0.0 <2.0.0
- `1.2.x`: >=1.2.0 <1.3.0

❷ **Tilde`~`**

MINOR 버전이 지정되어 있을 경우 PATCH 변경을 허용한다.  
그렇지 않을 경우 MINOR까지 변경을 허용한다.

- `~1.2.3`: >=1.2.3 <1.3.0
- `~1.2`: >=1.2.0 <1.3.0 (1.2.x와 동일)
- `~1`: >=1.0.0 <2.0.0 (1.x와 동일)

❸ **Caret`^`**

이전 버전과의 호환성이 보장되도록 업데이트한다.

- `^1.2.3`: >=1.2.3 <2.0.0
- `^1.2`: >=1.2.0 <2.0.0
- `^1`: >=1.0.0 <2.0.0

다만, `1.0.0` 미만의 버전일 경우 큰 변경이 일어날 수도 있기 때문에 Tilde처럼 동작한다.

- `^0.2.3`: >=0.2.3 <0.3.0

또한 아래 예시와 같이 `0.0.x`의 경우 지정 버전만을 사용한다.

- `^0.0.3`: >=0.0.3 <0.0.4 (0.0.3과 동일)

## npm의 단점

### 버전

현재는 위에서 설명했듯이 `package-lock.json` 파일을 통해 버전을 고정하여 해당 문제를 해결한 상태이다.  
기존에는 워크스페이스마다 버전이 일치하지 않을 수 있다는 위험이 존재했다.

### 시간

순차적인 설치로 인해 설치 소요 시간이 길다.

## yarn

yarn은 위의 문제들의 해결과 여러 기능을 추가해 나왔다.

### yarn.lock

yarn.lock 파일을 이용해 일관적이지 않은 패키지 버전 문제를 해결했다.

### checksum

checksum을 사용해 패키지가 제대로 설치되었는지 확인한다.  
yarn.lock 파일의 `resolved` 주소 뒤 해시값을 확인할 수 있다.

### 속도

캐시 사용 및 병렬 설치로 속도가 빠르다.

## 참고 자료

- [About semantic versioning - npm docs](https://docs.npmjs.com/about-semantic-versioning)
- [Semantic Versioning 2.0.0](https://semver.org/)
- [node-semver README.md](https://github.com/npm/node-semver#readme)
- [Guide to managing npm packages in your package.json](https://medium.com/openclassrooms-product-design-and-engineering/guide-to-managing-npm-packages-in-your-package-json-d315fe2ccab0)
