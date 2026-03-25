## 1단계: Codespace를 시작하고 코드를 푸시하기

### Codespaces가 왜 중요한가요?

**Codespace**는 저장소의 구성 파일로 정의되는 클라우드에서 호스팅되는 개발 환경입니다. 이를 통해 프로젝트에 특화된 반복 가능한 개발 환경을 만들어 개발자 온보딩을 간소화하고, 유명한 "내 컴퓨터에서는 되는데!" 문제를 방지합니다 😎

각 Codespace는 [Dev Container 사양](https://containers.dev/implementors/spec/)을 따르며 GitHub에서 [Docker 컨테이너](https://code.visualstudio.com/docs/devcontainers/containers)로 호스팅됩니다.

하지만 걱정하지 마세요! Docker를 알 필요도, 컴퓨터에 설치할 필요도 없습니다!

> [!TIP]
> Dev Container 구성이 저장소의 일부이므로, 자체 Docker 호스트를 사용하여 로컬에서도 사용할 수 있습니다. 편리하죠!

Codespace는 로컬 개발과 비교하여 여러 장점/기능이 있습니다. 몇 가지를 소개하면:

- 저장소 페이지에서 직접 Codespace를 시작할 수 있습니다.
- 브라우저에서 개발 가능. IDE 설치가 필요 없습니다.
  - 로컬에 설치된 VS Code를 원격 Codespace에 연결하는 옵션도 있습니다.
- 프로젝트 실행에 필요한 모든 것을 사전 구성:
  - **[features](https://containers.dev/features)**를 추가하여 일반적인 개발 도구를 설치.
  - Codespace 생명주기의 다양한 단계에서 스크립트 실행 _(예: python/npm 패키지 설치)_.
  - 프로젝트 요구사항에 맞게 VS Code 설정과 확장 프로그램 설정.
- 빠른 인터넷 접속 (컨테이너가 데이터센터에 있으므로).

> [!TIP]
> Codespaces는 풀 리퀘스트 리뷰 같은 단기 상황에서도 유용합니다. 들어오는 코드 변경사항을 테스트하기 위해 올바른 환경이 설정되어 있는지 확인할 필요가 없습니다.

시작해 봅시다! Codespace를 시작하고, 애플리케이션을 실행하고, 변경하고, 푸시하겠습니다. 일반적인 개발 과정처럼요! 🤓

### ⌨️ 활동: Codespace 시작하기

1. 두 번째 탭을 열고 이 저장소로 이동하세요. **Code** 탭에 있는지 확인하세요.

1. 파일 목록 오른쪽 위에 있는 녹색 **<> Code** 버튼을 클릭하세요.

   <img width="300" alt="녹색 Code 버튼" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/green-code-button.png" />

1. **Codespaces** 탭을 선택하고 **Create codespace on main** 버튼을 클릭하세요. VS Code가 실행되는 새 창이 열리고 원격 Codespace에 연결됩니다. Codespace가 생성될 때까지 몇 분 기다리세요.

1. VS Code 창의 왼쪽 하단에서 원격 연결 상태를 확인하세요.

   <img width="350" alt="VS Code의 원격 연결 상태" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/remote-connection-status.png"/>

> [!TIP]
> 저장소에 구성이 포함되어 있지 않으면 GitHub는 [universal](https://github.com/devcontainers/images/tree/main/src/universal) Codespace 이미지를 사용합니다. 여러 유용하고 일반적으로 사용되는 도구가 포함되어 있습니다.

### ⌨️ 활동: 애플리케이션 실행하기

1. VS Code Codespace에 있는지 확인하세요.

1. 왼쪽 사이드바에서 **탐색기** 탭을 선택하고 `src/hello.py` 파일을 여세요.

   <img width="250" alt="VS Code 탐색기 탭" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/vs-code-explorer-tab.png" />

1. 하단 패널에서 **터미널** 탭을 선택하세요.

   <img width="350" alt="VS Code 터미널 탭" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/vs-code-terminal-tab.png" />

1. Codespace의 원격 터미널에 다음 명령을 붙여넣어 여러 도구의 설치된 버전을 확인하세요. 나중에 비교할 수 있도록 버전을 메모해 두세요.

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

1. Codespace의 원격 터미널에 다음 명령을 붙여넣어 Python 프로그램을 실행하세요.

   ```bash
   python src/hello.py
   ```

### ⌨️ 활동: Codespace에서 저장소로 변경사항 푸시하기

1. `src/hello.py` 파일의 내용을 다음으로 교체하고 파일을 저장하세요.

   ```py
   print("Hello World!")
   ```

1. 메시지를 업데이트했으면, 변경사항을 커밋하고 GitHub에 푸시하세요. VS Code의 소스 제어 도구를 사용하거나 아래 터미널 명령을 사용하세요.

   ```bash
   git add 'src/hello.py'
   git commit -m 'fix: incomplete hello message'
   git push
   ```

1. (선택사항) 웹 브라우저에서 `src/hello.py` 파일을 열어 변경사항이 업데이트되었는지 확인하세요.

1. 변경사항이 GitHub에 푸시되면, Mona가 작업을 확인하기 시작합니다. 피드백과 다음 학습 단계를 제공할 때까지 잠시 기다려 주세요.
