---
title: IHostPolicyManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostPolicyManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostPolicyManager
helpviewer_keywords:
- IHostPolicyManager interface [.NET Framework hosting]
ms.assetid: 8c4aa124-5e00-46d9-b1e8-57ba6574bb0d
topic_type:
- apiref
ms.openlocfilehash: db089a55128fa675ceedf157b046fe205d8c6b51
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804333"
---
# <a name="ihostpolicymanager-interface"></a>IHostPolicyManager 인터페이스
중단, 시간 초과 또는 오류가 발생 하는 경우 CLR (공용 언어 런타임)에서 수행 하는 작업을 호스트에 알리는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[OnDefaultAction 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-ondefaultaction-method.md)|CLR이 스레드 abort 또는 unload에 대 한 응답으로 [ICLRPolicyManager:: SetDefaultAction](iclrpolicymanager-setdefaultaction-method.md) 에 대 한 호출로 지정 된 기본 작업을 수행 하려고 함을 호스트에 알립니다 <xref:System.AppDomain> .|  
|[OnFailure 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-onfailure-method.md)|리소스 할당 또는 재사용 실패에 대 한 응답으로 CLR이 [ICLRPolicyManager:: SetActionOnFailure](iclrpolicymanager-setactiononfailure-method.md) 호출에 지정 된 작업을 수행 하려고 함을 호스트에 알립니다.|  
|[OnTimeout 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-ontimeout-method.md)|시간 제한에 대 한 응답으로 CLR이 [ICLRPolicyManager:: SetActionOnTimeout](iclrpolicymanager-setactionontimeout-method.md) 호출로 지정 된 작업을 수행 하려고 함을 호스트에 알립니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:**[시스템 요구 사항](../../get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Mscoree.dll  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [EClrFailure 열거형](eclrfailure-enumeration.md)
- [EClrOperation 열거형](eclroperation-enumeration.md)
- [EPolicyAction 열거형](epolicyaction-enumeration.md)
- [ICLRPolicyManager 인터페이스](iclrpolicymanager-interface.md)
- [호스팅 인터페이스](hosting-interfaces.md)
