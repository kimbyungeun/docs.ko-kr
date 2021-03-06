---
title: '방법: 열거형 값과 연결된 문자열 확인'
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
- strings [Visual Basic], enumeration values
- values [Visual Basic], enumeration members
ms.assetid: 9253e7c8-579c-49a2-8f26-392b20ea99eb
ms.openlocfilehash: c396a4e2ebe973f5be65c3fab5f22cdedb29be1a
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351142"
---
# <a name="how-to-determine-the-string-associated-with-an-enumeration-value-visual-basic"></a>방법: 열거형 값과 연결된 문자열 확인(Visual Basic)
<xref:System.Enum.GetValues%2A> 및 <xref:System.Enum.GetNames%2A> 메서드를 사용 하 여 열거형 멤버와 연결 된 문자열 및 값을 확인할 수 있습니다.  
  
### <a name="to-determine-the-string-associated-with-an-enumeration"></a>열거형과 연결 된 문자열을 확인 하려면  
  
- <xref:System.Enum.GetNames%2A> 메서드를 사용 하 여 열거형 멤버와 연결 된 문자열을 검색 합니다. 이 예제에서는 열거형 `flavorEnum`선언한 다음 <xref:System.Enum.GetNames%2A> 메서드를 사용 하 여 각 멤버와 관련 된 문자열을 표시 합니다.  
  
     [!code-vb[VbEnumsTask#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#2)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Enum.GetValues%2A>
- <xref:System.Enum.GetNames%2A>
- <xref:System.Enum>
- [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [방법: Visual Basic에서 열거형 반복](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [열거형을 사용하는 경우](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [Enum 문](../../../../visual-basic/language-reference/statements/enum-statement.md)
