---
title: 시작 화면을 추가 하는 방법
ms.date: 08/18/2018
helpviewer_keywords:
- WPF [WPF], splash screen
- startup window [WPF]
- SplashScreen class [WPF]
- splash screen [WPF]
ms.assetid: d70a25c4-5fb9-4c27-b01d-b1b8ef39b3fd
ms.openlocfilehash: 39f53e21c40f036c65894b4f275cd5fb414999be
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76740456"
---
# <a name="how-to-add-a-splash-screen-to-a-wpf-application"></a>방법: WPF 애플리케이션에 시작 화면 추가

이 항목에서는 시작 창 또는 *시작 화면*을 WINDOWS PRESENTATION FOUNDATION (WPF) 응용 프로그램에 추가 하는 방법을 보여 줍니다.

## <a name="to-add-an-existing-image-as-a-splash-screen"></a>기존 이미지를 시작 화면으로 추가하려면

1. 시작 화면으로 사용하려는 이미지를 찾거나 만듭니다. Windows Imaging 구성 요소(WIC)에서 지원되는 모든 이미지 형식을 사용할 수 있습니다. 예를 들어, BMP, GIF, JPEG, PNG 또는 TIFF 형식으로 사용할 수 있습니다.

2. WPF 응용 프로그램 프로젝트에 해당 이미지 파일을 추가합니다.

3. **솔루션 탐색기**에서 이미지를 선택 합니다.

4. 속성 창에서 **빌드 작업** 속성의 드롭다운 화살표를 클릭 합니다.

5. 드롭다운 목록에서 **SplashScreen** 를 선택 합니다.

6. **F5** 키를 눌러 애플리케이션을 빌드하고 실행합니다.

     시작 화면 이미지가 화면 중앙에 나타난 다음 메인 응용 프로그램 창이 나타나면 사라집니다.

## <a name="to-exclude-the-splash-screen-from-build"></a>빌드에서 시작 화면을 제외하려면

1. **솔루션 탐색기**에서 시작 화면 이미지를 선택 합니다.

2. **속성** 창에서 **빌드 작업** 을 **없음**으로 설정 합니다.

## <a name="to-remove-the-splash-screen-from-an-application"></a>응용 프로그램에서 시작 화면을 제거 하려면

**솔루션 탐색기**에서 시작 화면 이미지를 삭제 합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.SplashScreen>
- [방법: 프로젝트에 기존 항목 추가](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/9f4t9t92(v=vs.100))
