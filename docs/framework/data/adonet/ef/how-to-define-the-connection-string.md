---
title: '방법: 연결 문자열 정의'
ms.date: 03/30/2017
ms.assetid: 6027335d-4e26-420d-9151-6523289b1989
ms.openlocfilehash: e5b675a50f883825cce97275048447b79b64cc97
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150573"
---
# <a name="how-to-define-the-connection-string"></a>방법: 연결 문자열 정의

이 항목에서는 개념적 모델에 연결할 때 사용하는 연결 문자열을 정의하는 방법을 설명합니다. 이 항목은 [어드벤처웍스 세일즈](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb387147(v=vs.100)) 컨셉 모델을 기반으로 합니다. AdventureWorks 영업 모델은 엔터티 프레임워크 설명서의 작업 관련 항목 전체에서 사용됩니다. 이 항목에서는 엔터티 프레임워크를 이미 구성하고 AdventureWorks 영업 모델을 정의했다고 가정합니다. 자세한 내용은 [방법: 모델 및 매핑 파일 수동으로 정의](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399785(v=vs.100))하는 방법을 참조 하십시오. 이 항목의 절차는 [엔터티 프레임워크 프로젝트를 수동으로 구성하는 방법에도](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))포함되어 있습니다.

> [!NOTE]
> Visual Studio 프로젝트에서 엔터티 데이터 모델 마법사를 사용하는 경우 .edmx 파일이 자동으로 생성되고 엔터티 프레임워크를 사용하도록 프로젝트를 구성합니다. 자세한 내용은 [엔터티 데이터 모델 마법사를 사용하는 방법을](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))참조하십시오.

## <a name="to-define-the-entity-framework-connection-string"></a>Entity Framework 연결 문자열을 정의하려면

- 프로젝트의 애플리케이션 구성 파일(app.config)을 열고 다음 연결 문자열을 추가합니다.

```xml
<connectionStrings>
    <add name="AdventureWorksEntities"
         connectionString="metadata=.\AdventureWorks.csdl|.\AdventureWorks.ssdl|.\AdventureWorks.msl;
         provider=System.Data.SqlClient;provider connection string='Data Source=localhost;
         Initial Catalog=AdventureWorks;Integrated Security=True;Connection Timeout=60;
         multipleactiveresultsets=true'" providerName="System.Data.EntityClient" />
</connectionStrings>
```

프로젝트에 응용 프로그램 구성 파일이 없는 경우 **프로젝트** 메뉴에서 **새 항목 추가를** 선택하고 **일반** 범주를 선택한 다음 응용 프로그램 **구성 파일**을 선택한 다음 **추가를**클릭하여 추가할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [퀵 스타트](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399182(v=vs.100))
- [방법: 새 .edmx 파일 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716703(v=vs.100))
- [ADO.NET 엔터티 데이터 모델 도구](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
