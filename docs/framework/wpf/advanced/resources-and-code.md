---
title: 리소스 및 코드
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keys [WPF], using objects as
- resources [WPF], accessing from procedural code
- procedural code [WPF], creating resources with
- procedural code [WPF], accessing resources from
- resources [WPF], creating with procedural code
ms.assetid: c1cfcddb-e39c-41c8-a7f3-60984914dfae
ms.openlocfilehash: 8074562ddb865b482cf123743796ac68bb529f85
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646236"
---
# <a name="resources-and-code"></a>리소스 및 코드
이 개요에서는 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 구문이 아닌 코드를 사용하여 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 리소스를 만들거나 리소스에 액세스하는 방법을 중점적으로 설명합니다. 일반적인 리소스 사용 및 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 구문 측면에서 본 리소스에 대한 자세한 내용은 [XAML 리소스](../../../desktop-wpf/fundamentals/xaml-resources-define.md)를 참조하세요.  

<a name="accessing"></a>
## <a name="accessing-resources-from-code"></a>코드에서 리소스 액세스  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]를 통해 정의된 리소스를 식별하는 키는 코드에서 리소스를 요청할 경우 특정 리소스를 검색하는 데도 사용됩니다. 코드에서 리소스를 검색하는 가장 간단한 방법은 <xref:System.Windows.FrameworkElement.FindResource%2A> 응용 <xref:System.Windows.FrameworkElement.TryFindResource%2A> 프로그램의 프레임워크 수준 개체에서 또는 메서드를 호출하는 것입니다. 이러한 메서드 간의 동작 차이는 요청된 키를 찾을 수 없는 경우에 발생합니다. <xref:System.Windows.FrameworkElement.FindResource%2A>예외를 제기합니다. <xref:System.Windows.FrameworkElement.TryFindResource%2A> 예외를 발생시키지 않지만 `null`반환합니다. 각 메서드는 리소스 키를 입력 매개 변수로 사용하고 느슨하게 형식화된 개체를 반환합니다. 일반적으로 리소스 키는 문자열이지만 문자열이 아닌 리소스 키가 사용되기도 합니다. 자세한 내용은 [개체를 키로 사용](#objectaskey) 섹션을 참조하세요. 일반적으로 반환된 개체는 리소스를 요청할 때 설정할 속성에 필요한 형식으로 캐스트합니다. 코드 리소스 확인에 대한 조회 논리는 동작 리소스 참조 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사례와 같습니다. 리소스 검색은 호출 요소에서 시작되고 논리 트리의 다음 부모 요소로 계속됩니다. 조회는 애플리케이션 리소스, 테마 및 시스템 리소스(필요한 경우)로 계속 진행됩니다. 리소스에 대한 코드 요청은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 로드되는 리소스 사전 다음에 만들어졌을 수 있는 리소스 사전의 런타임 변경 내용 및 실시간 시스템 리소스 변경 내용을 제대로 처리합니다.  
  
 다음은 키별로 리소스를 찾아 반환된 값을 사용하여 이벤트 처리기로 구현된 속성을 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 설정하는 간단한 코드 예제입니다.  
  
 [!code-csharp[PropertiesOvwSupport#ResourceProceduralGet](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml.cs#resourceproceduralget)]
 [!code-vb[PropertiesOvwSupport#ResourceProceduralGet](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page3.xaml.vb#resourceproceduralget)]  
  
 리소스 참조를 할당하는 다른 <xref:System.Windows.FrameworkElement.SetResourceReference%2A>방법은 은입니다. 이 메서드가 사용하는 두 개의 매개 변수는 리소스 키 및 리소스 값을 할당해야 하는 요소 인스턴스에 있는 특정 종속성 속성의 식별자입니다. 기능적으로 이 메서드는 동일하고 반환 값을 캐스트할 필요가 없는 장점이 있습니다.  
  
 프로그래밍 방식으로 리소스에 액세스하는 또 다른 방법은 <xref:System.Windows.FrameworkElement.Resources%2A> 사전으로 속성의 내용에 액세스하는 것입니다. 이 속성에 포함된 사전에 액세스하면 새 리소스를 기존 컬렉션에 추가하고, 특정 키 이름이 이미 컬렉션에 사용되는지 확인하는 작업과 같은 사전/컬렉션 작업을 수행할 수 있습니다. 코드에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 완전히 작성하는 경우 코드에서 전체 컬렉션을 만들고 키를 할당한 다음 완료된 컬렉션을 <xref:System.Windows.FrameworkElement.Resources%2A> 설정된 요소의 속성에 할당할 수도 있습니다. 이 내용은 다음 섹션에서 설명합니다.  
  
 특정 키를 인덱스로 사용하여 지정된 <xref:System.Windows.FrameworkElement.Resources%2A> 컬렉션 내에서 인덱싱할 수 있지만 이러한 방식으로 리소스에 액세스하는 것은 리소스 확인의 일반적인 런타임 규칙을 따르지 않는다는 점에 유의해야 합니다. 해당 특정 컬렉션에만 액세스하게 됩니다. 리소스 조회는 요청된 키에서 유효한 개체를 찾을 수 없는 경우 애플리케이션 또는 루트 범위를 통과하지 않습니다. 하지만 키 검색 범위가 더 제한되므로 정확히 말하자면 어떤 경우에는 이 방법에 성능상 장점이 있을 수 있습니다. 리소스 <xref:System.Windows.ResourceDictionary> 사전을 직접 사용하여 작업하는 방법에 대한 자세한 내용은 클래스를 참조하십시오.  
  
<a name="creating"></a>
## <a name="creating-resources-with-code"></a>코드를 사용하여 리소스 만들기  
 코드에서 전체 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션을 만들려면 코드에서 해당 애플리케이션의 모든 리소스를 만들어야 할 수도 있습니다. 이를 위해 새 <xref:System.Windows.ResourceDictionary> 인스턴스를 만든 다음 에 대한 연속 호출을 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType>사용하여 사전에 모든 리소스를 추가합니다. 그런 다음 <xref:System.Windows.ResourceDictionary> 이렇게 만든 을 <xref:System.Windows.FrameworkElement.Resources%2A> 사용하여 페이지 범위에 있는 요소 또는 에 <xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType>있는 속성에 속성을 설정합니다. 요소에 추가하지 <xref:System.Windows.ResourceDictionary> 않고 독립 실행형 개체로 유지할 수도 있습니다. 하지만 이 작업을 수행할 경우 제네릭 사전인 것처럼 항목 키를 사용하여 인스턴스 내의 리소스에 액세스해야 합니다. 요소 <xref:System.Windows.ResourceDictionary> `Resources` 속성에 연결되지 않은 A는 요소 트리의 일부로 존재하지 않으며 관련 <xref:System.Windows.FrameworkElement.FindResource%2A> 메서드에서 사용할 수 있는 조회 시퀀스에 대한 범위가 없습니다.  
  
<a name="objectaskey"></a>
## <a name="using-objects-as-keys"></a>개체를 키로 사용  
 대부분의 리소스 사용에서는 리소스 키를 문자열로 설정합니다. 하지만 다양한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기능은 키를 지정하는 데 의도적으로 문자열 형식을 사용하지 않습니다. 대신에 이 매개 변수는 개체입니다. 리소스에 개체로 키를 지정하는 기능은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 스타일 및 테마 지정 지원에서 사용됩니다. 스타일이 아닌 <xref:System.Type> 컨트롤의 기본 스타일이 되는 테마의 스타일은 각각 적용해야 하는 컨트롤의 키에 의해 키로 설정됩니다. 형식으로 키가 지정되는 방법은 각 컨트롤 형식의 기본 인스턴스에 적용되는 안정적인 조회 메커니즘이고, 형식은 리플렉션을 통해 검색되고 파생 형식에 기본 스타일이 없더라도 파생 클래스의 스타일을 지정하는 데 사용될 수 있습니다. <xref:System.Type> [x:Type 마크업 확장](../../../desktop-wpf/xaml-services/xtype-markup-extension.md)을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사용하여 정의된 리소스에 대한 키를 지정할 수 있습니다. [ComponentResourceKey 태그 확장](componentresourcekey-markup-extension.md)과 같은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기능을 지원하는 기타 문자열이 아닌 키 사용에 대한 비슷한 확장이 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [XAML 리소스](../../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [스타일 지정 및 템플릿](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
