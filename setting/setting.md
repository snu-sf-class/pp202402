# ⚠️  중요 ⚠️

**Copilot 등의 AI 자동완성 기능을 사용하다 Clone checker 등에 걸렸을 경우, 작성한 코드에 대한 모든 책임은 수강생 본인에게 있습니다.**

현재 2024년에 있어 현실적으로 이러한 툴의 사용을 막을 방법은 없으나, 자신이 작성한 코드를 본인이 설명하지 못하는 경우 과제에 불이익이 가해질 수 있음을 인지 바랍니다.

# 환경 설정
본 수업에서는 Scala 3과 Rust를 사용해 실습 및 과제를 진행합니다. 또한 git을 사용해 과제 제출을 진행할 것이니 수강자 여러분은 필히 git의 기초 개념과 사용법을 숙지해주시기 바랍니다. 

(git은 `git fetch`, `git commit`, `git push`, `git pull`, `git clone`만 사용할 수 있으면 됩니다.)

과제 진행은 IntelliJ, emacs, vim 등 수강생 분께서 원하시는 편집기를 사용해도 무방하나, **시험은 VSCode 환경에서 치뤄짐을 유의 바랍니다.** (또한 시험환경에서는 자동완성 기능 없이 Syntax Hightlighting만 지원됩니다.)

## git
과제 제출 및 채점은 전부 git으로 관리할 예정입니다. git의 사용법은 아래 링크에 있는 내용만 숙지하면 충분합니다. 

- https://www.pigno.se/barn/tutorial-git/docs/#/

위 링크에서 ssh-keygen 생성 부분이 깨져있는데, ssh-keygen 및 git의 설치법은 아래 링크를 참고 바랍니다.

- https://www.lainyzine.com/ko/article/creating-ssh-key-for-github/

숙제 코드는 저희 측에서 준비한 GitLab (사설 서버에서 돌릴 수 있는 GitHub이라고 보면 됨) 서버에 각 수강생 분들의 계정을 만들고, 그 계정에다 새로운 git 리포지토리를 만듦으로써 배포할 예정입니다. 

과제의 제출은 git push를 통해 해당 리포지토리의 코드를 업데이트 함으로써 이루어집니다. 제출 마감 기한의 23:59:59 까지 push된 코드를 기반으로 채점을 진행할 예정입니다.

## Scala 3

### JDK 17 설치
Scala 언어를 컴파일 하기 위해서는 JDK (Java Development Kit)가 컴퓨터에 설치되어 있어야 합니다. 다음 링크 중 하나에서 자신의 OS에 맞는 **JDK 17** (중요!) 버전을 다운받아 설치해주시기 바랍니다. 

