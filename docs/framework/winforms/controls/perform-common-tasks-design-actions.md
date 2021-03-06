---
title: 컨트롤에서 디자이너 작업을 사용 하 여 일반적인 작업 수행
ms.date: 02/13/2019
helpviewer_keywords:
- designer actions
ms.assetid: cac337e6-00f6-4584-80f4-75728f5ea113
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 342741b9ce032b1b8ec50a6c689d9109d12f5b3b
ms.sourcegitcommit: 44a7cd8687f227fc6db3211ccf4783dc20235e51
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77634896"
---
# <a name="walkthrough-perform-common-tasks-using-designer-actions"></a>연습: 디자이너 작업을 사용 하 여 일반 작업 수행

Windows Forms 응용 프로그램에 대 한 폼과 컨트롤을 구성할 때 반복적으로 수행 하는 많은 태스크가 있습니다. 다음 목록에서는 일반적으로 수행 하는 작업을 보여 줍니다.

- <xref:System.Windows.Forms.TabControl>에서 탭 추가 또는 제거
- 컨트롤을 부모에 도킹 합니다.
- <xref:System.Windows.Forms.SplitContainer> 컨트롤의 방향 변경

개발 속도를 높이기 위해 많은 컨트롤은 디자이너 작업을 제공 합니다. 디자이너 작업은 디자인 타임에 단일 제스처로 이와 같은 일반적인 작업을 수행할 수 있는 상황에 맞는 메뉴입니다. 이러한 작업을 *디자이너 작업 동사*라고 합니다.

디자이너 작업은 디자이너에서 수명 동안 컨트롤 인스턴스에 연결 된 상태로 유지 되며 항상 사용할 수 있습니다.

## <a name="create-the-project"></a>프로젝트 만들기

첫 번째 단계는 프로젝트를 만들고 폼을 설정하는 것입니다.

1. Visual Studio에서 **DesignerActionsExample**이라는 Windows 기반 응용 프로그램 프로젝트를 만듭니다.

2. **Windows Forms 디자이너**에서 양식을 선택 합니다.

## <a name="use-designer-actions"></a>디자이너 작업 사용

디자이너 작업은 디자인 타임에이를 제공 하는 컨트롤에서 항상 사용할 수 있습니다.

1. <xref:System.Windows.Forms.TabControl>를 **도구 상자** 에서 폼으로 끌어옵니다. <xref:System.Windows.Forms.TabControl>측면에 표시 되는 디자이너 작업 문자 모양 (![작은 검은색 화살표](./media/designer-actions-glyph.gif))을 확인 합니다.

2. 디자이너 작업 문자 모양을 클릭 합니다. 문자 모양 옆에 나타나는 바로 가기 메뉴에서 **추가 탭** 항목을 선택 합니다. 새 탭 페이지가 <xref:System.Windows.Forms.TabControl>에 추가 되는지 확인 합니다.

3. <xref:System.Windows.Forms.TableLayoutPanel> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

4. 디자이너 작업 문자 모양을 클릭 합니다. 문자 모양 옆에 나타나는 바로 가기 메뉴에서 **열 추가** 항목을 선택 합니다. 새 열이 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤에 추가 되는지 확인 합니다.

5. <xref:System.Windows.Forms.SplitContainer> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

6. 디자이너 작업 문자 모양을 클릭 합니다. 문자 모양 옆에 나타나는 바로 가기 메뉴에서 **가로 분할자 방향** 항목을 선택 합니다. <xref:System.Windows.Forms.SplitContainer> 컨트롤의 분할자 막대가 이제 가로 방향으로 표시 되는지 확인 합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.Forms.TextBox>
- <xref:System.Windows.Forms.TabControl>
- <xref:System.Windows.Forms.SplitContainer>
- <xref:System.ComponentModel.Design.DesignerActionList>
