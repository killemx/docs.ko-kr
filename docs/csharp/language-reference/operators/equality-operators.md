---
title: 같음 연산자 - C# 참조
description: C# 같음 비교 연산자 및 C# 형식 같음에 대해 알아봅니다.
ms.date: 10/30/2020
author: pkulikov
f1_keywords:
- ==_CSharpKeyword
- '!=_CSharpKeyword'
helpviewer_keywords:
- comparison operators [C#]
- relational operators [C#]
- equality operator [C#]
- equals operator [C#]
- == operator [C#]
- inequality operator [C#]
- not equals operator [C#]
- '!= operator [C#]'
ms.openlocfilehash: 39461157c33fea0effb5c8808ded1c9981900e17
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063217"
---
# <a name="equality-operators-c-reference"></a>같음 연산자(C# 참조)

[`==`(같음)](#equality-operator-) 및 [`!=`(같지 않음)](#inequality-operator-) 연산자는 피연산자가 같은지 여부를 확인합니다.

## <a name="equality-operator-"></a>같음 연산자 ==

같음 연산자 `==`는 피연산자가 같으면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다.

### <a name="value-types-equality"></a>값 형식 같음

[기본 제공 값 형식](../builtin-types/value-types.md#built-in-value-types)의 피연산자는 해당 값이 같은 경우 동일합니다.

[!code-csharp-interactive[value types equality](snippets/shared/EqualityOperators.cs#ValueTypesEquality)]

> [!NOTE]
> `==`, [, `<`, `>`, `<=` 및 `>=`](comparison-operators.md) 연산자의 경우 피연산자 중 하나가 숫자(<xref:System.Double.NaN?displayProperty=nameWithType> 또는 <xref:System.Single.NaN?displayProperty=nameWithType>)가 아니면 연산의 결과는 `false`입니다. 즉, `NaN` 값이 `NaN`를 포함한 다른 `double`(또는 `float`) 값보다 크거나, 작거나, 같지 않습니다. 자세한 내용과 예제는 <xref:System.Double.NaN?displayProperty=nameWithType> 또는 <xref:System.Single.NaN?displayProperty=nameWithType> 참조 문서를 참조하세요.

기본 정수 형식의 해당 값이 같은 경우 동일한 [열거형](../builtin-types/enum.md) 형식의 피연산자가 동일합니다.

사용자 정의 [구조체](../builtin-types/struct.md) 형식은 기본적으로 `==` 연산자를 지원하지 않습니다. `==` 연산자를 지원하려면 사용자 정의 구조체가 해당 연산자를 [오버로드](operator-overloading.md)해야 합니다.

C# 7.3부터는 `==` 및 `!=` 연산자가 C# [튜플](../builtin-types/value-tuples.md)에서 지원됩니다. 자세한 내용은 [튜플 형식](../builtin-types/value-tuples.md) 문서의 [튜플 같음](../builtin-types/value-tuples.md#tuple-equality) 섹션을 참조하세요.

### <a name="reference-types-equality"></a>참조 형식 같음

기본적으로 두 개의 레코드가 아닌 참조 형식 피연산자는 동일한 개체를 참조하는 경우 같습니다.

[!code-csharp[reference type equality](snippets/shared/EqualityOperators.cs#ReferenceTypesEquality)]

이 예제에서 표시한 대로 사용자 지정 참조 형식은 기본적으로 `==` 연산자를 지원합니다. 그러나 참조 형식은 `==` 연산자를 오버로드할 수 있습니다. 참조 형식이 `==` 연산자를 오버로드하는 경우 <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> 메서드를 사용하여 해당 형식의 두 참조가 동일한 개체를 참조하는지 확인합니다.

### <a name="record-types-equality"></a>레코드 형식 같음

C# 9.0 이상에서 사용할 수 있는 [레코드 형식](../../whats-new/csharp-9.md#record-types)은 기본적으로 값 같음 의미 체계를 제공하는 `==` 및 `!=` 연산자를 지원합니다. 즉, 두 개의 레코드 피연산자는 둘 다 `null`이거나 모든 필드와 자동 구현 속성의 해당 값이 같은 경우에 같습니다.

:::code language="csharp" source="snippets/shared/EqualityOperators.cs" id="RecordTypesEquality":::

앞의 예제처럼 레코드가 아닌 참조 형식 멤버의 경우 참조되는 인스턴스가 아니라 해당 참조 값이 비교됩니다.

### <a name="string-equality"></a>문자열 같음

두 개의 [문자열](../builtin-types/reference-types.md#the-string-type) 피연산자가 모두 `null`이거나 두 문자열 인스턴스가 같은 길이고 각 문자 위치에 동일한 문자가 있을 때 동일합니다.

[!code-csharp-interactive[string equality](snippets/shared/EqualityOperators.cs#StringEquality)]

대/소문자 구분 서수 비교입니다. 문자열 비교에 대한 자세한 내용은 [C#에서 문자열을 비교하는 방법](../../how-to/compare-strings.md)을 참조하세요.

### <a name="delegate-equality"></a>대리자 같음

동일한 런타임 형식의 두 [대리자](../../programming-guide/delegates/index.md) 피연산자가 둘 다 `null`이거나 해당 호출 목록의 길이가 같고 각 위치에 동일한 항목이 있는 경우 두 피연산자는 같습니다.

[!code-csharp-interactive[delegate equality](snippets/shared/EqualityOperators.cs#DelegateEquality)]

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [대리자 같음 연산자](~/_csharplang/spec/expressions.md#delegate-equality-operators) 섹션을 참조하세요.

의미상 동일한 [람다 식](lambda-expressions.md) 평가에서 생성된 대리자는 다음 예제와 같이 동일하지 않습니다.

[!code-csharp-interactive[from identical lambdas](snippets/shared/EqualityOperators.cs#IdenticalLambdas)]

## <a name="inequality-operator-"></a>같지 않음 연산자 !=

같지 않음 연산자 `!=`는 피연산자가 같지 않으면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다. [기본 제공 형식](../builtin-types/built-in-types.md)의 피연산자의 경우 식 `x != y`는 식 `!(x == y)`와 동일한 결과를 생성합니다. 형식 같음에 대한 자세한 내용은 [같음 연산자](#equality-operator-) 섹션을 참조하세요.

다음 예제에서는 `!=` 연산자의 사용법을 보여 줍니다.

[!code-csharp-interactive[non-equality examples](snippets/shared/EqualityOperators.cs#NonEquality)]

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 `==` 및 `!=` 연산자를 [오버로드](operator-overloading.md)할 수 있습니다. 형식이 두 연산자 중 하나를 오버로드하는 경우 나머지 연산자도 오버로드해야 합니다.

레코드 형식은 `==` 및 `!=` 연산자를 명시적으로 오버로드할 수 없습니다. 레코드 형식 `T`에 대한 `==` 및 `!=` 연산자의 동작을 변경해야 하는 경우 다음 시그니처를 사용하여 <xref:System.IEquatable%601.Equals%2A?displayProperty=nameWithType> 메서드를 구현합니다.

```csharp
public virtual bool Equals(T? other);
```

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [관계형 및 형식 테스트 연산자](~/_csharplang/spec/expressions.md#relational-and-type-testing-operators) 섹션을 참조하세요.

레코드 형식 같음에 관한 자세한 내용은 [레코드 기능 제안 노트](~/_csharplang/proposals/csharp-9.0/records.md)의 [같음 멤버](~/_csharplang/proposals/csharp-9.0/records.md#equality-members) 섹션을 참조하세요.

## <a name="see-also"></a>참조

- [C# 참조](../index.md)
- [C# 연산자 및 식](index.md)
- <xref:System.IEquatable%601?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>
- [같음 비교](../../programming-guide/statements-expressions-operators/equality-comparisons.md)
- [비교 연산자](comparison-operators.md)