- Adoptium Temurin OpenJDK - [Link](https://adoptium.net/temurin/releases/?version=17)
- Azul Zulu OpenJDK - [Link](https://www.azul.com/downloads/?version=java-17-lts&package=jdk#zulu)

본 수업에서는 위 둘 이외의 다른 JDK 버전 및 빌드를 사용하는 경우에 대해 과제의 유효성을 보장하지 않습니다.

### Scala 컴파일러 / Coursier / sbt 설치

Coursier는 (Java에서의 Maven/Ivy 등과 같은) Scala 버전 및 라이브러리 관리, sbt (simple/scala build tool)는 Scala 프로젝트를 빌드하여 jar 파일 또는 실행 파일을 만들기 위해 필요한 툴입니다. 

아래 링크에서 자신의 OS에 맞는 설치 방법을 따라주시면 Coursier (`cs`), sbt (`sbt`) 및 기초 Scala 컴파일러 (`scala`, `scalac`)가 자동으로 설치됩니다.

- https://www.scala-lang.org/download/

**주의**: 만약 Scala 3이 아닌 Scala 2가 컴퓨터에 설치되어 있다면, 본 과목에서는 Scala 3을 사용할 것이므로 기존 Scala 설치를 제거 후 재설치 등을 하여 Scala 3이 실행되는 것을 확인 바랍니다. (재설치는 `cs uninstall --all` 후 `cs setup`을 통해 할 수 있습니다.)

PowerShell / bash 등의 콘솔 창에서 다음과 비슷한 결과가 나오면 정상적으로 설치된 것입니다.
```
$ sbt --script-version
1.10.1
$ scala -version
Scala code runner version: 1.4.0
Scala version (default): 3.5.0
```

### VSCode
아래에서는 sbt를 통해 새로운 프로젝트를 만들고 이를 VSCode에서 불러오는 방법을 설명합니다. 과제 파일 등 기존 프로젝트를 불러오는 방법은 아래 설정을 따라한 다음, VSCode에서 build.sbt가 있는 폴더를 열면 됩니다.

<details>
<summary>접기/펼치기</summary>

#### 0. VSCode 설치

아래 링크에서 OS 설정에 맞는 VSCode를 다운받아 설치해주시기 바랍니다.

[https://code.visualstudio.com](https://code.visualstudio.com/)

#### 1. Metals 설정

![](./scala%20vscode%201.png)

Metals는 VSCode에서 Scala 개발환경을 관리하는 확장기능입니다. 왼쪽의 확장기능 (사각형 4개) 버튼을 누른 다음, 상단 창에서 metals를 검색하여 Scala (Metals)를 설치해주시기 바랍니다.


#### 2. 테스트 프로젝트 작성

![](./scala%20vscode%202.png)

VSCode 터미널에 아래 명령어를 입력하여 새로운 프로젝트를 작성해봅시다.
```
sbt new scala/scala3.g8
```
Scala 프로젝트의 이름 (name)을 작성하라는 창이 나올텐데, 적당히 아무 이름을 적어넣읍시다. (그림에선 pp202302)

#### 3. 프로젝트 열기

![](./scala%20vscode%203.png)

VSCode의 파일 탭을 누른 다음 Open Folder…를 선택 후 방금 만들어진 폴더를 선택합니다. (그림은 MacOS 지만 Windows도 비슷합니다.)

만들어진 폴더는 `sbt new` 를 실행한 후 가장 마지막에 뜬 `Template applied in (...)` 의 (…) 에 써져 있는 경로에 있습니다.

![](./scala%20vscode%204.png)

위와 같이 우하단에 New sbt workspace detected 라는 안내문이 뜨는 경우, Import build 를 선택해주시기 바랍니다.

#### 4. 코드 실행

![](./scala%20vscode%205.png)

위 절차를 마무리 했다면 왼쪽 패널에서 Explorer 창 (종이 2장 겹쳐진 아이콘) 을 연 후, `src/main/scala/Main.scala` 파일을 열어봅시다.

위와 같은 파일이 기본으로 들어있을 텐데, `@main def hello` 함수 위에 `run | debug` 라는 아이콘이 생겨있을 것입니다. 

`run` 을 누르면 `hello` 함수를 실행할 수 있습니다. 아래와 같은 창이 나올 것입니다.

![](./scala%20vscode%206.png)

#### 5. 테스트 코드 실행

![](./scala%20vscode%207.png)

src/test/scala/MySuite.scala 파일이 기본적으로 작성되어 있을 것입니다. 해당 파일을 클릭 후 열린 파일의 class 또는 test 함수 왼쪽에 있는 노란색 화살표 (그림에선 이미 한 번 실행해서 초록색으로 바뀌어져 있음)을 누르면 테스트를 실행할 수 있습니다.

![](./scala%20vscode%208.png)

테스트 기능에 대한 자세한 내용은 아래 링크를 참고 바랍니다.

https://scalameta.org/munit/docs/getting-started.html

</details>

### IntelliJ

IntelliJ IDEA 2023.2 버전 기반으로 설명되었으며, 이전 버전을 사용중이면 IntelliJ를 업그레이드하고, 이후 버전을 사용한다면 본 세팅문을 버전에 맞춰 적절히 적용하시기 바랍니다.

<details>
<summary>설정방법</summary>

#### 0. IntelliJ 설치
다음 링크에서 최신 IntelliJ IDEA **Community** 버전을 다운받을 수 있습니다.

[https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/ko-kr/idea/download/?section=mac)

#### 1. Scala Plugin 설치
![](./scala%20intellij%2001.jpg)

IntelliJ를 처음 켜고 나오는 화면에서 좌측의 Plugins에 들어갑니다.

![](./scala%20intellij%2002.jpg)

Scala와 Rust 플러그인을 찾아 설치 후 IntelliJ를 재부팅합니다.

#### 2. 새 프로젝트 생성 및 설정

![](./scala%20intellij%2003.png)

IntelliJ 실행시 나오는 화면 상단의 New Project 버튼을 눌러 새로운 프로젝트를 작성해봅시다. 

![](./scala%20intellij%2004.png)

다음 칸들을 설정합니다.

- Name: 적절한 아무 폴더 이름
- Location: 폴더를 둘 위치
- Langugage: **Scala** 선택
- Build System: **sbt** 선택
- JDK: 적절한 JDK 선택. 만약 붉은색으로 JDK가 없다고 나오면 아래의 3.1을 참고하여 JDK를 설정합시다.
- sbt: 1.9 이상의 최신 버전 선택
- Scala: **3.3.0 선택 (중요!)**

다 했으면 우하단의 Create를 누릅니다.

#### 3. JDK 설정

![](./scala%20intellij%2005.png)

Scala는 Java 기반의 언어기 때문에 JDK (Java Development Kit)를 깔아야 프로그래밍을 진행할 수 있습니다.

다음처럼 **\<No SDK\>** 가 떠있는 경우 IntelliJ가 JDK를 스스로 깔거나, 사용자가 수동으로 JDK를 설치한 다음 JDK가 있는 폴더의 경로를 지정해주어야 합니다.

본 수업에서 **JDK 버전은 Java 17을 사용하며, Azul Zulu 또는 Eclipse Temurin을 권장합니다.**

**설정 방법**

1. **Add SDK > JDK…** 를 눌러 기존에 PC에 깔린 JDK를 설정할 수 있습니다.
2. IntelliJ가 알아서 설치하게 하고 싶은 경우 Add SDK > Download JDK… 를 선택한 후, 다음과 같이 **버전 17**, 벤더로 **Azul Zulu**를 설정한 후 다운로드를 진행합니다.

    a. MacOS의 경우, CPU로 Apple Silicon (M1, M2 등)을 사용 중이라면 aarch64 버전을 선택하면 됩니다.

![](./scala%20intellij%2006.png)

#### 4. 프로그램 작성

![](./scala%20intellij%2007.png)

좌상단의 드롭다운 리스트에서 Project를 선택하면 프로젝트 폴더의 구조를 볼 수 있습니다. 기본적으로 src/main/scala 폴더에 프로그램을 작성하면 됩니다.

![](./scala%20intellij%2008.png)

src/main/scala 폴더에서 우측 키를 눌러 New > Scala Class/File을 클릭합니다. 파일 제목은 Main.scala로 설정해봅시다.

![](./scala%20intellij%2009.png)

다음과 같은 팝업이 나올텐데, 아무 거나 클릭하고 이름으론 Main을 넣은 뒤 엔터 키를 쳐봅시다. 어차피 안의 내용은 전부 삭제할 것입니다.

![](./scala%20intellij%2010.png)

기존 코드를 지우고 다음과 같이 프로그램을 작성해봅시다.

![](./scala%20intellij%2011.png)

@main def hello() 왼쪽에 초록색 재생 버튼이 있습니다. 클릭한 다음 나오는 Run ‘hello’를 누르면 화면 실행 결과가 표시됩니다.

</details>


<details>
<summary>기존 프로젝트 불러오기 (과제 등)</summary>

이 패널에서는 위 VSCode로 작성한 프로젝트를 불러와 보겠습니다. 

#### 1. 프로젝트 열기

![](./scala%20intellij%2021.png)

IntelliJ를 새로 실행하고 왼쪽의 Projects 패널을 연 다음, 우상단의 Open 버튼을 누릅니다.

![](./scala%20intellij%2022.png)

기존의 Scala 프로젝트 폴더 (build.sbt 파일이 있는 폴더)를 찾아서 열어봅시다.

![](./scala%20intellij%2023.png)

`build.sbt` 파일이 있다면 이런 창이 뜰 수 있는데, sbt project를 선택한 후 OK를 누릅시다.

#### 2. 파일 실행

![](./scala%20intellij%2024.png)

과제 프로젝트 등에는 src 폴더 아래에 main과 test 폴더가 있을 것입니다. 각각의 폴더에 있는 Scala 파일을 열면 코드 왼쪽에 초록색 실행 버튼이 있는데, 버튼을 누르면 함수의 실행 결과를 볼 수 있습니다.

</details>


## Rust

### (필수!) 기반 컴파일러 설치 - rustup + cargo + rustc 

아래 사이트에 나와있는 대로 rustup을 설치합시다. rustup은 Rust의 버전을 관리할 수 있는 툴이며, 이를 통해 Rust 프로젝트 및 라이브러리 의존성을 관리하는 `cargo`, Rust 컴파일러인 `rustc`를 설치할 수 있습니다.

- https://www.rust-lang.org/tools/install
    - Linux/macOS의 경우 링크를 열자마자 나오는 `curl --proto ...` 를 콘솔에 넣으면 됩니다.
    - Windows의 경우 아래 링크에서 rustup-init.exe 의 링크를 찾아 설치할 수 있습니다.
    - https://forge.rust-lang.org/infra/other-installation-methods.html

실행했다면 다음을 콘솔창에 입력하여 설치가 제대로 되었는지 확인해봅시다.

```
> cargo --version
cargo 1.72.0 (103a7ff2e 2023-08-15)
```

위와 같이 1.72 버전 이상이 설치되었다면 정상입니다.

만약 기존에 rustup이 설치된 상태라면 `rustup update`를 입력하여 최신 버전으로 업데이트를 하도록 합시다.

```
> cargo new hello_cargo
```
콘솔 창에서 위 코드를 입력하면 빈 cargo 프로젝트를 만들 수 있습니다.


```bash
> cargo fmt # formatting the code automatically
```
콘솔 창에서 위 코드를 입력하면 프로젝트의 코드를 보기 좋은 형태로 자동으로 수정해줍니다. 
(예 : 들여쓰기, 불필요한 괄호)

```bash
> cargo clippy # printing problems of the code and how to fix them
```
콘솔 창에서 위 코드를 입력하면 프로젝트의 코드에 있는 경고사항을 찾아서 어떻게 고칠 수 있는지 출력합니다.  
(예 : 쓰이지 않은 variable 삭제, 권장되지 않는 (대체 가능한) 라이브러리 함수 등)

### VSCode

![](./rust%20vscode%201.png)

위와 같이 vscode 확장에서 `rust-analyzer`를 찾아 설치해 줍시다.

그 다음, 앞에서 만든 새 cargo 프로젝트를 vscode에서 열어봅시다.

![](./rust%20vscode%202.png)

src/main.rs에 기본적인 hello world 코드가 있습니다. `fn main()` 위의 `Run`을 클릭하면 메인함수를 실행할 수 있습니다.

main함수가 argument를 받는 경우에는 `Run`을 클릭했을 때 에러가 날 수 있으며, 이 경우 콘솔창에서 `cargo run 42` 와 같은 명령어로 42라는 argument를 넘겨줄 수 있습니다.

![](./rust%20vscode%203.png)

위와 같이 test를 작성할 경우, `Run Test`를 클릭해서 개별 test를, `Run Tests`를 클릭해서 전체 test를 실행할 수 있습니다. 

### IntelliJ

![](./rust%20intellij%201.png)

IntelliJ 초기 시작시에 나오는 Plugins에 Rust 플러그인이 있습니다. 먼저 설치해줍시다.

그 다음 아래와 같이 cargo 프로젝트를 열면 자동으로 Rust 프로젝트를 사용할 수 있게 됩니다.

![](./rust%20intellij%202.png)

src/main.rs를 열면 fn main() 왼쪽에 실행 버튼이 있습니다. 버튼을 눌러 main 함수를 실행할 수 있습니다. Rust 프로젝트를 처음 열었을 때 Updating crate.io index라고 뜨면서 굉장히 오래 걸리는 경우가 있습니다. 끝날 때까지 인내심을 가지고 기다려줍시다.
