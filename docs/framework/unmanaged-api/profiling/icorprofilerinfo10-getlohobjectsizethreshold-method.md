---
title: 'ICorProfilerInfo10:: GetLOHObjectSizeThreshold'
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo10.GetLOHObjectSizeThreshold
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 280f0a401f87f81e1ef9d4a2c85c06599442b5ec
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543948"
---
# <a name="icorprofilerinfo10getlohobjectsizethreshold-method"></a>ICorProfilerInfo10:: GetLOHObjectSizeThreshold 메서드

구성 된 LOH (large object heap) 임계값을 가져옵니다.

## <a name="syntax"></a>구문

```cpp
HRESULT GetLOHObjectSizeThreshold( [out] DWORD *pThreshold );
```

## <a name="parameters"></a>매개 변수

- `pThreshold`

  \[out] 대량 개체 힙 임계값 (바이트)입니다.

## <a name="remarks"></a>설명

큰 개체 힙 임계값 보다 큰 개체는 큰 개체 힙에 할당 됩니다. .NET Core 3.0부터 큰 개체 힙 임계값은 구성 가능 하며, `pThreshold` 활성 큰 개체 힙 임계값 크기 (바이트)를 포함 합니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [.Net Core 지원 운영 체제](../../../core/install/windows.md?pivots=os-windows)를 참조 하세요.

**헤더:** CorProf.idl, CorProf.h

**라이브러리:** CorGuids.lib

**.Net 버전:**[!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]

## <a name="see-also"></a>참조

- [ICorProfilerInfo10 인터페이스](icorprofilerinfo10-interface.md)
