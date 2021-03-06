---
title: NameValueSectionHandler 및 DictionarySectionHandler에 대 한 <clear> 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: ff2294ec-fb82-4b0c-933e-ae185433fc7b
ms.openlocfilehash: f6d860f35d22002030ffa3d09dd0d8a96116bf5e
ms.sourcegitcommit: 9c54866bcbdc49dbb981dd55be9bbd0443837aa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77214749"
---
# <a name="clear-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>NameValueSectionHandler 및 DictionarySectionHandler에 대 한 \<clear > 요소

섹션에서 이전에 정의 된 모든 설정을 지웁니다.

[ **\<configuration>** ](configuration-element.md)\
&nbsp;&nbsp;[ **\<섹션 이름 >** ](custom-element-2.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<clear >**

## <a name="syntax"></a>구문

```xml
<clear />
```

## <a name="attributes"></a>특성

None

## <a name="parent-element"></a>부모 요소

|     | Description |
| --- | ------------|
| [ **\<섹션 이름 >** 요소인](custom-element-2.md) | <xref:System.Configuration.NameValueSectionHandler> 및 <xref:System.Configuration.DictionarySectionHandler> 클래스를 사용 하는 사용자 지정 구성 섹션에 대 한 설정을 정의 합니다. |

## <a name="child-elements"></a>자식 요소

None

## <a name="remarks"></a>설명

**\<clear >** 요소를 사용 하 여 구성 파일 계층 구조에서 상위 수준에 정의 된 응용 프로그램의 모든 설정을 제거할 수 있습니다.

## <a name="example"></a>예제

이 예제에서는 컴퓨터 구성 파일 및 응용 프로그램 구성 파일을 정의 하 고, 응용 프로그램 구성 파일에서 **\<clear >** 요소를 사용 하 여 이전에 컴퓨터 구성 파일에 정의 된 섹션을 지우는 방법을 보여 줍니다.

다음 컴퓨터 구성 파일 코드는 **\<mysection >** 섹션을 선언 합니다.

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="mySection" type="System.Configuration.NameValueSectionHandler,System" />
  </configSections>
  <mySection>
    <add key="key1" value="value1" />
    <add key="key2" value="value2" />
  </mySection>
</configuration>
```

다음 응용 프로그램 구성 파일 코드는 **\<mySection >** 에서 모든 설정을 제거 합니다. 응용 프로그램은 컴퓨터 구성 파일의 **\<mysection >** 섹션에서에 선언 된 설정을 검색할 수 없습니다.

```xml
<!-- Application configuration file -->
<configuration>
  <mySection>
    <clear/>
  </mySection>
</configuration>
```

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일 *, 컴퓨터 구성 파일 (machine.config*) 및 응용 프로그램 디렉터리 수준에 없는 *web.config 파일* 에서 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [.NET Framework에 대 한 구성 파일 스키마](index.md)
