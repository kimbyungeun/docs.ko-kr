---
title: -verbose
ms.date: 03/13/2018
helpviewer_keywords:
- verbose compiler option [Visual Basic]
- -verbose compiler option [Visual Basic]
- /verbose compiler option [Visual Basic]
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
ms.openlocfilehash: 8c5bc1d2ce331b8fe9461f91d64fbeab5a070b59
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004980"
---
# <a name="-verbose"></a>-verbose
컴파일러가 자세한 상태 및 오류 메시지를 생성하도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-verbose[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 선택 사항입니다. `-verbose`를 지정하는 것은 `-verbose+`를 지정하는 것과 동일하며, 이로 인해 컴파일러가 자세한 정보 메시지를 내보냅니다. 이 옵션의 기본값은 `-verbose-`입니다.  
  
## <a name="remarks"></a>설명  
 `-verbose` 옵션은 컴파일러에서 발생한 총 오류 수에 대한 정보를 표시하고, 모듈에서 로드되는 어셈블리를 보고하고, 현재 컴파일되는 파일을 표시합니다.  
  
> [!NOTE]
> Visual Studio 개발 환경 내에서는 `-verbose` 옵션을 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드는 `In.vb`를 컴파일하고 자세한 상태 정보를 표시하도록 컴파일러에 지시합니다.  
  
```console  
vbc -verbose in.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
