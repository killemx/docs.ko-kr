---
title: dotnet new 명령
description: dotnet new 명령은 지정된 템플릿을 기반으로 새 .NET Core 프로젝트를 만듭니다.
no-loc:
- Blazor
- WebAssembly
ms.date: 09/01/2020
ms.openlocfilehash: 4a4c8e2806fee663b5f6aa255a6f24250a072a85
ms.sourcegitcommit: 532b03d5bbab764d63356193b04cd2281bc01239
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2020
ms.locfileid: "92526613"
---
# <a name="dotnet-new"></a>dotnet new

**이 문서의 적용 대상:**  ✔️ .NET Core 2.0 SDK 이상 버전

## <a name="name"></a>이름

`dotnet new` - 지정된 템플릿을 기반으로 새 프로젝트, 구성 파일 또는 솔루션을 만듭니다.

## <a name="synopsis"></a>개요

```dotnetcli
dotnet new <TEMPLATE> [--dry-run] [--force] [-i|--install {PATH|NUGET_ID}]
    [-lang|--language {"C#"|"F#"|VB}] [-n|--name <OUTPUT_NAME>]
    [--nuget-source <SOURCE>] [-o|--output <OUTPUT_DIRECTORY>]
    [-u|--uninstall] [--update-apply] [--update-check] [Template options]

dotnet new <TEMPLATE> [-l|--list] [--type <TYPE>]

dotnet new -h|--help
```

## <a name="description"></a>설명

`dotnet new` 명령은 템플릿을 기반으로 .NET Core 프로젝트 또는 다른 아티팩트를 만듭니다.

