---
title: 본문에 의한 경로
ms.date: 03/30/2017
ms.assetid: 07a6fc3b-c360-42e0-b663-3d0f22cf4502
ms.openlocfilehash: c3f4b19e646a6a9716d2264a3969b339208c60a1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79144190"
---
# <a name="route-by-body"></a>본문에 의한 경로
이 샘플에서는 SOAP 작업이 있는 메시지 개체를 수락하는 서비스를 구현하는 방법을 보여 줍니다. 이 샘플은 계산기 서비스를 구현하는 [시작 하기를](../../../../docs/framework/wcf/samples/getting-started-sample.md) 기반으로 합니다. 서비스는 `Calculate` 요청 매개 변수를 받아 <xref:System.ServiceModel.Channels.Message> 응답을 반환하는 단일 <xref:System.ServiceModel.Channels.Message> 작업을 구현합니다.  
  
 이 샘플에서 클라이언트는 콘솔 애플리케이션(.exe)이고 서비스는 IIS에서 호스팅됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플에서는 본문 콘텐츠에 기반한 메시지 디스패치를 보여 줍니다. 기본 제공 WCF(Windows 통신 재단) 서비스 모델 메시지 디스패치 메커니즘은 메시지 작업을 기반으로 합니다. 반면 모든 작업을 Action=""으로 정의하는 기존 웹 서비스도 많습니다. 동작 정보를 기준으로 계속 요청 메시지를 디스패치하는 WSDL을 기반으로 하여 서비스를 빌드할 수 없습니다. 이 샘플에서는 WSDL을 기반으로 하는 서비스 계약을 보여 줍니다. WSDL은 샘플에 포함된 Service.wsdl에 있습니다. 서비스 계약은 [시작에](../../../../docs/framework/wcf/samples/getting-started-sample.md)사용되는 것과 유사한 계산기입니다. 하지만 `[OperationContract]`는 모든 작업에 대해 `Action=""`을 지정합니다.  
  
```csharp  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples"),
                 XmlSerializerFormat, DispatchByBodyBehavior]  
    public interface ICalculator  
    {  
        [OperationContract(Action="")]  
        double Add(double n1, double n2);  
        [OperationContract(Action = "")]  
        double Subtract(double n1, double n2);  
        [OperationContract(Action = "")]  
        double Multiply(double n1, double n2);  
        [OperationContract(Action = "")]  
        double Divide(double n1, double n2);  
    }  
```  
  
 계약이 지정되면 서비스에서는 작업 사이에서 메시지를 디스패치할 수 있도록 사용자 지정 디스패치 동작 `DispatchByBodyBehavior`를 요청합니다. 이 디스패치 동작은 `DispatchByBodyElementOperationSelector` 각 래퍼 요소의 QName으로 키를 지정한 작업 이름 테이블을 통해 사용자 지정 작업 선택기의 초기화를 수행합니다. `DispatchByBodyElementOperationSelector`는 본문의 첫 번째 자식에 대한 시작 태그를 살펴보고 이전에 설명한 테이블을 사용하여 작업을 선택합니다.  
  
 클라이언트는 [ServiceModel 메타데이터 유틸리티 도구(Svcutil.exe)를](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)사용하여 서비스에서 내보낸 WSDL에서 자동으로 생성된 프록시를 사용합니다.  
  
```console  
svcutil.exe  /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples /uxs http://localhost/servicemodelsamples/service.svc?wsdl /out:generatedProxy.cs  
```  
  
 모든 작업의 동작이 비어 있어도 자동 생성된 프록시의 동작 매개 변수를 제외하고는 클라이언트 코드에 영향을 주지 않습니다.  
  
 클라이언트 코드는 몇 가지 계산을 수행합니다. 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console
Add(100, 15.99) = 115.99  
Subtract(145, 76.54) = 68.46  
Multiply(9, 81.25) = 731.25  
Divide(22, 7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. Windows 통신 기초 [샘플에 대한 일회성 설치 절차를](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)수행했어야 합니다.  
  
2. 솔루션을 빌드하려면 Windows 통신 [기초 샘플 빌드의 지침을 따르십시오.](../../../../docs/framework/wcf/samples/building-the-samples.md)  
  
3. 단일 또는 교차 컴퓨터 구성에서 샘플을 실행하려면 Windows [통신 기반 샘플 실행의 지침을 따르십시오.](../../../../docs/framework/wcf/samples/running-the-samples.md)  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대한 WCF(Windows 통신 재단) 및 WF(Windows 워크플로우 재단) 샘플로](https://www.microsoft.com/download/details.aspx?id=21459) 이동하여 모든 WCF(Windows 통신 재단) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Interop\RouteByBody`  
