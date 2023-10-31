# AngularJS Git Commit Message Conventions
#### [Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153#commit-message-conventions)
---

# 목표
- 스크립트로 CHANGELOG.md를 작성할 수 있다.
- git bisect를 사용하여 중요하지 않은 커밋을 무시할 수 있다. (Formatting과 같이 중요하지 않은 커밋인 경우)
  
  >  git bisect : 커밋의 특정 범위 내에서 이진탐색을 통해 문제가 발생한 최초의 커밋을 찾는데 도움을 주는 git의 기능
- 커밋 기록 탐색시 더 좋은 정보를 제공한다.

# CHANGELOG.md 생성
변경 로그에서는 다음의 3가지 내용을 사용한다.
- 새로운 기능 (new Feature)
- 버그 수정 (bug fixs)
- 주요 변경 사항 (breaking changes)

위의 3가지 목록들은 릴리즈를 수행할 때 관련 커밋에 대한 링크와 함께 스크립트로 생성할 수 있다.
물론 실제 릴리스 전에 이 변경 로그를 편집할 수도 있지만 추가적인 파일이 필요할 것이다.

마지막 릴리즈 이후의 모든 제목 목록을 출력한다. (※ 제목 (subject) : 커밋 메세지의 첫 번째 줄)
```shell
git log <last tag> HEAD --pretty=format:%s
```
해당 릴리스의 새로운 기능
```shell
git log <last release> HEAD --grep feature
```
## 중요하지 않은 커밋 식별
- Formatting changes (공백 및 빈 줄 추가/제거, 들여쓰기)
- 세미콜론 및 주석 누락
등의 중요하지 않은 커밋의 경우 무시할 수 있다. (논리적 변경이 아님)

git bisect을 통한 이진 탐색을 할 때 위와 같은 중요하지 않은 커밋은 무시할 수 있다.
```shell
git bisect skip $(git rev-list --grep irrelevant <good place> HEAD)
```
## 기록 조회 시 더 많은 정보 제공
다음과 같이 일종의 'Context'(맥락) 정보를 추가해야 한다. (최근 몇 개의 Angular 커밋에서 가져온 내용)
- Fix small typo in docs widget (tutorial instructions)
- Fix test for scenario.Application - should remove old iframe
- docs - various doc fixes
- docs - stripping extra new lines
- Replaced double line break with single when text is fetched from Google
- Added support for properties in documentation

모든 메시지들은 변경 사항의 위치를 명시하려고 하지만 어떠한 규칙이 존재하지는 않는다.

다음 메시지를 보자.
- fix comment stripping
- fixing broken links
- Bit of refactoring
- Check whether links do exist and throw exception
- Fix sitemap include (to work on case sensitive linux)

이러한 메시지들은 변경 사항의 위치를 명시하지 않는다.
그래서 아마도 코드 부분: docs, docs-parser, compiler, scenario-runner, …와 같은 내용을 추가해야 할 것이다.
내용을 찾기 위해 파일 변경 내역을 확인할 수는 있지만, 이것은 많은 시간이 소요된다.

그리고 Git 기록을 살펴보면 모두가 변경 사항의 위치를 명시하려고 노력하지만 어떠한 규칙은 없다는 것을 알 수 있다.

---

# Format of the commit message (커밋 메시지 형식)
```shell
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```
커밋 메시지의 각 줄은 100자 이내로 작성되어야 한다. 이렇게 하면 GitHub 및 다양한 Git 도구에서 메시지를 쉽게 읽을 수 있다.

## Subject Line (제목)
제목에는 변경사항에 대한 간결한 설명이 포함된다.

### 커밋의 유형 : `<type>`에 들어갈 수 있는 항목들
- feat (feature) : 새로운 기능 추가
- fix (bug fix) : 버그 수정
- docs (documentation) : 문서 관련 내용
- style (formatting, missing semi colons, …) : 코드 스타일 변경
- refactor : 코드 리팩토링
- test (when adding missing tests) : 테스트 추가
- build : 빌드 관련 파일 수정
- ci : CI 설정 파일 수정
- perf : 성능 개선
- chore (maintain) : 그 외의 수정 (유지보수 관련 작업 등)

