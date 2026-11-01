## 포트폴리오 설치, 빌드, 재배포 안내

### 1. 프로젝트 소개
이 프로젝트는 Hugo Theme Stack을 기반으로 제작한 개인 포트폴리오 웹사이트입니다. GitHub Pages와 GitHub Actions를 이용하여 자동으로 빌드하고 배포했습니다.

- GitHub 저장소: https://github.com/awefs-svg/protfolio_assignment
- 배포된 사이트: https://awefs-svg.github.io/protfolio_assignment/
- 사용 테마 : Hugo Theme Stack
- 테마 원본 : https://github.com/CaiJimmy/hugo-theme-stack

### 2.실행 환경 및 필요한 도구
- 운영체제 : Windows 11 기준
- Git : 2.54.0.windows.1
- Hugo : 0.167.0 Extended
- Go : 1.25.6 이상 권장
- Python : 배포 스크립트 실행 시 3.9 이상 필요

Git은 프로젝트를 다운로드하고 변경 사항을 관리하는 데 사용합니다.

Hugo는 Markdown 파일과 테마를 이용하여 웹사이트를 생성하는 도구이며, 이 프로젝트에서는 Hugo Extended 버전을 사용합니다.

Go는 Hugo 모듈의 의존성을 처리하는 데 사용됩니다.

Python은 GitHub Pages 배포 준비 및 빌드 스크립트 실행에 사용됩니다.

#### 도구 설치 주소
- Git: https://git-scm.com/downloads
- Hugo: https://gohugo.io/installation/
- Go: https://go.dev/dl/
- Python: https://www.python.org/downloads/

각 도구를 설치한 후 Windows PowerShell 또는 터미널에서 다음 명령어를 입력해 설치 여부를 확인합니다

git --version / hugo version / go version / python --version

명령어 실행 결과에 각 도구의 버전이 표시되면 설치된 것을 알 수 있습니다.

Hugo는 버전 정보에 extended가 표시되는지 확인해야합니다.

### 3.프로젝트 다운로드

#### 방법 1. Git 명령어로 다운로드
터미널을 열고 프로젝트를 저장할 폴더를 이동한 다음 명령어를 실행합니다.

=> git clone https://github.com/awefs-svg/protfolio_assignment.git

다운로드한 프로젝트 폴더로 이동합니다.

=> cd protfolio_assignment

(프로젝트의 실제 Hugo 사이트는 site 폴더에 있습니다.)

#### 방법2. GitHub에서 ZIP 파일 다운로드
1. GitHub 저장소에 접속합니다.
2. 초록색 Code 버튼을 클릭합니다.
3. Download ZIP을 선택합니다.
4. 다운로드한 ZIP 파일의 압축을 해제합니다.

### 4. 웹사이트 빌드
본 프로젝트는 GitHub Actions를 이용한 자동 빌드 방식을 사용합니다.

main 브랜치에 변경 사항이 반영되면 .github/workflows/hugo-pages.yml에 정의된 배포 작업이 실행됩니다.

GitHub Actions는 필요한 도구를 설치한 뒤 다음 명령어를 순서대로 실행합니다.

- 1단계. 의존성 준비
=> python .github/pages_build.py --dependencies

- 2단계. 웹사이트 빌드
=> python .github/pages_build.py --build

이 명령어는 GitHub Actions에서 자동으로 실행되므로 사용자가 직접 입력할 필요는 없습니다.

또한 빌드 과정에서 GitHub Pages에 맞는 사이트 경로를 처리하며, 최종 빌드 결과물을 저장소 최상위의 public 폴더에 생성하여 배포합니다.

위 명령어를 개인 컴퓨터에서 직접 실행하려면 Python뿐 아니라 Hugo, Go 등의 관련 도구와 환경 설정이 필요합니다. 따라서 이 프로젝트에서는 GitHub Actions를 이용한 빌드 방법을 권장합니다.

### 5. 기존 저장소에서 수정 및 재배포하기
이 방법은 원본 GitHub 저장소에 수정 권한이 있는 사용자를 위한 방법입니다.

- 방법 1. GitHub 웹사이트에서 수정하기
1. GitHub 저장소에 접속합니다.
2. 수정할 Markdown 또는 설정 파일을 선택합니다.
3. 연필 모양의 편집 버튼을 클릭합니다.
4. 내용을 수정한 뒤 Commit changes를 클릭합니다.
5. 변경 사항을 main 브랜치에 반영합니다.

