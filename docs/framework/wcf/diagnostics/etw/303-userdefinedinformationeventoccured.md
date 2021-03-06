---
title: 303 - UserDefinedInformationEventOccured
ms.date: 03/30/2017
ms.assetid: 5ed5acaf-3755-4417-92c4-4ebc8e854ca1
ms.openlocfilehash: 0b782b5ac0527b5acb3ebf0bf11c117563042495
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61595781"
---
# <a name="303---userdefinedinformationeventoccured"></a>303 - UserDefinedInformationEventOccured
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|ID|303|  
|키워드|문제 해결, HealthMonitoring, UserEvents, ServiceModel, EndToEndMonitoring|  
|수준|정보|  
|채널|Microsoft-Windows-애플리케이션 서버-애플리케이션/분석|  
  
## <a name="description"></a>설명  
 이 이벤트는 사용자 코드에서 내보내집니다. 개발자는 자신의 서비스에서 사용자 정의 정보 이벤트가 발생할 때 이 이벤트를 내보낼 수 있습니다. 이 작업은 <xref:System.Diagnostics.Eventing> API를 사용하여 수행할 수 있습니다. 이외에도 이 API를 래핑하고 이 이벤트를 적절히 내보내는 방법을 보여 주는 WCF 샘플을 사용할 수도 있습니다.  
  
## <a name="message"></a>메시지  
 이름:'%1', 참조:'%2', 페이로드:%3  
  
## <a name="details"></a>설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|--------------------|--------------------|-----------------|  
|이름|`xs:string`|이벤트의 사용자 정의 이름입니다.|  
|HostReference|`xs:string`|웹 호스팅 서비스의 경우 이 필드는 웹 계층의 서비스를 고유하게 식별합니다. 해당 형식으로 정의 됩니다 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'. 예제: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.|  
|Payload|`xs:string`|이벤트의 사용자 정의 페이로드입니다.|
