## 2단계: Codespace에서 커스텀 이미지 사용하기

방금 만든 Codespace에는 특별한 구성을 지정하지 않았기 때문에 GitHub가 기본 Docker 이미지를 사용했습니다. 이것은 매우 유용하지만, 일관성이 없고 런타임 환경을 버전 고정하지 않습니다. 개발 환경을 반복 가능하게 유지하려면 구성을 지정하는 것이 중요합니다.

특정 Docker 컨테이너 이미지를 제공하여 이를 설정해 봅시다.

### Codespace를 어떻게 구성하나요?

구성은 저장소의 `.devcontainer/devcontainer.json`을 통해 직접 제공됩니다. 여러 구성을 추가할 수도 있습니다!

이 파일을 만들고 가장 일반적인 설정 몇 가지를 설정해 봅시다. VS Code 설정, 포트 포워딩, 생명주기 스크립트 실행 등 다른 옵션은 GitHub의 [Codespaces 문서](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces)를 참조하세요.

### ⌨️ 활동: Codespace 커스터마이징하기

1. VS Code Codespace에 있는지 확인하세요.

1. VS Code 파일 탐색기를 사용하여 구성 파일을 만드세요.

   ```txt
   .devcontainer/devcontainer.json
   ```

   또는 아래 터미널 명령을 실행하여 만들 수 있습니다.

   ```bash
   mkdir -p .devcontainer
   touch .devcontainer/devcontainer.json
   ```

1. `.devcontainer/devcontainer.json` 파일을 열고 다음 내용을 추가하세요. 기본 이미지로 시작합시다.

   ```json
   {
     "name": "Basic Dev Environment",
     "image": "mcr.microsoft.com/devcontainers/base:debian"
   }
   ```

   > 💡 **팁**: 이름은 선택사항이지만, 여러 옵션이 있는 경우 GitHub에서 Codespace를 만들 때 구성을 식별하는 데 도움이 됩니다.

1. 저장 후, VS Code가 구성 변경을 감지했다는 알림을 표시할 수 있습니다. **Accept** 옵션을 선택하여 개발 컨테이너를 다시 빌드하거나, 수동으로 명령 팔레트(`CTRL`+`Shift`+`P`)를 사용하여 `Codespaces: Rebuild Container` 명령을 실행하세요. **Rebuild** 옵션을 선택하세요. 전체 빌드는 필요하지 않습니다.

   <img width="350" alt="Codespace 다시 빌드 명령" src="https://raw.githubusercontent.com/skills-kr/code-with-codespaces/main/.github/images/rebuild-codespace-command.png"/>

1. Codespace가 다시 빌드되고 VS Code가 다시 연결될 때까지 몇 분 기다리세요.

1. 하단 패널을 확장하고 **터미널** 탭을 선택하세요.

1. 다음 명령을 사용하여 도구 버전을 다시 확인하세요. 이제 아무것도 설치되어 있지 않은 것을 확인하세요!

   ```bash
   node --version
   dotnet --version
   python --version
   gh --version
   ```

1. ⚠️ 현재 Codespaces에 [Git-LFS](https://git-lfs.com/)가 설치되어 있어야 하는 버그가 있습니다. 다음 명령을 실행하여 영향받는 Git 훅을 제거하세요.

   ```bash
   rm .git/hooks/post-checkout
   rm .git/hooks/post-commit
   rm .git/hooks/post-merge
   rm .git/hooks/pre-push
   ```

1. 새 구성이 확인되었으니, 변경사항을 커밋합시다. VS Code의 소스 제어 도구를 사용하거나 아래 터미널 명령을 사용하세요.

   ```bash
   git add '.devcontainer/devcontainer.json'
   git commit -m 'feat: Add codespace configuration'
   git push
   ```

1. Dev Container 구성이 커밋되면, Mona가 작업을 확인하기 시작합니다. 피드백과 다음 학습 단계를 제공할 때까지 잠시 기다려 주세요.
