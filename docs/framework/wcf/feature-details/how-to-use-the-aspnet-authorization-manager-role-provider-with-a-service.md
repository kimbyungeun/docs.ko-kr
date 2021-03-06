---
title: '방법: 서비스에서 ASP.NET 권한 부여 관리자 역할 공급자 사용'
ms.date: 03/30/2017
ms.assetid: f21deb81-91ef-49ef-94d6-494785143271
ms.openlocfilehash: 009b96defdf27591ddb98afaa684745b5fcbe0d4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184807"
---
# <a name="how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service"></a>방법: 서비스에서 ASP.NET 권한 부여 관리자 역할 공급자 사용
ASP.NET 웹 서비스를 호스팅하는 경우 권한 부여 관리자를 응용 프로그램에 통합하여 서비스에 대한 권한을 제공할 수 있습니다. 애플리케이션 개발자는 권한 부여 관리자를 사용하여 개별 작업을 정의할 수 있습니다. 개별 작업은 그룹으로 분류되어 작업을 형성할 수 있습니다. 관리자는 역할에 특정 작업 또는 개별 작업을 수행할 권한을 부여할 수 있습니다. 권한 부여 관리자는 역할, 작업 및 사용자를 관리할 수 있도록 MMC(Microsoft Management Console) 스냅인과 같은 관리 도구를 제공합니다. 관리자는 XML 파일, Active Directory 또는 ADAM(Active Directory Application Mode) 저장소에서 권한 부여 관리자 정책 저장소를 구성합니다.  
  
 권한 부여 관리자는 웹 서비스를 호스팅하는 ASP.NET 응용 프로그램에 대한 권한 부여 관리자 ASP.NET 역할 공급자를 구성하여 응용 프로그램에 통합됩니다. 다른 ASP.NET 역할 공급자와 마찬가지로 권한 부여 관리자 ASP.NET `providers` 역할 공급자는 <> 요소를 사용하여 구성됩니다.  
  
 다음 코드 예제는 권한 부여 관리자를 애플리케이션에 통합하는 웹 서비스에 대한 구성 파일의 일부입니다.  
  
```xml  
<system.web>  
    <roleManager enabled="true" defaultProvider="AzManRoleProvider">  
      <providers>  
        <add name="AzManRoleProvider"  
             type="System.Web.Security.AuthorizationStoreRoleProvider, System.Web, Version=2.0.0.0, Culture=neutral, publicKeyToken=b03f5f7f11d50a3a"  
             connectionStringName="AzManPolicyStoreConnectionString"
             applicationName="SecureService"/>  
      </providers>  
    </roleManager>  
</system.web>  
```  
  
 ASP.NET 역할 공급자를 WCF 응용 프로그램과 통합하는 방법에 대한 자세한 내용은 서비스 ASP.NET [역할 공급자 사용 방법을](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)참조하십시오. ASP.NET 사용 권한 부여 관리자를 사용하는 방법에 대한 자세한 내용은 [ASP.NET 2.0의 권한 부여 관리자(AzMan) 사용 방법을](https://docs.microsoft.com/previous-versions/msp-n-p/ff649313(v=pandp.10))참조하십시오.  
  
## <a name="see-also"></a>참고 항목

- [방법: 서비스에서 ASP.NET 역할 공급자 사용](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
