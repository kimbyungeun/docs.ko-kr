---
title: '연습: DataGridView 컨트롤의 데이터 유효성 검사'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- validating data [Windows Forms], Windows Forms
- data [Windows Forms], validation
- DataGridView control [Windows Forms], data validation
- data grids [Windows Forms], validating data
- data validation [Windows Forms], Windows Forms
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: a4f1d015-2969-430c-8ea2-b612d179c290
ms.openlocfilehash: 45753fb206ad58616c9a727bd81bd2458db6053e
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76740093"
---
# <a name="walkthrough-validating-data-in-the-windows-forms-datagridview-control"></a>연습: Windows Forms DataGridView 컨트롤의 데이터 유효성 검사

사용자에 게 데이터 입력 기능을 표시 하는 경우 폼에 입력 한 데이터의 유효성을 검사 해야 하는 경우가 많습니다. <xref:System.Windows.Forms.DataGridView> 클래스는 데이터를 데이터 저장소에 커밋하기 전에 유효성 검사를 수행 하는 편리한 방법을 제공 합니다. 현재 셀이 변경 될 때 <xref:System.Windows.Forms.DataGridView>에서 발생 하는 <xref:System.Windows.Forms.DataGridView.CellValidating> 이벤트를 처리 하 여 데이터의 유효성을 검사할 수 있습니다.

이 연습에서는 Northwind 샘플 데이터베이스의 `Customers` 테이블에서 행을 검색 하 여 <xref:System.Windows.Forms.DataGridView> 컨트롤에 표시 합니다. 사용자가 `CompanyName` 열의 셀을 편집 하 여 셀을 벗어나면 <xref:System.Windows.Forms.DataGridView.CellValidating> 이벤트 처리기는 새 회사 이름 문자열을 검사 하 여 비어 있지 않은지 확인 합니다. 새 값이 빈 문자열이 면 <xref:System.Windows.Forms.DataGridView>은 비어 있지 않은 문자열을 입력할 때까지 사용자의 커서가 셀을 벗어날 수 없도록 합니다.

이 항목의 코드를 단일 목록으로 복사 하려면 [방법: Windows Forms DataGridView 컨트롤의 데이터 유효성 검사](how-to-validate-data-in-the-windows-forms-datagridview-control.md)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

이 연습을 완료하려면 다음 사항이 필요합니다.

- Northwind SQL Server 예제 데이터베이스가 있는 서버에 액세스 합니다.

## <a name="creating-the-form"></a>폼 만들기

#### <a name="to-validate-data-entered-in-a-datagridview"></a>DataGridView에 입력 한 데이터의 유효성을 검사 하려면

1. <xref:System.Windows.Forms.Form>에서 파생 되 고 <xref:System.Windows.Forms.DataGridView> 컨트롤과 <xref:System.Windows.Forms.BindingSource> 구성 요소를 포함 하는 클래스를 만듭니다.

    다음 코드 예제에서는 기본 초기화를 제공 하며 `Main` 메서드를 포함 합니다.

    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#01](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#01)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#01](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#01)]
    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#02](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#02](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#02)]

2. 데이터베이스 연결에 대 한 세부 정보를 처리 하기 위해 폼의 클래스 정의에 메서드를 구현 합니다.

    이 코드 예제에서는 채워진 <xref:System.Data.DataTable> 개체를 반환 하는 `GetData` 메서드를 사용 합니다. `connectionString` 변수를 데이터베이스에 적합 한 값으로 설정 해야 합니다.

    > [!IMPORTANT]
    > 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 애플리케이션 보안 문제가 발생할 수 있습니다. 통합 보안이 라고도 하는 Windows 인증을 사용 하 여 데이터베이스에 대 한 액세스를 보다 안전 하 게 제어할 수 있습니다. 자세한 내용은 [연결 정보 보호](../../data/adonet/protecting-connection-information.md)를 참조하세요.

    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#30)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#30)]

3. <xref:System.Windows.Forms.DataGridView>를 초기화 하 고 데이터 바인딩을 <xref:System.Windows.Forms.BindingSource> 하 고 설정 하는 폼의 <xref:System.Windows.Forms.Form.Load> 이벤트에 대 한 처리기를 구현 합니다.

    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#10)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#10)]

