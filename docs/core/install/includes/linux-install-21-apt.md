---
ms.openlocfilehash: 188fef66444cd60f59a3cb9619c0d86efd155f99
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93135931"
---

### <a name="install-the-sdk"></a>SDK 설치

.NET Core SDK를 사용하면 .NET Core로 앱을 개발할 수 있습니다. .NET Core SDK를 설치하면 해당 런타임을 설치할 필요가 없습니다. .NET Core SDK를 설치하려면 다음 명령을 실행합니다.

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-2.1
```

> [!IMPORTANT]
> **패키지 dotnet-sdk-2.1을 찾을 수 없습니다** 와 같은 오류 메시지가 표시되는 경우 [APT 문제 해결](#apt-troubleshooting) 섹션을 참조하세요.

### <a name="install-the-runtime"></a>런타임 설치

.NET Core 런타임을 사용하면 런타임을 포함하지 않았던 .NET Core로 만든 앱을 실행할 수 있습니다. 다음 명령을 실행하면 .NET Core에 대해 가장 호환성이 높은 ASP.NET Core 런타임이 설치됩니다. 터미널에서 다음 명령을 실행합니다.

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-2.1
```

> [!IMPORTANT]
> **패키지 aspnetcore-runtime-2.1을 찾을 수 없습니다** 와 같은 오류 메시지가 표시되는 경우 [APT 문제 해결](#apt-troubleshooting) 섹션을 참조하세요.

ASP.NET Core 런타임의 대안으로, ASP.NET Core 지원이 포함되지 않은 .NET Core 런타임을 설치할 수 있습니다. 이전 명령에서 `aspnetcore-runtime-2.1`을 `dotnet-runtime-2.1`로 바꿉니다.

```bash
sudo apt-get install -y dotnet-runtime-2.1
```
