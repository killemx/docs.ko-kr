---
title: "'If' 이항 식의 첫 번째 피연산자는 nullable이거나 참조 형식이어야 합니다."
ms.date: 07/20/2015
f1_keywords:
- bc33107
- vbc33107
helpviewer_keywords:
- BC33107
ms.assetid: 493c8899-3f6b-4471-8eb6-9284e8492768
ms.openlocfilehash: bca9b74a68815b4e5a3bb2dc114b9031cdf24099
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162741"
---
# <a name="bc33107-first-operand-in-a-binary-if-expression-must-be-nullable-or-a-reference-type"></a>BC33107: 이항 ' If ' 식의 첫 번째 피연산자는 nullable 이거나 참조 형식 이어야 합니다.

식에는 `If` 두 개 또는 세 개의 인수를 사용할 수 있습니다. 두 개의 인수만 전송 하는 경우 첫 번째 인수는 참조 형식 이거나 nullable 값 형식 이어야 합니다. 첫 번째 인수가 이외의 값으로 계산 되 면 `Nothing` 해당 값이 반환 됩니다. 첫 번째 인수가로 계산 되는 경우 `Nothing` 두 번째 인수가 계산 되어 반환 됩니다.

 예를 들어, 다음 코드에는 세 개의 인수와 두 개의 인수를 사용 하는 식이 포함 되어 있습니다 `If` . 식은 동일한 값을 계산 하 고 반환 합니다.

```vb
' firstChoice is a nullable value type.
Dim firstChoice? As Integer = Nothing
Dim secondChoice As Integer = 1128
' If expression with three arguments.
Console.WriteLine(If(firstChoice IsNot Nothing, firstChoice, secondChoice))
' If expression with two arguments.
Console.WriteLine(If(firstChoice, secondChoice))
```

 다음 식에서이 오류가 발생 합니다.

```vb
Dim choice1 = 4
Dim choice2 = 5
Dim booleanVar = True

' Not valid.
'Console.WriteLine(If(choice1 < choice2, 1))
' Not valid.
'Console.WriteLine(If(booleanVar, "Test returns True."))
```

 **오류 ID:** BC33107

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

- 첫 번째 인수가 nullable 값 형식 또는 참조 형식이 되도록 코드를 변경할 수 없는 경우에는 세 인수 식으로 변환 하거나 문으로 변환 하는 것이 좋습니다 `If` `If...Then...Else` .

```vb
Console.WriteLine(If(choice1 < choice2, 1, 2))
Console.WriteLine(If(booleanVar, "Test returns True.", "Test returns False."))
```

## <a name="see-also"></a>참고 항목

- [If 연산자](../operators/if-operator.md)
- [If...Then...Else 문](../statements/if-then-else-statement.md)
- [Nullable 값 형식](../../programming-guide/language-features/data-types/nullable-value-types.md)