이 명령은 [템플릿 엔진](https://github.com/dotnet/templating)을 호출하여 지정된 템플릿 및 옵션을 기반으로 디스크에 아티팩트를 만듭니다.

### <a name="implicit-restore"></a>암시적 복원

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

## <a name="arguments"></a>인수

- **`TEMPLATE`**

  명령이 호출될 때 인스턴스화할 템플릿입니다. 각 템플릿에는 전달할 수 있는 특정 옵션이 있을 수 있습니다. 자세한 내용은 [템플릿 옵션](#template-options)을 참조하세요.

  `dotnet new --list` 또는 `dotnet new -l`을 실행하여 설치된 모든 템플릿의 목록을 볼 수 있습니다. `TEMPLATE` 값이 반환된 테이블의 **템플릿** 또는 **약식 이름** 열의 텍스트와 정확히 일치하지 않는 경우 해당 두 열에 대해 부분 문자열 일치가 수행됩니다.

  .NET Core 3.0 SDK부터 CLI는 다음 조건에서 `dotnet new` 명령을 호출할 때 NuGet.org에서 템플릿을 검색합니다.

  - `dotnet new`를 호출할 때 CLI가 템플릿 일치 또는 부분 일치조차 찾을 수 없는 경우.
  - 최신 버전의 템플릿을 사용할 수 있는 경우. 이 경우 프로젝트 또는 아티팩트가 만들어지지만 CLI는 업데이트된 템플릿 버전에 대해 경고합니다.

  다음 표에는 .NET Core SDK와 함께 사전 설치된 템플릿이 나와 있습니다. 템플릿의 기본 언어는 대괄호 안에 표시됩니다. 특정 템플릿 옵션을 보려면 약식 이름 링크를 클릭합니다.

| 템플릿                                    | 짧은 이름                      | 언어     | Tags                                  | 도입 |
|----------------------------------------------|---------------------------------|--------------|---------------------------------------|------------|
| Console Application                          | [console](#console)             | [C#], F#, VB | 일반/콘솔                        | 1.0        |
| Class library                                | [classlib](#classlib)           | [C#], F#, VB | 일반/라이브러리                        | 1.0        |
| WPF Application                              | [wpf](#wpf)                     | [C#], VB     | 일반/WPF                            | 3.0(VB의 경우 5.0)|
| WPF Class library                            | [wpflib](#wpf)                  | [C#], VB     | 일반/WPF                            | 3.0(VB의 경우 5.0)|
| WPF Custom Control Library                   | [wpfcustomcontrollib](#wpf)     | [C#], VB     | 일반/WPF                            | 3.0(VB의 경우 5.0)|
| WPF User Control Library                     | [wpfusercontrollib](#wpf)       | [C#], VB     | 일반/WPF                            | 3.0(VB의 경우 5.0)|
| Windows Forms(WinForms) Application          | [winforms](#winforms)           | [C#], VB     | 일반/WinForms                       | 3.0(VB의 경우 5.0)|
| Windows Forms(WinForms) Class Library        | [winformslib](#winforms)        | [C#], VB     | 일반/WinForms                       | 3.0(VB의 경우 5.0)|
| Worker Service                               | [worker](#web-others)           | [C#]         | 일반/Worker/웹                     | 3.0        |
| Unit Test Project                            | [mstest](#test)                 | [C#], F#, VB | Test/MSTest                           | 1.0        |
| NUnit 3 Test Project                         | [nunit](#nunit)                 | [C#], F#, VB | Test/NUnit                            | 2.1.400    |
| NUnit 3 Test Item                            | `nunit-test`                    | [C#], F#, VB | Test/NUnit                            | 2.2        |
| xUnit Test Project                           | [xunit](#test)                  | [C#], F#, VB | Test/xUnit                            | 1.0        |
| Razor Components                             | `razorcomponent`                | [C#]         | Web/ASP.NET                           | 3.0        |
| Razor Page                                   | [page](#page)                   | [C#]         | Web/ASP.NET                           | 2.0        |
| MVC ViewImports                              | [viewimports](#namespace)       | [C#]         | Web/ASP.NET                           | 2.0        |
| MVC ViewStart                                | `viewstart`                     | [C#]         | Web/ASP.NET                           | 2.0        |
| Blazor Server App                            | [blazorserver](#blazorserver)   | [C#]         | Web/Blazor                            | 3.0        |
| Blazor WebAssembly App                       | `blazorwasm`                    | [C#]         | Web/Blazor/WebAssembly                | 3.1.300    |
| ASP.NET Core Empty                           | [web](#web)                     | [C#], F#     | Web/Empty                             | 1.0        |
| ASP.NET Core Web App (Model-View-Controller) | [mvc](#web-options)             | [C#], F#     | Web/MVC                               | 1.0        |
| ASP.NET Core Web APp                         | [webapp, razor](#web-options)   | [C#]         | Web/MVC/Razor Pages                   | 2.2, 2.0   |
| ASP.NET Core with Angular                    | [angular](#spa)                 | [C#]         | Web/MVC/SPA                           | 2.0        |
| ASP.NET Core with React.js                   | [react](#spa)                   | [C#]         | Web/MVC/SPA                           | 2.0        |
| ASP.NET Core with React.js 및 Redux           | [reactredux](#reactredux)       | [C#]         | Web/MVC/SPA                           | 2.0        |
| Razor Class Library                          | [razorclasslib](#razorclasslib) | [C#]         | Web/Razor/Library/Razor 클래스 라이브러리 | 2.1        |
| ASP.NET Core Web API                         | [webapi](#webapi)               | [C#], F#     | Web/WebAPI                            | 1.0        |
| ASP.NET Core gRPC Service                    | [grpc](#web-others)             | [C#]         | Web/gRPC                              | 3.0        |
| dotnet gitignore file                        | `gitignore`                     |              | Config                                | 3.0        |
| global.json file                             | [globaljson](#globaljson)       |              | Config                                | 2.0        |
| NuGet Config                                 | `nugetconfig`                   |              | Config                                | 1.0        |
| Dotnet local tool manifest file              | `tool-manifest`                 |              | Config                                | 3.0        |
| Web Config                                   | `webconfig`                     |              | Config                                | 1.0        |
| Solution File                                | `sln`                           |              | 솔루션                                  | 1.0        |
| Protocol Buffer File                         | [proto](#namespace)             |              | Web/gRPC                              | 3.0        |

## <a name="options"></a>옵션

- **`--dry-run`**

  지정된 명령이 실행되어 템플릿 만들기로 이어질 경우 발생하는 작업에 대한 요약을 표시합니다. .NET Core 2.2 SDK부터 사용할 수 있습니다.

- **`--force`**

  기존 파일을 변경할 경우에도 콘텐츠를 강제 생성합니다. 선택한 템플릿이 출력 디렉터리의 기존 파일을 재정의하는 경우에 필요합니다.

- **`-h|--help`**

  명령에 대한 도움말을 출력합니다. `dotnet new` 명령 자체 또는 템플릿에 대해 호출될 수 있습니다. 예: `dotnet new mvc --help`.

- **`-i|--install <PATH|NUGET_ID>`**

  제공된 `PATH` 또는 `NUGET_ID`에서 템플릿 패키지를 설치합니다. 시험판 버전의 템플릿 패키지를 설치하려면 버전을 `<package-name>::<package-version>` 형식으로 지정해야 합니다. 기본적으로 `dotnet new`는 안정적인 최신 패키지 버전을 나타내는 버전에 대해 \*를 전달합니다. [예제](#examples) 섹션의 예제를 참조하세요.
  
  이 명령을 실행할 때 템플릿의 버전이 이미 설치되어 있는 경우 템플릿이 지정된 버전으로 업데이트되거나 버전이 지정되지 않은 경우 안정적인 최신 버전으로 업데이트됩니다.

  사용자 지정 템플릿을 만드는 방법에 대한 자세한 내용은 [dotnet new에 대한 사용자 지정 템플릿](custom-templates.md)을 참조하세요.

- **`-l|--list`**

  지정된 이름을 포함하는 템플릿을 나열합니다. 이름을 지정하지 않으면 모든 템플릿이 나열됩니다.

- **`-lang|--language {C#|F#|VB}`**

  만들 템플릿의 언어입니다. 허용되는 언어는 템플릿에 따라 다릅니다([인수](#arguments) 섹션에서 기본값 참조). 일부 템플릿의 경우 유효하지 않습니다.

  > [!NOTE]
  > 일부 셸은 `#`을 특수 문자로 해석합니다. 이러한 경우 언어 매개 변수 값을 따옴표로 묶습니다. 예: `dotnet new console -lang "F#"`.

- **`-n|--name <OUTPUT_NAME>`**

  생성된 출력에 대한 이름입니다. 이름을 지정하지 않으면 현재 디렉터리의 이름이 사용됩니다.

- **`--nuget-source <SOURCE>`**

  설치 중 사용할 NuGet 소스를 지정합니다. .NET Core 2.1 SDK부터 사용할 수 있습니다.

- **`-o|--output <OUTPUT_DIRECTORY>`**

  생성된 출력을 배치할 위치입니다. 기본값은 현재 디렉터리입니다.

- **`--type <TYPE>`**

  사용 가능한 형식에 따라 템플릿을 필터링합니다. 미리 정의된 값은 `project` 및 `item`입니다.

- **`-u|--uninstall [PATH|NUGET_ID]`**

  제공된 `PATH` 또는 `NUGET_ID`에서 템플릿 패키지를 제거합니다. `<PATH|NUGET_ID>` 값을 지정하지 않으면 현재 설치된 모든 템플릿 팩과 연결된 템플릿이 표시됩니다. `NUGET_ID`를 지정하는 경우 버전 번호를 포함하지 않습니다.

  이 옵션에 대한 매개 변수를 지정하지 않으면 명령은 설치된 템플릿 및 해당 세부 정보를 나열합니다.

  > [!NOTE]
  > `PATH`를 사용하여 템플릿을 제거하려면 경로를 정규화해야 합니다. 예를 들어 *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* 는 작동하지만 상위 폴더의 *./GarciaSoftware.ConsoleTemplate.CSharp* 는 작동하지 않습니다.
  > 템플릿 경로에 마지막 디렉터리 슬래시를 포함하지 마세요.

- **`--update-apply`**

  현재 설치된 템플릿 패키지에 사용할 수 있는 업데이트가 있는지 확인하고 설치합니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.

- **`--update-check`**

  현재 설치된 템플릿 패키지에 사용할 수 있는 업데이트가 있는지 확인합니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.

## <a name="template-options"></a>템플릿 옵션

각 프로젝트 템플릿에는 사용할 수 있는 추가 옵션이 있을 수 있습니다. 코어 템플릿에는 다음과 같은 추가 옵션이 있습니다.

### <a name="console"></a>console

- **`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |

- **`--langVersion <VERSION_NUMBER>`**

  생성된 프로젝트 파일에서 `LangVersion` 속성을 설정합니다. 예를 들어 C# 7.3을 사용하려면 `--langVersion 7.3`을 사용합니다. F#에서 지원되지 않습니다. .NET Core 2.2 SDK부터 사용할 수 있습니다.

  기본 C# 버전 목록은 [기본값](../../csharp/language-reference/configure-language-version.md#defaults)을 참조하세요.

- **`--no-restore`**

  지정할 경우 프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다. .NET Core 2.2 SDK부터 사용할 수 있습니다.

**_

### <a name="classlib"></a>classlib

- _ *`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 값: `netcoreapp<version>`(.NET Core 클래스 라이브러리를 만드는 경우) 또는 `netstandard<version>`(.NET Standard 클래스 라이브러리를 만드는 경우). 기본값은 `netstandard2.0`입니다.

- **`--langVersion <VERSION_NUMBER>`**

  생성된 프로젝트 파일에서 `LangVersion` 속성을 설정합니다. 예를 들어 C# 7.3을 사용하려면 `--langVersion 7.3`을 사용합니다. F#에서 지원되지 않습니다. .NET Core 2.2 SDK부터 사용할 수 있습니다.

  기본 C# 버전 목록은 [기본값](../../csharp/language-reference/configure-language-version.md#defaults)을 참조하세요.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="wpf-wpflib-wpfcustomcontrollib-wpfusercontrollib"></a><a name="wpf"></a> wpf, wpflib, wpfcustomcontrollib, wpfusercontrollib

- _ *`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 기본값은 `netcoreapp3.1`입니다. .NET Core 3.1 SDK부터 사용할 수 있습니다.

- **`--langVersion <VERSION_NUMBER>`**

  생성된 프로젝트 파일에서 `LangVersion` 속성을 설정합니다. 예를 들어 C# 7.3을 사용하려면 `--langVersion 7.3`을 사용합니다.

  기본 C# 버전 목록은 [기본값](../../csharp/language-reference/configure-language-version.md#defaults)을 참조하세요.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="winforms-winformslib"></a><a name="winforms"></a> winforms, winformslib

- _ *`--langVersion <VERSION_NUMBER>`**

  생성된 프로젝트 파일에서 `LangVersion` 속성을 설정합니다. 예를 들어 C# 7.3을 사용하려면 `--langVersion 7.3`을 사용합니다.

  기본 C# 버전 목록은 [기본값](../../csharp/language-reference/configure-language-version.md#defaults)을 참조하세요.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="worker-grpc"></a><a name="web-others"></a> worker, grpc

- _ *`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. 기본값은 `netcoreapp3.1`입니다. .NET Core 3.1 SDK부터 사용할 수 있습니다.

- **`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="mstest-xunit"></a><a name="test"></a> mstest, xunit

- _ *`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 3.0 SDK 이후 사용할 수 있는 옵션입니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |

- **`-p|--enable-pack`**

  [dotnet pack](dotnet-pack.md)을 사용하여 프로젝트에 대한 패키징을 사용하도록 설정합니다.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="nunit"></a>nunit

- _ *`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.2         | `netcoreapp2.2` |
  | 2.1         | `netcoreapp2.1` |

- **`-p|--enable-pack`**

  [dotnet pack](dotnet-pack.md)을 사용하여 프로젝트에 대한 패키징을 사용하도록 설정합니다.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="page"></a>page

- _ *`-na|--namespace <NAMESPACE_NAME>`**

  생성된 코드에 대한 네임스페이스입니다. 기본값은 `MyApp.Namespace`입니다.

- **`-np|--no-pagemodel`**

  PageModel 없이 페이지를 만듭니다.

**_

### <a name="viewimports-proto"></a><a name="namespace"></a> viewimports, proto

- _ *`-na|--namespace <NAMESPACE_NAME>`**

  생성된 코드에 대한 네임스페이스입니다. 기본값은 `MyApp.Namespace`입니다.

**_

### <a name="blazorserver"></a>blazorserver

- _ *`-au|--auth <AUTHENTICATION_TYPE>`**

  사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

  - `None` - 인증하지 않습니다(기본값).
  - `Individual` - 개별 인증입니다.
  - `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
  - `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
  - `MultiOrg` - 여러 테넌트에 대한 조직적 인증입니다.
  - `Windows` - Windows 인증입니다.

- **`--aad-b2c-instance <INSTANCE>`**

  연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

- **`-ssp|--susi-policy-id <ID>`**

  이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`-rp|--reset-password-policy-id <ID>`**

  이 프로젝트에 대한 암호 재설정 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`-ep|--edit-profile-policy-id <ID>`**

  이 프로젝트에 대한 프로필 편집 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`--aad-instance <INSTANCE>`**

  연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

- **`--client-id <ID>`**

  이 프로젝트의 클라이언트 ID입니다. `IndividualB2C`, `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

- **`--domain <DOMAIN>`**

  디렉터리 테넌트의 도메인입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

- **`--tenant-id <ID>`**

  연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

- **`--callback-path <PATH>`**

  리디렉션 URI의 애플리케이션 기본 경로 내 요청 경로입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `/signin-oidc`입니다.

- **`-r|--org-read-access`**

  디렉터리에 대한 이 애플리케이션 읽기 액세스를 허용합니다. `SingleOrg` 또는 `MultiOrg` 인증에만 적용됩니다.

- **`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`--no-https`**

  HTTPS를 해제합니다. 이 옵션은 `--auth`에 `Individual`, `IndividualB2C`, `SingleOrg` 또는 `MultiOrg`를 사용하지 않는 경우에만 적용됩니다.

- **`-uld|--use-local-db`**

  SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="web"></a>web

- _ *`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 2.2 SDK에서 사용할 수 없는 옵션입니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.1` |

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

- **`--no-https`**

  HTTPS를 해제합니다.

**_

### <a name="mvc-webapp"></a><a name="web-options"></a> mvc, webapp

- _ *`-au|--auth <AUTHENTICATION_TYPE>`**

  사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

  - `None` - 인증하지 않습니다(기본값).
  - `Individual` - 개별 인증입니다.
  - `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
  - `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
  - `MultiOrg` - 여러 테넌트에 대한 조직적 인증입니다.
  - `Windows` - Windows 인증입니다.

- **`--aad-b2c-instance <INSTANCE>`**

  연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

- **`-ssp|--susi-policy-id <ID>`**

  이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`-rp|--reset-password-policy-id <ID>`**

  이 프로젝트에 대한 암호 재설정 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`-ep|--edit-profile-policy-id <ID>`**

  이 프로젝트에 대한 프로필 편집 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`--aad-instance <INSTANCE>`**

  연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

- **`--client-id <ID>`**

  이 프로젝트의 클라이언트 ID입니다. `IndividualB2C`, `SingleOrg` 또는 `MultiOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

- **`--domain <DOMAIN>`**

  디렉터리 테넌트의 도메인입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

- **`--tenant-id <ID>`**

  연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

- **`--callback-path <PATH>`**

  리디렉션 URI의 애플리케이션 기본 경로 내 요청 경로입니다. `SingleOrg` 또는 `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `/signin-oidc`입니다.

- **`-r|--org-read-access`**

  디렉터리에 대한 이 애플리케이션 읽기 액세스를 허용합니다. `SingleOrg` 또는 `MultiOrg` 인증에만 적용됩니다.

- **`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`--no-https`**

  HTTPS를 해제합니다. 이 옵션은 `Individual`, `IndividualB2C`, `SingleOrg` 또는 `MultiOrg`를 사용하지 않는 경우에만 적용됩니다.

- **`-uld|--use-local-db`**

  SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다.

- **`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 3.0 SDK 이후 사용할 수 있는 옵션입니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

- **`--use-browserlink`**

  프로젝트에 BrowserLink를 포함합니다. .NET Core 2.2 및 3.1 SDK에서 사용할 수 없는 옵션입니다.

- **`-rrc|--razor-runtime-compilation`**

  프로젝트가 디버그 빌드에서 [Razor 런타임 컴파일](/aspnet/core/mvc/views/view-compilation#runtime-compilation)을 사용하도록 구성되어 있는지 확인합니다. .NET Core 3.1.201 SDK 이후 사용할 수 있는 옵션입니다.

**_

### <a name="angular-react"></a><a name="spa"></a> angular, react

- _ *`-au|--auth <AUTHENTICATION_TYPE>`**

  사용할 인증 형식입니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.
  
  가능한 값은 다음과 같습니다.

  - `None` - 인증하지 않습니다(기본값).
  - `Individual` - 개별 인증입니다.

- **`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

- **`--no-https`**

  HTTPS를 해제합니다. 이 옵션은 인증이 `None`인 경우에만 적용됩니다.

- **`-uld|--use-local-db`**

  SQLite 대신 LocalDB를 사용하도록 지정합니다. `Individual` 또는 `IndividualB2C` 인증에만 적용됩니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.

- **`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 2.2 SDK에서 사용할 수 없는 옵션입니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.0` |

**_

### <a name="reactredux"></a>reactredux

- _ *`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 2.2 SDK에서 사용할 수 없는 옵션입니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.0` |

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

- **`--no-https`**

  HTTPS를 해제합니다.

**_

### <a name="razorclasslib"></a>razorclasslib

- _ *`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

- **`-s|--support-pages-and-views`**

  이 라이브러리에 구성 요소 외에 기존의 Razor 페이지와 뷰를 추가하는 것을 지원합니다. .NET Core 3.0 SDK 이후 사용할 수 있습니다.

**_
  
### <a name="webapi"></a>webapi

- _ *`-au|--auth <AUTHENTICATION_TYPE>`**

  사용할 인증 형식입니다. 가능한 값은 다음과 같습니다.

  - `None` - 인증하지 않습니다(기본값).
  - `IndividualB2C` - Azure AD B2C를 사용한 개별 인증입니다.
  - `SingleOrg` - 단일 테넌트에 대한 조직적 인증입니다.
  - `Windows` - Windows 인증입니다.

- **`--aad-b2c-instance <INSTANCE>`**

  연결할 Azure Active Directory B2C 인스턴스입니다. `IndividualB2C` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/tfp/`입니다.

- **`-ssp|--susi-policy-id <ID>`**

  이 프로젝트에 대한 로그인 및 등록 정책 ID입니다. `IndividualB2C` 인증과 함께 사용합니다.

- **`--aad-instance <INSTANCE>`**

  연결할 Azure Active Directory 인스턴스입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `https://login.microsoftonline.com/`입니다.

- **`--client-id <ID>`**

  이 프로젝트의 클라이언트 ID입니다. `IndividualB2C` 또는 `SingleOrg` 인증과 함께 사용합니다. 기본값은 `11111111-1111-1111-11111111111111111`입니다.

- **`--domain <DOMAIN>`**

  디렉터리 테넌트의 도메인입니다. `IndividualB2C` 또는 `SingleOrg` 인증과 함께 사용합니다. 기본값은 `qualified.domain.name`입니다.

- **`--tenant-id <ID>`**

  연결할 디렉터리의 TenantId ID입니다. `SingleOrg` 인증과 함께 사용합니다. 기본값은 `22222222-2222-2222-2222-222222222222`입니다.

- **`-r|--org-read-access`**

  디렉터리에 대한 이 애플리케이션 읽기 액세스를 허용합니다. `SingleOrg` 인증에만 적용됩니다.

- **`--exclude-launch-settings`**

  생성된 템플릿에서 *launchSettings.json* 을 제외합니다.

- **`--no-https`**

  HTTPS를 해제합니다. `app.UseHsts` 및 `app.UseHttpsRedirection`은 `Startup.Configure`에 추가되지 않습니다. 이 옵션은 인증에 `IndividualB2C` 또는 `SingleOrg`를 사용하지 않는 경우에만 적용됩니다.

- **`-uld|--use-local-db`**

  SQLite 대신 LocalDB를 사용하도록 지정합니다. `IndividualB2C` 인증에만 적용됩니다.

- **`-f|--framework <FRAMEWORK>`**

  대상으로 할 [프레임워크](../../standard/frameworks.md)를 지정합니다. .NET Core 2.2 SDK에서 사용할 수 없는 옵션입니다.

  다음 표에서는 사용하는 SDK 버전 번호에 따른 기본값을 나열합니다.

  | SDK 버전 | 기본값   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.1` |

- **`--no-restore`**

  프로젝트를 만드는 동안 암시적 복원을 실행하지 않습니다.

**_

### <a name="globaljson"></a>globaljson

- _ *`--sdk-version <VERSION_NUMBER>`**

  *global.json* 파일에서 사용할 .NET Core SDK 버전을 지정합니다.

***

## <a name="examples"></a>예

- 템플릿 이름을 지정하여 C# 콘솔 애플리케이션 프로젝트를 만듭니다.

  ```dotnetcli
  dotnet new "Console Application"
  ```

- 현재 디렉터리에 F# 콘솔 애플리케이션 프로젝트를 만듭니다.

  ```dotnetcli
  dotnet new console -lang "F#"
  ```

- 지정된 디렉터리에 .NET Standard 클래스 라이브러리 프로젝트를 만듭니다.

  ```dotnetcli
  dotnet new classlib -lang VB -o MyLibrary
  ```

- 인증 없이 현재 디렉터리에 새 ASP.NET Core C# MVC 프로젝트를 만듭니다.

  ```dotnetcli
  dotnet new mvc -au None
  ```

- 새 xUnit 프로젝트를 만듭니다.

  ```dotnetcli
  dotnet new xunit
  ```

- SPA(단일 페이지 애플리케이션) 템플릿에 사용할 수 있는 모든 템플릿을 나열합니다.

  ```dotnetcli
  dotnet new spa -l
  ```

- *we* 부분 문자열과 일치하는 모든 템플릿을 나열합니다. 정확히 일치하는 항목을 찾을 수 없으므로 부분 문자열 일치는 약식 이름과 열 모두에 대해 실행됩니다.

  ```dotnetcli
  dotnet new we -l
  ```

- *ng* 와 일치하는 템플릿을 호출해 보세요. 단일 일치 항목을 확인할 수 없는 경우 부분적으로 일치하는 템플릿을 나열합니다.

  ```dotnetcli
  dotnet new ng
  ```

- ASP.NET Core용 SPA 템플릿의 버전 2.0을 설치합니다.

  ```dotnetcli
  dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
  ```

- 설치된 템플릿 및 해당 세부 정보(제거 방법 포함)를 나열합니다.

  ```dotnetcli
  dotnet new -u
  ```

- SDK 버전을 3.1.101로 설정하여 현재 디렉터리에 *global.json* 을 만듭니다.

  ```dotnetcli
  dotnet new globaljson --sdk-version 3.1.101
  ```

## <a name="see-also"></a>참조

- [dotnet new에 대한 사용자 지정 템플릿](custom-templates.md)
- [dotnet용 사용자 지정 템플릿 새로 만들기](../tutorials/cli-templates-create-item-template.md)
- [dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)(dotnet/dotnet-template-samples GitHub 리포지토리)
- [Available templates for dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)(dotnet new에 대한 사용 가능한 템플릿)
