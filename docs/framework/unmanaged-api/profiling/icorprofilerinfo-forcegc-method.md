---
title: ICorProfilerInfo::ForceGC 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.ForceGC
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::ForceGC
helpviewer_keywords:
- ICorProfilerInfo::ForceGC method [.NET Framework profiling]
- ForceGC method [.NET Framework profiling]
ms.assetid: 0da1ef80-d242-4636-87d0-43e0470b342a
topic_type:
- apiref
ms.openlocfilehash: e1fe38419cda328c919f0840d51cf6336919aa60
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76864221"
---
# <a name="icorprofilerinfoforcegc-method"></a>ICorProfilerInfo::ForceGC 메서드
CLR (공용 언어 런타임) 내에서 가비지 수집을 강제로 수행 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ForceGC();  
```  
  
## <a name="remarks"></a>주의  
 `ForceGC` 메서드는 관리 코드를 실행 하지 않고 스택에 프로파일러 콜백이 없는 스레드에서만 호출 해야 합니다. 가장 편리한 구현은 신호를 받을 때 `ForceGC`를 호출 하는 프로파일러 내에 별도의 스레드를 만드는 것입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참조

- [ICorProfilerInfo 인터페이스](icorprofilerinfo-interface.md)