### 커밋의 영향 범위 : `<scope>`에 들어갈 수 있는 항목들
커밋 변경 사항이 어떤 부분에 영향을 미치는지를 명시하는 것으로, 예를 들면 $location, $browser, $compile, $rootScope, ngHref, ngClick, ngView 등이 될 수 있다.
- 커밋이 어떤 부분 또는 모듈과 관련이 있는지를 명시적으로 나타내어 다른 개발자가 커밋의 범위를 이해하도록 도와준다.
- scope는 생략 가능하다.

### `<subject>`
- 명령문 형태와 현재 시제를 사용해야 한다. ("changed"나 "changes"가 아닌, "change"를 사용)
- 첫 글자는 대문자가 아닌 소문자로 사용한다.
- 문장 끝에 마침표(.)를 붙이지 말아야 한다.

## Message body (내용)
- 명령문 형태와 현재 시제를 사용해야 한다. ("changed"나 "changes"가 아닌, "change"를 사용)
- 변경 이유와 이전코드와의 차이점을 포함시켜야 한다.
> http://365git.tumblr.com/post/3308646748/writing-git-commit-messages http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

## Message footer
### Breaking changes (주요 변경 내용)
모든 주요 변경 사항은 다음 내용을 Message footer에 포함하고 있어야 한다.

- 변경 사항에 대한 설명 (description of the change)
- 변경 사유[정당성] (justification)
- 마이그레이션 참고 사항 (migration notes)

이를 통해 커밋에서 발생하는 파괴적인 변경 사항을 명확하게 문서화하고, 다른 개발자들이 이 변경 사항에 대응하는 방법을 이해할 수 있다.

```shell
BREAKING CHANGE: isolate scope bindings definition has changed and
    the inject option for the directive controller injection was removed.
    
    To migrate the code follow the example below:
    
    Before:
    
    scope: {
      myAttr: 'attribute',
      myBind: 'bind',
      myExpression: 'expression',
      myEval: 'evaluate',
      myAccessor: 'accessor'
    }
    
    After:
    
    scope: {
      myAttr: '@',
      myBind: '@',
      myExpression: '&',
      // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
      myAccessor: '=' // in directive's template change myAccessor() to myAccessor
    }
    
    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```
### Referencing Issues (이슈 참조)
해결된 이슈에 대한 참조는 `Closes #<이슈번호>` 형태로 Message footer에 추가한다.

```
이슈가 하나인 경우
Closes #234

이슈가 여러개인 경우
Closes #123, #245, #992
```
이를 통해 커밋과 관련된 이슈를 자세히 추적할 수 있으며, 이슈가 어떤 커밋에서 해결되었는지를 파악하기 용이해진다.

# Examples
> - Installing a new dependency
-> **build: Install new dependency**
- Restructuring folder structure
-> **refactor: Reorganize folder layout**
- Updating/Changing stylesheets
-> **style: Update style sheets**
- Changing the name of an existing component
-> **refactor: Rename component**


```shell
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```shell
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
```

```shell
feat(directive): ng:disabled, ng:checked, ng:multiple, ng:readonly, ng:selected

New directives for proper binding these attributes in older browsers (IE).
Added coresponding description, live examples and e2e tests.

Closes #351
```

```shell
style($location): add couple of missing semi colons
```

```shell
docs(guide): updated fixed docs from Google Docs

Couple of typos fixed:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```

```shell
feat($compile): simplify isolate scope bindings

Changed the isolate scope binding options to:
  - @attr - attribute binding (including interpolation)
  - =model - by-directional model binding
  - &expr - expression execution binding

This change simplifies the terminology as well as
number of choices available to the developer. It
also supports local name aliasing from the parent.

BREAKING CHANGE: isolate scope bindings definition has changed and
the inject option for the directive controller injection was removed.

To migrate the code follow the example below:

Before:

scope: {
  myAttr: 'attribute',
  myBind: 'bind',
  myExpression: 'expression',
  myEval: 'evaluate',
  myAccessor: 'accessor'
}

After:

scope: {
  myAttr: '@',
  myBind: '@',
  myExpression: '&',
  // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
  myAccessor: '=' // in directive's template change myAccessor() to myAccessor
}

The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```
