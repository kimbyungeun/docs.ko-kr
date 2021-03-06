---
title: ICorProfilerInfo::GetFunctionInfo 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetFunctionInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetFunctionInfo
helpviewer_keywords:
- ICorProfilerInfo::GetFunctionInfo method [.NET Framework profiling]
- GetFunctionInfo method [.NET Framework profiling]
ms.assetid: c42b5891-019d-46b3-b551-4606295b75b8
topic_type:
- apiref
ms.openlocfilehash: 823cc5638ff3e0955aca0bd9ba5795f6b369c6b0
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76863623"
---
# <a name="icorprofilerinfogetfunctioninfo-method"></a>ICorProfilerInfo::GetFunctionInfo 메서드
지정 된 함수에 대 한 부모 클래스 및 메타 데이터 토큰을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFunctionInfo(  
    [in]  FunctionID functionId,  
    [out] ClassID    *pClassId,  
    [out] ModuleID   *pModuleId,  
    [out] mdToken    *pToken);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 진행 부모 클래스 및 메타 데이터 토큰을 가져올 함수의 ID입니다.  
  
 `pClassId`  
 [out] 함수의 부모 클래스에 대한 포인터입니다.  
  
 `pModuleId`  
 [out] 함수의 부모 클래스가 정의된 모듈에 대한 포인터입니다.  
  
 `pToken`  
 [out] 함수의 메타데이터 토큰에 대한 포인터입니다.  
  
## <a name="remarks"></a>주의  
 프로파일러 코드는 [ICorProfilerInfo:: GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 를 호출 하 여 지정 된 모듈에 대 한 메타 데이터 인터페이스를 가져올 수 있습니다. `pToken`에서 참조하는 위치로 반환되는 메타데이터 토큰을 사용하여 함수에 대한 메타데이터에 액세스할 수 있습니다.  
  
 함수 사용에 대 한 추가 컨텍스트 정보 없이 제네릭 클래스에 대 한 함수 `ClassID`를 얻을 수 없습니다. 이 경우 `pClassId`은 0이 됩니다. 프로파일러 코드는 COR_PRF_FRAME_INFO 값을 사용 하 여 [ICorProfilerInfo2:: GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md) 를 사용 하 여 더 많은 컨텍스트를 제공 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참조

- [ICorProfilerInfo 인터페이스](icorprofilerinfo-interface.md)
