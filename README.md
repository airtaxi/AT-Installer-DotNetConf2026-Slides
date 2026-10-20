# .NET으로 만드는 MSIX 인스톨러 자동화

**대한민국 .NET Conf 2026** 발표자료입니다. 부제는 "샌드박스 배포를 더블클릭 한 번으로"입니다.

> `index.html`을 브라우저로 열면 바로 볼 수 있습니다. 시작 화면에서 **발표 시작**을 누르면 전체 화면으로 바뀌고, 방향키나 스페이스바로 슬라이드를 넘깁니다. 주소 뒤에 `#번호`를 붙이면 해당 쪽으로 바로 이동합니다.

## 발표 개요

MSIX로 배포하면 앱이 쓰는 파일과 레지스트리를 Windows가 따로 관리하고, 앱을 지울 때 함께 정리합니다. 하나의 `.msixbundle`에 x64, x86, ARM64를 모두 담을 수도 있습니다.

문제는 Microsoft Store 밖에서 배포할 때입니다. 사용자가 인증서를 직접 신뢰 목록에 등록해야 설치가 되고, 공인 코드 서명 인증서는 비용과 발급 조건 때문에 개인 개발자가 쓰기 어렵습니다.

이 발표는 그 과정을 .NET 코드로 자동화한 AT Installer 이야기입니다. 설치기가 권한 상승, 인증서 등록, 설치된 버전 비교, 패키지 배포를 처리하므로 사용자는 EXE 하나만 실행하면 됩니다. 같은 기능을 GUI 생성기와 명령줄 도구로 만들어 빌드 파이프라인에도 넣을 수 있게 했습니다.

## 다루는 내용

| 순서 | 구간 | 내용 |
|---|---|---|
| 1 | 왜 MSIX인가 | 자체 인스톨러의 한계, 파일과 레지스트리 가상화 |
| 2 | 사이드로딩의 벽 | 인증서 오류, 공인 인증서를 쓰기 어려운 이유 |
| 3 | 데모: Tauri 앱 설치 | NSIS와 MSIX의 설치와 제거 결과 비교 |
| 4 | 설치기 내부 구조 | 7z SFX, 권한 상승, 인증서 등록, `PackageManager`로 배포, silent 모드 종료 코드 |
| 5 | 생성기 내부 구조 | MSIX 인스톨러 생성기 화면, PE 헤더로 아키텍처 판별, 매니페스트 읽기, WinApp CLI 패키징, SFX 조립 |
| 6 | 데모: CLI 파이프라인 | `dotnet publish`로 빌드한 WPF 앱을 `aticmsixgen`으로 인스톨러까지 |
| 7 | .NET 플랫폼 활용 | GUI와 CLI의 코드 공유, NativeAOT 전환, RID별 dotnet tool, GitHub Actions 배포 |

데모 두 개는 실행 화면을 슬라이드에 넣어 두었습니다. 라이브 데모 없이도 발표 흐름을 따라갈 수 있습니다.

## 관련 프로젝트

- **AT Installer**: 설치기, 패키지 생성 도구, MSIX 인스톨러 생성기의 소스 코드입니다. [GitHub](https://github.com/airtaxi/AT-Installer) (MIT)
- **MSIX 인스톨러 생성기**: 인증서 생성, MSIX 패키징, EXE 인스톨러 조립을 하는 GUI 도구입니다. [Microsoft Store](https://apps.microsoft.com/detail/9P5GS17TCDQX)
- **aticmsixgen**: 같은 기능을 명령줄에서 쓰는 NativeAOT dotnet tool입니다. `dotnet tool install --global aticmsixgen` [NuGet](https://www.nuget.org/packages/aticmsixgen)

## 발표자

**이호원 (Howon Lee)**, GitHub [airtaxi](https://github.com/airtaxi)

Windows를 좋아해서 C#과 .NET을 시작했고, 지금은 WinUI와 Uno Platform으로 Windows 앱을 만듭니다. 오픈소스 Windows 앱을 15개 넘게 공개했습니다.

## 함께하기

**닷넷코리아 오픈채팅방**: [open.kakao.com/o/gaXg2I5g](https://open.kakao.com/o/gaXg2I5g)

.NET 관련 정보를 나누고 국내 개발자들과 이야기를 이어 갈 수 있는 곳입니다.

## 라이선스

MIT License. 슬라이드 화면에 나오는 다른 프로젝트의 로고와 자료(Tauri 등)는 각각의 라이선스를 따릅니다.
