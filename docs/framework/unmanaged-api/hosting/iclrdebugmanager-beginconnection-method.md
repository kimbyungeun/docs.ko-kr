---
title: ICLRDebugManager::BeginConnection 메서드
ms.date: 03/30/2017
api_name:
- ICLRDebugManager.BeginConnection
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDebugManager::BeginConnection
helpviewer_keywords:
- ICLRDebugManager::BeginConnection method [.NET Framework hosting]
- BeginConnection method [.NET Framework hosting]
ms.assetid: bdd98146-ff4d-4150-a264-a4c1a32d31f3
topic_type:
- apiref
ms.openlocfilehash: fc25e250938d7549c7a9693bee937d4756268b93
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615815"
---
# <a name="iclrdebugmanagerbeginconnection-method"></a>ICLRDebugManager::BeginConnection 메서드
작업 목록과 식별자를 연결 하기 위해 호스트와 디버거 간에 새 연결을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT BeginConnection (  
    [in] CONNID dwConnectionId,  
    [in, string] wchar_t* szConnectionName  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwConnectionId`  
 진행 CLR (공용 언어 런타임) 작업 목록과 연결할 식별자입니다.  
  
 `szConnectionName`  
 진행 CLR 작업 목록과 연결할 이름입니다.  
  
## <a name="return-value"></a>Return Value  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|`BeginConnection`성공적으로 반환 되었습니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|차단 된 스레드나 파이버에서 대기 하는 동안 이벤트를 취소 했습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL 반환 된 후에는 프로세스 내에서 CLR을 더 이상 사용할 수 없습니다. 호스팅 메서드를 이후에 호출 하면 HOST_E_CLRNOTAVAILABLE 반환 됩니다.|  
|E_INVALIDARG|`dwConnectionId`가 0 이거나 `BeginConnection` 이 값을 사용 하 여 이미 호출 `dwConnectionId` 되었거나 `szConnectionName` 가 null 인 경우|  
|E_OUTOFMEMORY|메모리가 부족 하 여이 연결과 관련 된 작업 목록을 저장할 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 [ICLRDebugManager](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-interface.md) 는 작업 목록과 식별자를 연결 하는 데 사용 되는 세 가지 메서드인 `BeginConnection` , [Setconnectiontasks](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setconnectiontasks-method.md)및 [endconnection](iclrdebugmanager-endconnection-method.md)을 제공 합니다.  
  
> [!IMPORTANT]
> 이러한 세 메서드는 각 작업 집합에 대해 특정 순서로 호출 되어야 합니다. `BeginConnection`새 연결을 설정 하기 위해가 먼저 호출 됩니다. `SetConnectionTasks`는 해당 연결과 관련 된 태스크 집합을 제공 하기 위해 다음에 호출 됩니다. `EndConnection`작업 목록과 식별자와 이름 간의 연결을 제거 하기 위해 마지막으로 호출 됩니다. 그러나 다른 연결에 대 한 호출은 중첩할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:**[시스템 요구 사항](../../get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Mscoree.dll  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [ICLRControl 인터페이스](iclrcontrol-interface.md)
- [ICLRDebugManager 인터페이스](iclrdebugmanager-interface.md)
- [EndConnection 메서드](iclrdebugmanager-endconnection-method.md)
- [SetConnectionTasks 메서드](iclrdebugmanager-setconnectiontasks-method.md)
- [IHostControl 인터페이스](ihostcontrol-interface.md)
