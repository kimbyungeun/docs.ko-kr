---
title: EnumImportTypes 메서드
ms.date: 03/30/2017
api_name:
- EnumImportTypes
- IALink.EnumImportTypes
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EnumImportTypes
helpviewer_keywords:
- EnumImportTypes method
ms.assetid: 83a0e4e7-ec06-40cb-9b63-700b9695bb04
topic_type:
- apiref
ms.openlocfilehash: ca7c7570aff63aa328dddc0626648fa74397addc
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448741"
---
# <a name="enumimporttypes-method"></a>EnumImportTypes 메서드

각 범위에서 각 형식을 열거 합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT EnumImportTypes(
    HALINKENUM   hEnum,
    DWORD        dwMax,
    mdTypeDef    aTypeDefs[],
    DWORD*       pdwCount
) PURE;
```

## <a name="parameters"></a>매개 변수

`hEnum`\
열거자에 대 한 핸들입니다.

`dwMax`\
검색할 최대 형식 수입니다.

`aTypeDefs`\
`dwMax`를 초과 하지 않는 형식 토큰을 받습니다.

`pdwCount`\
`aTypeDefs`에서 실제 형식의 수를 받습니다.

## <a name="return-value"></a>반환 값

메서드가 성공 하면 S_OK을 반환 합니다.

## <a name="requirements"></a>요구 사항

Alink 필요

## <a name="see-also"></a>참고자료

- [IALink 인터페이스](ialink-interface.md)
- [IALink2 인터페이스](ialink2-interface.md)
- [ALink API](index.md)
