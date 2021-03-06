---
title: '방법: 바이트 배열을 문자열로 변환'
ms.date: 07/20/2015
helpviewer_keywords:
- string conversion [Visual Basic], arrays
- byte arrays [Visual Basic], converting to strings
- examples [Visual Basic], strings
- arrays [Visual Basic], converting to strings
ms.assetid: d0dc8317-9ab3-4324-99f7-3f5788c0e72a
ms.openlocfilehash: 8c1d9d1d2e89390873bc1c3dbb9623f047433a9a
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351983"
---
# <a name="how-to-convert-an-array-of-bytes-into-a-string-in-visual-basic"></a>방법: Visual Basic에서 바이트 배열을 문자열로 변환
이 항목에서는 바이트 배열의 바이트를 문자열로 변환 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> encoding 클래스의 <xref:System.Text.Encoding.GetString%2A> 메서드를 사용 하 여 바이트 배열의 모든 바이트를 문자열로 변환 합니다.  
  
 [!code-vb[VbVbalrStrings#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#72)]  
  
 여러 인코딩 옵션 중에서 선택 하 여 바이트 배열을 문자열로 변환할 수 있습니다.  
  
- <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType>: ASCII (7 비트) 문자 집합에 대 한 인코딩을 가져옵니다.  
  
- <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=nameWithType>: 빅 endian 바이트 순서를 사용 하는 UTF-16 형식에 대 한 인코딩을 가져옵니다.  
  
- <xref:System.Text.Encoding.Default%2A?displayProperty=nameWithType>: 시스템의 현재 ANSI 코드 페이지에 대 한 인코딩을 가져옵니다.  
  
- <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType>: 작은 endian 바이트 순서를 사용 하 여 UTF-16 형식에 대 한 인코딩을 가져옵니다.  
  
- <xref:System.Text.Encoding.UTF32%2A?displayProperty=nameWithType>: 작은 endian 바이트 순서를 사용 하 여 32 형식에 대 한 인코딩을 가져옵니다.  
  
- <xref:System.Text.Encoding.UTF7%2A?displayProperty=nameWithType>: UTF-7 형식에 대 한 인코딩을 가져옵니다.  
  
- <xref:System.Text.Encoding.UTF8%2A?displayProperty=nameWithType>: UTF-8 형식에 대 한 인코딩을 가져옵니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Text.Encoding?displayProperty=nameWithType>
- <xref:System.Text.Encoding.GetString%2A>
- [방법: Visual Basic에서 문자열을 바이트 배열로 변환](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-strings-into-an-array-of-bytes.md)