4. <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.CellValidating> 및 <xref:System.Windows.Forms.DataGridView.CellEndEdit> 이벤트에 대 한 처리기를 구현 합니다.

    <xref:System.Windows.Forms.DataGridView.CellValidating> 이벤트 처리기는 `CompanyName` 열의 셀 값이 비어 있는지 여부를 확인 하는 위치입니다. 셀 값의 유효성 검사가 실패 하면 <xref:System.Windows.Forms.DataGridViewCellValidatingEventArgs?displayProperty=nameWithType> 클래스의 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 속성을 `true`로 설정 합니다. 이렇게 하면 <xref:System.Windows.Forms.DataGridView> 컨트롤에서 커서가 셀을 벗어날 수 없습니다. 행의 <xref:System.Windows.Forms.DataGridViewRow.ErrorText%2A> 속성을 설명 문자열로 설정 합니다. 그러면 오류 텍스트를 포함 하는 도구 설명이 포함 된 오류 아이콘이 표시 됩니다. <xref:System.Windows.Forms.DataGridView.CellEndEdit> 이벤트 처리기에서 행의 <xref:System.Windows.Forms.DataGridViewRow.ErrorText%2A> 속성을 빈 문자열로 설정 합니다. <xref:System.Windows.Forms.DataGridView.CellEndEdit> 이벤트는 셀이 편집 모드를 끝내는 경우에만 발생 하며 유효성 검사에 실패 하는 경우에는 수행할 수 없습니다.

    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#20)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#20)]

## <a name="testing-the-application"></a>애플리케이션 테스트

이제 폼을 테스트 하 여 예상 대로 동작 하는지 확인할 수 있습니다.

#### <a name="to-test-the-form"></a>폼을 테스트 하려면

- 애플리케이션을 컴파일하고 실행합니다.

  `Customers` 테이블의 데이터로 채워진 <xref:System.Windows.Forms.DataGridView> 표시 됩니다. `CompanyName` 열에서 셀을 두 번 클릭 하면 값을 편집할 수 있습니다. 모든 문자를 삭제 하 고 TAB 키를 눌러 셀을 종료 하면 <xref:System.Windows.Forms.DataGridView>를 종료 하지 못하게 됩니다. 셀에 비어 있지 않은 문자열을 입력 하면 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하 여 셀을 종료할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 응용 프로그램은 <xref:System.Windows.Forms.DataGridView> 컨트롤의 기능에 대 한 기본적인 이해를 제공 합니다. 여러 가지 방법으로 <xref:System.Windows.Forms.DataGridView> 컨트롤의 모양과 동작을 사용자 지정할 수 있습니다.

- 테두리 및 머리글 스타일을 변경 합니다. 자세한 내용은 [방법: 테두리 및 Windows Forms DataGridView 컨트롤의 모눈선 스타일 변경](change-the-border-and-gridline-styles-in-the-datagrid.md)합니다.

- 사용자 입력을 <xref:System.Windows.Forms.DataGridView> 컨트롤로 설정 하거나 제한 합니다. 자세한 내용은 [방법: Datagridview 컨트롤 Windows Forms에서 행 추가 및 삭제 방지](prevent-row-addition-and-deletion-datagridview.md)및 [방법: Windows Forms Datagridview 컨트롤에서 열을 읽기 전용으로 설정](how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)을 참조 하세요.

- 데이터베이스 관련 오류에 대 한 사용자 입력을 확인 합니다. 자세한 내용은 [연습: Windows Forms DataGridView 컨트롤에서 데이터 입력 중에 발생 하는 오류 처리](handling-errors-that-occur-during-data-entry-in-the-datagrid.md)를 참조 하세요.

- 가상 모드를 사용 하 여 매우 큰 데이터 집합을 처리 합니다. 자세한 내용은 [연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)을 참조 하세요.

- 셀의 모양을 사용자 지정 합니다. 자세한 내용은 [방법: Datagridview 컨트롤 Windows Forms에서 셀 모양 사용자 지정](customize-the-appearance-of-cells-in-the-datagrid.md) 및 [방법: Windows Forms Datagridview 컨트롤에서 글꼴 및 색 스타일 설정](how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)을 참조 하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [Windows Forms DataGridView 컨트롤의 데이터 입력](data-entry-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤의 데이터 유효성 검사](how-to-validate-data-in-the-windows-forms-datagridview-control.md)
- [연습: Windows Forms DataGridView 컨트롤에서 데이터 입력 중에 발생하는 오류 처리](handling-errors-that-occur-during-data-entry-in-the-datagrid.md)
- [연결 정보 보호](../../data/adonet/protecting-connection-information.md)