이후 GitHub Actions가 자동으로 실행되어 웹사이트를 다시 빌드하고 배포합니다.

- 방법 2. Git 명령어로 수정 사항 반영하기
저장소를 복제한 상태에서 파일을 수정했다면, 저장소 최상위 폴더에서 다음 명령어를 실행합니다.

    - 1단계. 변경 사항 확인 => git status
    - 2단계. 변경 사항 추가 => git add .
    - 3단계. 커밋 생성 => git commit -m "Update portfolio content" 
    - 4단계. GitHub 저장소에 반영 => git push origin main

변경 사항이 main 브랜치에 반영되면 GitHub Actions를 통해 자동 배포가 시작됩니다.

단, 원본 저장소에 쓰기 권한이 없는 사용자는 git push origin main을 실행할 수 없습니다. 이 경우에는 아래의 새 저장소 배포 방법을 이용해야 합니다.

### 6. 다른 GitHub 계정에서 새로 배포하기

원본 저장소에 쓰기 권한이 없는 경우, 프로젝트를 자신의 GitHub 저장소로 복사하여 배포할 수 있습니다.

- 1단계. 저장소 복사
GitHub 저장소의 Fork 기능을 사용하거나, 프로젝트 ZIP 파일을 다운로드한 뒤 자신의 새 저장소에 업로드합니다.

- 2단계. GitHub Pages 설정
자신의 GitHub 저장소에서 다음 메뉴로 이동합니다.

=> Settings → Pages → Build and deployment

Source 항목에서 GitHub Actions를 선택합니다.

- 3단계. 사이트 주소 수정
site/config/_default/hugo.toml 파일에서 baseURL 값을 확인합니다.

현재 프로젝트의 설정은 다음과 같습니다.

=> baseURL = "https://awefs-svg.github.io/protfolio_assignment"

다른 계정의 저장소에 배포할 때에는 자신의 GitHub Pages 주소에 맞게 수정합니다.

예를 들어 GitHub 사용자 이름이 example-user, 저장소 이름이 my-portfolio라면 다음과 같이 설정합니다.

=> baseURL = "https://example-user.github.io/my-portfolio/"

이 주소는 예시이므로 실제 배포 환경에 맞게 변경해야 합니다.

- 4단계. 변경 사항 반영
수정한 설정을 자신의 저장소 main 브랜치에 커밋합니다.

- 5단계. GitHub Actions 실행 확인
GitHub 저장소의 Actions 탭에서 Deploy Hugo to GitHub Pages 작업이 실행되는지 확인합니다.

필요한 경우 해당 워크플로를 선택하고 Run workflow 버튼으로 수동 실행할 수도 있습니다.

- 6단계. 배포된 사이트 접속
배포 작업이 성공하면 자신의 GitHub Pages 주소에 접속하여 결과를 확인합니다.

새 저장소에서의 배포는 저장소 설정, 권한 및 주소에 따라 추가 조정이 필요할 수 있습니다.

### 7. 최종 웹사이트 확인
- 현재 배포된 포트폴리오는 다음 주소에서 확인할 수 있습니다.
=> https://awefs-svg.github.io/protfolio_assignment/

- 주요 페이지 주소는 다음과 같습니다.
=> Home: https://awefs-svg.github.io/protfolio_assignment/

=> Introduction: https://awefs-svg.github.io/protfolio_assignment/introduction/

=> Technical Skills: https://awefs-svg.github.io/protfolio_assignment/technical-skills/

=> Projects: https://awefs-svg.github.io/protfolio_assignment/page/projects/

웹사이트에 접속한 뒤 메뉴 이동, 콘텐츠 출력, 프로젝트 이미지 표시 및 화면 크기에 따른 레이아웃을 확인합니다.

### 8. 사용 테마 및 라이선스
본 프로젝트는 Hugo Theme Stack을 기반으로 제작했습니다.

- 테마명: Hugo Theme Stack
- 제작자: Jimmy
- 원본 저장소: https://github.com/CaiJimmy/hugo-theme-stack
- 라이선스: GNU General Public License v3.0

기존 테마의 저작권 및 라이선스 안내를 유지합니다.
