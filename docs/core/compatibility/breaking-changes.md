---
title: 호환성이 손상되는 변경
description: 각 .NET Core 버전의 호환성이 손상되는 변경에 대해 알아봅니다.
ms.date: 11/27/2019
ms.openlocfilehash: eea6542acb9fa659af764bfd3a2af00fd9740191
ms.sourcegitcommit: 1e8382d0ce8b5515864f8fbb178b9fd692a7503f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89656277"
---
# <a name="breaking-change-selectors"></a>호환성이 손상되는 변경 선택기

다음 버전 및 영역 선택기는 다양한 버전의 .NET Core, ASP.NET Core 및 EF Core에 적용 가능하며 호환성이 손상되는 변경 사항을 필터링한 목록을 제공합니다. 목차에서 버전별 또는 기술 영역별로 문서를 찾아볼 수 있습니다.

## <a name="by-version"></a>버전별

현재 대상으로 하는 .NET 버전을 선택한 후 마이그레이션할 .NET Core 버전을 선택합니다.

> [!div class="op_multi_selector" title1="대상 버전" title2="마이그레이션된 버전"]
>
> - [(3.1 | 5.0)](3.1-5.0.md)
> - [(3.0 | 3.1)](3.0-3.1.md)
> - [(2.2 | 3.1)](2.2-3.1.md)
> - [(2.2 | 3.0)](2.2-3.0.md)
> - [(2.0 | 2.1)](2.0-2.1.md)
> - [(.NET Framework | .NET Core)](fx-core.md)

## <a name="by-technology-area"></a>기술 영역별

관심 있는 .NET Core 기술 영역을 선택합니다. 개별 변경 내용은 .NET Core 버전별로 정렬되어 있습니다.

> [!div class="op_single_selector"]
>
> - [ASP.NET Core](aspnetcore.md)
> - [코드 분석](code-analysis.md)
> - [핵심 .NET 라이브러리](corefx.md)
> - [암호화](cryptography.md)
> - [EF Core](/ef/core/what-is-new/ef-core-3.0/breaking-changes)
> - [전역화](globalization.md)
> - [Interop](interop.md)
> - [네트워킹](networking.md)
> - [serialization](serialization.md)
> - [Visual Basic](visualbasic.md)
> - [Windows Forms](winforms.md)
> - [WPF](wpf.md)

## <a name="github-issues-and-announcements"></a>GitHub 문제 및 알림

.NET Core에 도입된 호환성이 손상되는 변경을 자세히 설명하는 개별 문제를 다음 GitHub 리포지토리에서 확인할 수도 있습니다.

- .NET Core의 경우 [dotnet/docs](https://github.com/dotnet/docs/issues?q=is%3Aissue+label%3Abreaking-change) 리포지토리.
- ASP.NET Core의 경우 [aspnet/Announcements](https://github.com/aspnet/Announcements/issues?q=is%3Aissue+is%3Aopen+label%3A%22Breaking+change%22+label%3A3.0.0) 리포지토리.
- Entity Framework Core의 경우 [dotnet/efcore](https://github.com/dotnet/efcore/issues?q=is%3Aopen+is%3Aissue+label%3Abreaking-change) 리포지토리.

## <a name="see-also"></a>참조

- [.NET Framework에서 .NET Core로 마이그레이션](../porting/index.md)
