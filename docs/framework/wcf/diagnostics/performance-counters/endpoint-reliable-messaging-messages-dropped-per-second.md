---
title: '엔드포인트: Reliable Messaging Messages Dropped Per Second'
ms.date: 03/30/2017
ms.assetid: ea3c4fc0-1e0f-4863-8879-57bc6c113018
ms.openlocfilehash: 06259ba0d60d9f1cec7717364f2e014bb123ee40
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90550269"
---
# <a name="endpoint-reliable-messaging-messages-dropped-per-second"></a>엔드포인트: Reliable Messaging Messages Dropped Per Second
카운터 이름: Reliable Messaging Sessions Dropped Per Second.  
  
## <a name="description"></a>Description  
 이 엔드포인트에서 삭제된 신뢰할 수 있는 메시징 메시지의 초당 총 수입니다.  
  
 이 카운터는 다음 수식을 사용 하 여 값을 계산 하는 성능 카운터 유형 [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10))입니다.  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)
