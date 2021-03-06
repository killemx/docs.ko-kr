---
title: '정규식 예제: 날짜 형식 변경'
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET regular expressions, examples
- regular expressions [.NET], examples
- pattern-matching with regular expressions, examples
ms.assetid: 5fcc75a5-09d7-45ae-a4c0-9ad6085ac83d
ms.openlocfilehash: b5eca8c294349fada9cfb1cb3ed8e2012edd8bda
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889415"
---
# <a name="regular-expression-example-changing-date-formats"></a>정규식 예제: 날짜 형식 변경
다음 코드 예제에서는 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 메서드를 사용하여 *mm*/*dd*/*yy* 형식의 날짜를 *dd*-*mm*-*yy* 형식의 날짜로 바꿉니다.  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a>예제  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 다음 코드에서는 애플리케이션에서 `MDYToDMY` 메서드를 호출하는 방법을 보여 줍니다.  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## <a name="comments"></a>설명  
 정규식 패턴 `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b`는 다음 표와 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`(?<month>\d{1,2})`|한 개 또는 두 개의 10진수를 찾습니다. 캡처된 `month` 그룹입니다.|  
|`/`|슬래시 기호를 찾습니다.|  
|`(?<day>\d{1,2})`|한 개 또는 두 개의 10진수를 찾습니다. 캡처된 `day` 그룹입니다.|  
|`/`|슬래시 기호를 찾습니다.|  
|`(?<year>\d{2,4})`|2~4개의 10진수를 찾습니다. 캡처된 `year` 그룹입니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 `${day}-${month}-${year}` 패턴은 다음 표와 같이 대체 문자열을 정의합니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`$(day)`|`day` 캡처링 그룹에 의해 캡처된 부분 문자열을 추가합니다.|  
|`-`|하이픈을 추가합니다.|  
|`$(month)`|`month` 캡처링 그룹에 의해 캡처된 부분 문자열을 추가합니다.|  
|`-`|하이픈을 추가합니다.|  
|`$(year)`|`year` 캡처링 그룹에 의해 캡처된 부분 문자열을 추가합니다.|  
  
## <a name="see-also"></a>참고 항목

- [.NET 정규식](regular-expressions.md)
