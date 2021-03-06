---
title: ICorDebugClass 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass
helpviewer_keywords:
- ICorDebugClass interface [.NET Framework debugging]
ms.assetid: 03a6facb-f12f-49be-9839-e73b9c791cd5
topic_type:
- apiref
ms.openlocfilehash: d7417e8dc193172c77d23fe3fa72c8298d802b5c
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894036"
---
# <a name="icordebugclass-interface"></a>ICorDebugClass 인터페이스

기본 또는 복합(즉, 사용자 정의) 형식을 나타냅니다. 형식이 제네릭이면 `ICorDebugClass`는 인스턴스화되지 않은 제네릭 형식을 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetModule 메서드](icordebugclass-getmodule-method.md)|이 클래스를 정의 하는 모듈을 가져옵니다.|  
|[GetStaticFieldValue 메서드](icordebugclass-getstaticfieldvalue-method.md)|지정 된 정적 필드의 값을 가져옵니다.|  
|[GetToken 메서드](icordebugclass-gettoken-method.md)|이 클래스 `TypeDef` 에 대 한 메타 데이터 토큰을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 인터페이스 `ICorDebugClass` 는 인스턴스화되지 않은 제네릭 형식을 나타냅니다. ICorDebugType 인터페이스는 인스턴스화된 제네릭 형식을 나타냅니다. 예 `Hashtable<K, V>` `ICorDebugClass`를 들어는로 표현 되는 반면 `Hashtable<Int32, String>` 는로 표현 됩니다 `ICorDebugType`.  
  
 제네릭이 아닌 형식은 `ICorDebugClass` 및 `ICorDebugType`로 표시 됩니다. 후자 인터페이스는 형식 인스턴스화를 처리 하기 위해 .NET Framework 버전 2.0에서 도입 되었습니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:**[시스템 요구 사항](../../get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참조

- [디버깅 인터페이스](debugging-interfaces.md)
