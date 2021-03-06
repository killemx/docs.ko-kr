---
title: '방법: SpinLock에서 스레드-추적 모드 사용'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to enable thread-tracking
ms.assetid: 62ee2e68-0bdd-4869-afc9-f0a57a11ae01
ms.openlocfilehash: 1a46655530948bb8732362dbd6d86ead495b0998
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279532"
---
# <a name="how-to-enable-thread-tracking-mode-in-spinlock"></a>방법: SpinLock에서 스레드-추적 모드 사용
<xref:System.Threading.SpinLock?displayProperty=nameWithType>은 대기 시간이 매우 짧은 시나리오에 사용할 수 있는 하위 수준의 상호 배제적인 잠금입니다. <xref:System.Threading.SpinLock>은 재진입 항목이 아닙니다. 스레드가 잠금 상태가 된 후에는 잠금을 올바르게 종료해야 다시 잠글 수 있습니다. 일반적으로 잠금을 다시 설정하려고 하면 교착 상태가 발생하고, 교착 상태는 디버그하기가 매우 어려울 수 있습니다. 개발에 대한 지원으로 <xref:System.Threading.SpinLock?displayProperty=nameWithType>은 스레드가 이미 보유하고 있는 잠금을 다시 설정하려고 할 때 예외가 throw되도록 하는 스레드 추적 모드를 지원합니다. 따라서 잠금이 올바르게 종료되지 않은 지점을 쉽게 찾을 수 있습니다. 부울 입력 매개 변수를 사용하고 `true`의 인수를 전달하는 <xref:System.Threading.SpinLock> 생성자를 사용하여 스레드 추적 모드를 켤 수 있습니다. 개발 및 테스트 단계를 완료한 후에는 성능을 향상시키기 위해 스레드 추적 모드를 끄세요.  
  
## <a name="example"></a>예제  
 다음 예제는 스레드 추적 모드를 보여줍니다. 잠금을 올바르게 종료하는 줄은 다음 결과 중 하나를 발생시키는 코딩 오류를 시뮬레이트하기 위해 주석으로 처리됩니다.  
  
- <xref:System.Threading.SpinLock>이 `true`(Visual Basic의 경우 `True`)의 인수를 사용하여 생성된 경우 예외가 throw됩니다.  
  
- <xref:System.Threading.SpinLock>이 `false`(Visual Basic의 경우 `False`)의 인수를 사용하여 생성된 경우 교착 상태가 됩니다.  
  
 [!code-csharp[CDS_SpinLock#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#01)]
 [!code-vb[CDS_SpinLock#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_threadtracking.vb#01)]  
  
## <a name="see-also"></a>참조

- [스핀 잠금](spinlock.md)
