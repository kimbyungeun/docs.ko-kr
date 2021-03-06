---
title: 인증서 클라이언트를 사용하는 메시지 보안
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 99770573-c815-4428-a38c-e4335c8bd7ce
ms.openlocfilehash: 3660877194931c2be5b9b1c9aa54e2595701697f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184653"
---
# <a name="message-security-with-a-certificate-client"></a>인증서 클라이언트를 사용하는 메시지 보안
다음 시나리오에서는 메시지 보안 모드를 사용하여 보안된 WCF(Windows 통신 재단) 클라이언트 및 서비스를 보여 주며, 클라이언트 및 서비스는 인증서를 사용하여 인증됩니다. 자세한 내용은 [분산 응용 프로그램 보안](../../../../docs/framework/wcf/feature-details/distributed-application-security.md)을 참조하십시오.

 ![인증서가 있는 클라이언트를 보여 주는 스크린샷입니다.](./media/message-security-with-a-certificate-client/client-with-certificate.gif)  
  
 샘플 응용 프로그램에 대 한 [메시지 보안 인증서를](../../../../docs/framework/wcf/samples/message-security-certificate.md)참조 하십시오.  

|특성|Description|  
|--------------------|-----------------|  
|보안 모드|메시지|  
|상호 운용성|WCF 전용|  
|인증(서버)|서비스 인증서 사용|  
|인증(클라이언트)|클라이언트 인증서 사용|  
|무결성|yes|  
|기밀성|yes|  
|전송|HTTP|  
|바인딩|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a>서비스  
 다음 코드와 구성은 독립적으로 실행되어야 합니다. 다음 중 하나를 수행합니다.  
  
- 구성 없이 코드를 사용하여 독립 실행형 서비스를 만듭니다.  
  
- 제공된 구성을 사용하여 서비스를 만들지만 엔드포인트를 정의하지 않습니다.  
  
### <a name="code"></a>코드  
 다음 코드에서는 안전한 컨텍스트를 설정하기 위해 메시지 보안을 사용하는 서비스 엔드포인트를 만드는 방법을 보여 줍니다.  
  
 [!code-csharp[C_SecurityScenarios#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#10)]
 [!code-vb[C_SecurityScenarios#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#10)]  
  
### <a name="configuration"></a>구성  
 코드 대신 다음 구성을 사용할 수 있습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="ServiceCredentialsBehavior">  
          <serviceCredentials>  
            <serviceCertificate findValue="Contoso.com"  
                                x509FindType="FindBySubjectName" />  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service behaviorConfiguration="ServiceCredentialsBehavior"
               name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"
                  binding="wsHttpBinding"  
                  bindingConfiguration="MessageAndCertificateClient"
                  name="SecuredByClientCertificate"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator">  
          <security mode="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>Client  
 다음 코드와 구성은 독립적으로 실행되어야 합니다. 다음 중 하나를 수행합니다.  
  
- 이 코드와 클라이언트 코드를 사용하여 독립 실행형 클라이언트를 만듭니다.  
  
- 엔드포인트 주소를 정의하지 않는 클라이언트를 만듭니다. 대신 구성 이름을 인수로 사용하는 클라이언트 생성자를 사용합니다. 다음은 그 예입니다.  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>코드  
 다음 코드에서는 클라이언트를 만듭니다. 바인딩은 메시지 모드 보안으로 설정되며 클라이언트 자격 증명 형식은 `Certificate`로 설정됩니다.  
  
 [!code-csharp[C_SecurityScenarios#17](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#17)]
 [!code-vb[C_SecurityScenarios#17](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#17)]  
  
### <a name="configuration"></a>구성  
 다음 구성에서는 엔드포인트 동작을 사용하는 클라이언트 인증서를 지정합니다. 자세한 내용은 [인증서 작업](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)을 참조하세요. 또한 코드는 <`identity`> 요소를 사용하여 예상되는 서버 ID의 DNS(도메인 이름 시스템)를 지정합니다. ID에 대한 자세한 내용은 [서비스 ID 및 인증을](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)참조하십시오.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="endpointCredentialsBehavior">  
          <clientCredentials>  
            <clientCertificate findValue="Cohowinery.com"
               storeLocation="LocalMachine"  
              x509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="http://machineName/Calculator"
                behaviorConfiguration="endpointCredentialsBehavior"  
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"  
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator">  
        <identity>  
          <dns value="Contoso.com" />  
        </identity>  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목

- [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [서비스 ID 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [Working with Certificates](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [Windows Server AppFabric 보안 모델](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
