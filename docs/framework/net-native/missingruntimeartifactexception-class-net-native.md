---
title: MissingRuntimeArtifactException 클래스(.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: d5b3d13e-689f-4584-8ba6-44f5167a8590
ms.openlocfilehash: 7a69add45202b3ad838de592fadc82a84fa0ba5d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79180978"
---
# <a name="missingruntimeartifactexception-class-net-native"></a>MissingRuntimeArtifactException 클래스(.NET 네이티브)
**.NET 윈도우 용 애플 리 케이 션 에 대 한 10, .NET 네이티브만**  
  
 형식 또는 형식 멤버의 메타데이터를 사용할 수는 있지만 해당 구현이 제거된 경우 throw되는 예외입니다.  
  
 **네임스페이스:** System.Reflection  
  
> [!IMPORTANT]
> 이 `MissingRuntimeArtifactException` 클래스는 .NET 네이티브 도구 체인에서 내부적으로 사용하기 위한 것입니다. 이 클래스는 타사 코드에서 사용하면 안 되고 애플리케이션 코드에서 예외를 처리하면 안 됩니다. 대신, [런타임 지시문 파일](runtime-directives-rd-xml-configuration-file-reference.md)에 항목을 추가하여 예외를 제거합니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
## <a name="syntax"></a>구문  
 [!code-csharp[ProjectN#22](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingruntimeartifactexception_syntax1.cs#22)]  
  
 `MissingRuntimeArtifactException` 클래스가 <xref:System.MemberAccessException>에서 파생됩니다.  
  
 `MissingRuntimeArtifactException` 클래스의 멤버는 다음과 같습니다.  
  
## <a name="constructors"></a>생성자  
  
|생성자|Description|  
|-----------------|-----------------|  
|`public MissingRuntimeArtifactException()`|오류를 설명하는 시스템 제공 메시지를 사용하여 `MissingRuntimeArtifactException` 클래스의 새 인스턴스를 초기화합니다.<br /><br /> 이 생성자는 .NET 네이티브 도구 체인에서만 내부적으로 사용할 수 있습니다.|  
|`public MissingRuntimeArtifactException(String message)`|지정한 오류 메시지를 사용하여 `MissingRuntimeArtifactException` 클래스의 새 인스턴스를 초기화합니다.<br /><br /> 이 생성자는 .NET 네이티브 도구 체인에서만 내부적으로 사용할 수 있습니다.|  
  
## <a name="properties"></a>속성  
  
|속성|Description|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|예외에 대한 사용자 정의 정보를 추가로 제공하는 키/값 쌍 컬렉션을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string HelpLink { get; set; }`|이 예외와 연결된 도움말 파일에 대한 링크를 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public int HResult { get; protected set; }`|특정 예외에 할당되는 코딩된 숫자 값인 `HRESULT`를 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public Exception InnerException { get; }`|현재 예외를 발생시킨 예외를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string Message { get; }`|현재 예외를 설명하는 메시지를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string Source { get; set; }`|오류를 발생시킨 애플리케이션 또는 개체의 이름을 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string StackTrace { get; }`|호출 스택의 직접 실행 프레임 문자열 표현을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public MethodBase TargetSite { get; }`|현재 예외가 throw된 메서드를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
  
## <a name="methods"></a>메서드  
  
|방법|Description|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|지정된 개체가 현재 개체와 같은지 확인합니다.  <xref:System.Object>에서 상속됩니다.|  
|`protected void Finalize()`|가비지 컬렉션이 회수하기 전에 개체가 리소스를 해제하고 다른 정리 작업을 수행할 수 있게 합니다. <xref:System.Object>에서 상속됩니다.|  
|`public Exception GetBaseException()`|후속 예외 하나 이상의 근본 원인이 되는 예외를 반환합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public int GetHashCode()`|`MissingRuntimeArtifactException` 인스턴스의 해시 코드를 반환합니다.   <xref:System.Object>에서 상속됩니다.|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|예외에 대한 정보를 사용하여 <xref:System.Runtime.Serialization.SerializationInfo> 개체를 설정합니다.  <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public Type GetType()`|현재 인스턴스의 런타임 형식을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`protected Object MemberwiseClone()`|현재 개체의 부분 복사본을 만듭니다. <xref:System.Object>에서 상속됩니다.|  
|`public string ToString()`|현재 예외의 문자열 표현을 반환합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
  
## <a name="events"></a>이벤트  
  
|행사|Description|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|예외에 대한 serialize된 데이터가 들어 있는 예외 상태 개체가 만들어지도록 예외가 serialize될 때 발생합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
  
## <a name="usage-details"></a>사용량 세부 정보  
 형식 또는 멤버의 메타데이터는 있는데 해당 구현은 제거된 경우 형식을 인스턴스화하거나 형식 멤버를 호출하려고 하면 `MissingRuntimeArtifactException` 예외가 throw됩니다.  
  
 메타데이터와 메서드를 동적으로 실행하는 구현 코드는 런타임 지시문(XML 구성) 파일인 \*.rd.xml에 의해 정의됩니다. 앱에서 이 예외가 throw되지 않도록 하려면 형식 또는 형식 멤버에 필요한 메타데이터가 런타임에 제공되도록 \*.rd.xml을 수정해야 합니다. \*.rd.xml 파일의 형식에 대한 자세한 내용은 [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)를 확인하세요.  
  
> [!IMPORTANT]
> 이 예외는 애플리케이션에 필요한 구현 코드를 런타임에 사용할 수 없음을 나타내므로 `try`/`catch` 블록에서 이 예외를 처리하면 안 됩니다. 대신 예외의 원인을 진단하고 런타임 지시문 파일을 사용하여 예외를 방지해야 합니다. 일반적으로 런타임 지시문 파일(.rd.xml `Activate` `Dynamic` \*file)에서 프로그램 요소에 대한 적절한 또는 정책을 지정하여 이 예외를 제거합니다. 예외를 제거하는 런타임 지시문 파일에 추가할 수 있는 항목을 가져오려면 두 문제 해결사 중 하나를 사용할 수 있습니다.  
>
> - 형식의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/type.html) 입니다.  
> - 메서드의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/method.html) 입니다.  
  
 `MissingRuntimeArtifactException` 클래스는 고유한 멤버를 포함하지 않으며 모든 멤버는 <xref:System.MemberAccessException>에서 상속됩니다.  
  
## <a name="see-also"></a>참고 항목

- [Runtime Directives (rd.xml) Configuration File Reference](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
