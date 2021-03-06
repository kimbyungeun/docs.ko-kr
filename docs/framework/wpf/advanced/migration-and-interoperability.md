---
title: 마이그레이션 및 상호 운용성
ms.date: 03/23/2020
f1_keywords:
- AutoGeneratedOrientationPage
helpviewer_keywords:
- Windows Presentation Foundation [WPF], interoperability
- WPF [WPF], migration
- Windows Forms controls [WPF interoperability]
- controls [WPF interoperability]
- Windows Presentation Foundation [WPF], migration
- interoperability [WPF]
- WPF [WPF], interoperability
- migration [WPF]
ms.assetid: d655de05-bf63-4814-bc64-6b3be01c70a2
ms.openlocfilehash: 180ece4f178406c6c3e704ecadaa9a72955ec038
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2020
ms.locfileid: "80249053"
---
# <a name="migration-and-interoperability"></a>마이그레이션 및 상호 운용성

이 페이지에는 응용 프로그램과 다른 유형의 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] Microsoft Windows 응용 프로그램 간의 상호 작업을 구현하는 방법을 설명하는 문서에 대한 링크가 포함되어 있습니다.

## <a name="in-this-section"></a>섹션 내용

[WPF에서 System.Xaml로 마이그레이션된 형식](types-migrated-from-wpf-to-system.md)\
[WPF 및 Windows 양식 상호 운용](wpf-and-windows-forms-interoperation.md)\
[WPF 및 Win32 상호 운용](wpf-and-win32-interoperation.md)\
[WPF 및 Direct3D9 상호 운용성](wpf-and-direct3d9-interoperation.md)

## <a name="reference"></a>참고

| 용어                                                     | 정의                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <xref:System.Windows.Forms.Integration.WindowsFormsHost> | [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 페이지 의 요소로 Windows Forms 컨트롤을 호스트 하는 데 사용할 수 있는 요소입니다.                                                                                                                                                                                                                                      |
| <xref:System.Windows.Forms.Integration.ElementHost>      | [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 컨트롤을 호스트하는 데 사용할 수 있는 Windows Forms 컨트롤입니다.                                                                                                                                                                                                                                                                 |
| <xref:System.Windows.Interop.HwndSource>                 | Win32 응용 프로그램 내에서 리전을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스트합니다.                                                                                                                                                                                                                                                                                |
| <xref:System.Windows.Interop.HwndHost>                   | 에 대한 <xref:System.Windows.Forms.Integration.WindowsFormsHost>기본 클래스는 응용 프로그램에서 호스팅할 때 모든 HWND 기반 기술이 사용하는 몇 가지 기본 기능을 정의합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램 내에서 Win32 창을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스트하려면 이 하위 클래스입니다. |
| <xref:System.Windows.Interop.BrowserInteropHelper>       | 브라우저에서 호스트하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에 대한 브라우저 환경의 조건을 보고하기 위한 도우미 클래스입니다.                                                                                                                                                                                                         |

## <a name="related-sections"></a>관련 섹션
