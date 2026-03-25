## 3단계: 기능(Features) 추가하기

컨테이너 기능, VS Code 확장 프로그램, VS Code 설정, 호스트 요구사항 등을 추가하여 Codespace를 더 커스터마이징할 수 있습니다.

GitHub CLI를 추가하고, VS Code에서 Python 프로그램을 실행하기 위한 확장 프로그램을 추가하고, Codespace를 처음 만들 때 일부 패키지를 설치하는 커스텀 스크립트를 추가해 봅시다.

### ⌨️ 활동: Python 지원 추가하기

1. VS Code에서 명령 팔레트(`CTRL`+`SHIFT`+`P`)를 열고 아래 명령을 선택하세요.

   ```txt
   Codespaces: Add Dev Container Configuration Files...
   ```

   <img width="350" alt="VS Code Dev Container 구성 명령" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/configure-dev-container-command.png" />

1. `Modify your active configuration...` 옵션을 선택하세요.

1. 기능 목록에서 `devcontainers`의 `Python`을 검색하고 선택하세요.

   - 기본값 대신 `Configure Options`를 선택하세요.
   - `Install Tools`는 `true`로 두세요.
   - Python 버전 선택: `3.10`

1. `.devcontainer/devcontainer.json` 파일로 이동하여 여세요.

1. 아래와 유사한 새 항목이 추가되었는지 확인하세요.

   ```json
   "features": {
      "ghcr.io/devcontainers/features/python:1": {
         "installTools": true,
         "version": "3.10"
      }
   },
   ```

### ⌨️ 활동: VS Code 확장 프로그램 추가하기

1. 왼쪽 탐색에서 **확장 프로그램** 탭을 선택하세요.

   <img width="200" alt="VS Code 확장 프로그램 탭" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/vs-code-extensions-tab.png" />

1. `python`을 검색하고 `Python`과 `Python Debugger` 항목을 찾으세요.

   <img width="250" alt="VS Code용 Python 확장 프로그램" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/python-extensions.png" />

1. 각 항목을 마우스 오른쪽 클릭하고 `Add to devcontainer.json` 옵션을 선택하세요.

   <img width="250" alt="devcontainer 구성에 추가 버튼" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/add-to-devcontainer-button.png" />

1. `.devcontainer/devcontainer.json` 파일로 이동하여 여세요.

1. 아래와 유사한 새 항목이 추가되었는지 확인하세요.

   ```json
   "customizations": {
      "vscode": {
         "extensions": [
            "ms-python.python",
            "ms-python.debugpy"
         ]
      }
   },
   ```

### ⌨️ 활동: 커스텀 스크립트 추가하기

Dev Container 사양은 Codespace를 더 커스터마이징하기 위해 [생명주기 스크립트](https://containers.dev/implementors/json_reference/#lifecycle-scripts)를 실행할 수 있는 여러 위치를 제공합니다. 초기 빌드(또는 다시 빌드) 후 한 번 실행되는 `postCreateCommand`를 추가해 봅시다.

1. VS Code 파일 탐색기를 사용하여 아래 이름의 스크립트 파일을 만드세요.

   ```txt
   .devcontainer/postCreate.sh
   ```

   또는 아래 터미널 명령을 실행하여 만들 수 있습니다.

   ```bash
   touch .devcontainer/postCreate.sh
   ```

1. 아래 터미널 명령을 실행하여 스크립트를 실행 가능하게 만드세요.

   ```bash
   chmod +x .devcontainer/postCreate.sh
   ```

1. `.devcontainer/postCreate.sh` 파일을 열고 다음 코드를 추가하세요. 증기 기관차 애니메이션을 설치합니다.

   ```bash
   #!/bin/bash

   sudo apt-get update
   sudo apt-get install sl
   echo "export PATH=\$PATH:/usr/games" >> ~/.bashrc
   echo "export PATH=\$PATH:/usr/games" >> ~/.zshrc
   ```

1. `.devcontainer/devcontainer.json` 파일로 이동하여 여세요.

1. `features`, `customizations`와 같은 수준(_최상위 수준_)에 `postCreateCommand` 항목을 만드세요.

   ```json
   "postCreateCommand": ".devcontainer/postCreate.sh"
   ```

1. 새 구성이 완료되었으니, 변경사항을 커밋합시다. VS Code의 소스 제어 도구를 사용하거나 아래 터미널 명령을 사용하세요.

   ```shell
   git add '.devcontainer/devcontainer.json'
   git add '.devcontainer/postCreate.sh'
   git commit -m 'feat: Add features, extensions, and postCreate script'
   git push
   ```

1. VS Code 명령 팔레트(`CTRL`+`Shift`+`P`)를 열고 `Codespaces: Rebuild Container` 명령을 실행하세요. **Rebuild** 옵션을 선택하세요. 전체 빌드는 필요하지 않습니다.

   <img width="350" alt="Codespace 다시 빌드 명령" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/rebuild-codespace-command.png"/>

1. Codespace가 다시 빌드되고 VS Code가 다시 연결될 때까지 몇 분 기다리세요.

1. 커스터마이징이 커밋되면, Mona가 작업을 확인하기 시작합니다. 피드백과 다음 학습 단계를 제공할 때까지 잠시 기다려 주세요.

> [!TIP]
> 계정에 [dotfiles 설치](https://docs.github.com/en/codespaces/setting-your-user-preferences/personalizing-github-codespaces-for-your-account)를 구성하여 개인 구성과 프로젝트 구성을 결합할 수도 있습니다.

### ⌨️ 활동: (선택사항) 커스터마이징 확인하기

Codespace를 다시 빌드했으니, Python 확장 프로그램, Python 버전, 커스텀 스크립트가 Codespace에서 올바르게 조정되었는지 확인해 봅시다.

1. Codespace에 있는지 확인하세요.

1. 왼쪽 사이드바에서 확장 프로그램 탭을 클릭하고 Python 확장 프로그램이 설치 및 활성화되었는지 확인하세요.

   <img width="250" alt="VS Code용 Python 확장 프로그램" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/python-extensions.png" />

1. 왼쪽 사이드바에서 **실행 및 디버그** 탭을 선택한 다음 **디버깅 시작** 아이콘을 누르세요. VS Code가 하단 패널을 열고 실행 로그를 표시합니다.

   <img width="250" alt="실행 및 디버그 탭의 시작 버튼" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/run-and-debug-start-button.png"/>

1. 하단 패널에서 **터미널** 탭으로 전환하세요.

1. 다음 명령을 실행하여 설치된 Python 버전을 확인하세요. 다른 도구들은 설치되어 있지 않은 것을 확인하세요.

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

1. 다음 명령을 실행하여 증기 기관차 애니메이션을 확인하세요.

   ```bash
   sl
   ```
