---
title: <example>
ms.date: 07/20/2015
helpviewer_keywords:
- example XML tag
- <example> XML tag
ms.assetid: 90eeda1c-3fc4-427c-879c-5046d265a97c
ms.openlocfilehash: 8f36ac1337dd0d1400180fbd3deae2bb24ad9c58
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348488"
---
# <a name="example-visual-basic"></a>\<예제 > (Visual Basic)
멤버에 대 한 예제를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<example>description</example>  
```  
  
## <a name="parameters"></a>매개 변수  
 `description`  
 코드 샘플에 대한 설명입니다.  
  
## <a name="remarks"></a>주의  
 `<example>` 태그를 사용 하 여 메서드 또는 다른 라이브러리 멤버를 사용 하는 방법에 대 한 예제를 지정할 수 있습니다. 여기에는 일반적으로 [\<code>](../../../visual-basic/language-reference/xmldoc/code.md) 태그를 같이 사용합니다.  
  
 [-doc](../../../visual-basic/reference/command-line-compiler/doc.md)로 컴파일하여 문서 주석을 파일로 처리합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 `<example>` 태그를 사용 하 여 `ID` 필드를 사용 하는 예제를 포함 합니다.  
  
 [!code-vb[VbVbcnXmlDocComments#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#2)]  
  
## <a name="see-also"></a>참고 항목

- [XML 주석 태그](../../../visual-basic/language-reference/xmldoc/index.md)
