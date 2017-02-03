# 언어 학자

[issues]: https://github.com/github/linguist/issues
[new-issue]: https://github.com/github/linguist/issues/new

이 라이브러리는 언어 분석 그래프를, 방울 언어를 감지 바이너리 또는 vendored 파일을 무시 차이점에 생성 된 파일을 억제하고 생성하는 GitHub.com에 사용됩니다.

난 그저 지금이 권한을 테스트입니다 ...

## 문제 해결

이 이유는 - ### 내 저장소가 잘못된 언어로 검출?

![language stats bar](https://cloud.githubusercontent.com/assets/173/5562290/48e24654-8ddf-11e4-8fe7-735b0ce3a0d3.png)

0 해당 언어로 식별 된 파일의 목록을 볼 수있는 통계 표시 줄에 언어의 이름을 클릭합니다.
당신이 작성하지 않은 파일을 볼 수 0 경우, (/lib/linguist/vendor.yml) 중 하나에 파일을 이동을 고려하거나 무시하도록 (#overrides) 기능을 [paths for vendored code] 사용합니다. [manual overrides]
0 파일이 잘못 분류되는 경우, 다른 사람이 이미이 문제를보고이 [open issues] [issues] 있는지 검색합니다. 추가 할 수있는 모든 정보, 공용 저장소에 특히 링크, 도움이됩니다.
0이이 오 분류 전혀보고 된 문제없고, 저장소에 대한 링크 또는 [open an issue] [new-issue] 잘못 분류되는 코드의 샘플을 포함합니다.

###이 파일의 구문 강조에 문제가 - 그리고 나는 그것에 대해 죄송합니다.

언어 학자는 파일의 언어를 감지하지만 실제 구문 강조는 서브 모듈의 집합으로이 프로젝트에 포함 된 언어 문법의 세트 (https://github.com/github/linguist/blob/master/vendor에 의해 제공됩니다 /README.md). [and may be found here]

당신이에 문제가 발생하면 구문 강조 GitHub의에서 ** 문법은 우리가 언어 학자 보석 등 업스트림 버그 수정을 만들 때마다 업데이트됩니다 **. 여기 없어 상류 문법 저장소에 문제를보고 자동으로로 통합되어주세요 고정되어있다.

## 오버라이드 (override)

언어 학자들은 언어의 정의와 vendored 경로에 대한 다른 사용자 지정 전략을 지원합니다.

### 사용 gitattributes

프로젝트에`.gitattributes` 파일을 추가하고 '언어 학자-documentation`,`언어 학자-language`하고,`언어 학자-vendored`을 설정 오버라이드 (override) 할 파일에 대한 표준 자식 스타일의 경로 매처 (matcher)를 사용합니다. `.gitattributes`는 언어 통계치를 결정하는 데 사용되지만, 강조 파일을 구문을 사용할 수 없다. 수동 구문 강조를 설정하려면 (# 사용-이맥스 또는-VIM-모드 라인)를 사용합니다. [Vim or Emacs modelines]

```
$ 고양이 .gitattributes
* .rb 언어학 언어 = 자바
```

당신의 자식의 repo에, 자바 스크립트 라이브러리와 같이 작성하지 않은 코드를 검사하는 것은 일반적인 관행이지만,이 종종 프로젝트의 언어 통계를 팽창 심지어 프로젝트가 다른 언어로 표시 될 수 있습니다. 기본적으로, 언어학에서 정의 된 경로들 모두를 처리 (https://github.com/github/linguist/blob/master/lib/linguist/vendor.yml) 언어 통계에 포함되지 않기 때문에 vendored하고 저장소. [lib/linguist/vendor.yml]

공급 업체 또는 취소 업체 경로하기 위해`언어 학자-vendored` 속성을 사용합니다.

```
$ 고양이 .gitattributes
특수 vendored 경로 / * 언어 학자-vendored
Jquery.js 언어 학자-vendored = 거짓
```

그냥 vendored 파일처럼, 언어 학자 프로젝트의 언어 통계에서 문서 파일을 제외합니다. (lib 디렉토리 [lib/linguist/documentation.yml] / 언어학 / documentation.yml)는 일반 문서 경로를 나열하고 저장소의 언어 통계에서 그들을 제외합니다.

문서로 해제 경로 또는를 표시하기 위해`언어 학자-documentation` 속성을 사용합니다.

```
$ 고양이 .gitattributes
프로젝트 문서 / * 언어 학자-문서
허위 문서 / formatter.rb 언어 학자-문서 =
```

#### 생성 된 파일 검출

모든 일반 텍스트 파일에 해당 소스 파일입니다. 축소 된 JS 컴파일 커피 스크립트와 같은 생성 된 파일을 검색 및 언어 통계에서 제외 될 수 있습니다. 추가 보너스로, vendored 및 문서 파일과는 달리,이 파일은 차이점 억제된다.

```루비
언어학 :: FileBlob.new ( "underscore.min.js"). 생성? # => 참
```

(https://github.com/github/linguist/blob/master/lib/linguist/generated.rb)를 [Linguist::Generated#generated?] 참조하십시오.

### 이맥스 또는 빔의 모드 라인을 사용하여

또한, 단일 파일의 언어를 설정하기 위해 빔 또는 이맥스 스타일의 모드 라인을 사용할 수 있습니다. 모드 라인은 파일에 삽입 될 수 있습니다 및 GitHub.com에서 파일을 구문-강조하는 방법을 결정할 때 존중

##### 빔
```
다양한 스타일의 # 몇 가지 예 :
정력 : 구문 = 자바
정력 : 설정 구문 = 루비 :
정력 : 설정 파일 형식 = 프롤로그 :
정력 : 설정 피트 = CPP :
```

##### 이맥스
```
- * - 모드 : PHP - * -
```

## 사용

보석을 설치합니다 :

```
$ 보석은 github에-언어 학자 설치
```

그런 다음 응용 프로그램에서 사용

```루비
필요 '견고한'
'언어학'을 필요로

REPO = 견고한 :: Repository.new ( '.')
프로젝트 = 언어 학자 :: Repository.new (REPO, repo.head.target_id)
Project.language # => "루비"
Project.languages ​​# { "Ruby" => 119387 } =>
```

이 통계는 또한`linguist` 실행하여 인쇄됩니다. 당신은을 사용할 수 있습니다
`--breakdown` 플래그, 이진 언어 별 파일도 출력 고장 것이다.

이 저장소 자체의 루트 디렉토리에`linguist`를 실행 시도 할 수 있습니다 :

```
$ 간부 언어 학자 번들 --breakdown

100.00 % 루비

루비:
Gemfile
Rakefile
빈 / 언어학
GitHub의-linguist.gemspec
lib/linguist.rb
…
```

## 기여

우리 (CONTRIBUTING.md)를 확인하시기 바랍니다. [contributing guidelines]

## 라이센스

이 보석에 포함 된 언어의 문법은 자신의 저장소 '에 의해 보호됩니다
각각의 라이센스. `grammars.yml` 각 문법에 대한 저장소를 지정합니다.

다른 모든 파일은 MIT 라이센스에 의해 보호됩니다,`LICENSE`를 참조하십시오.
