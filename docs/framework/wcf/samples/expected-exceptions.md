---
title: 예상되는 예외
ms.date: 03/30/2017
ms.assetid: 299a6987-ae6b-43c6-987f-12b034b583ae
ms.openlocfilehash: f250e526b528adf0b67365ceb07f13e4087d773d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79144711"
---
# <a name="expected-exceptions"></a>예상되는 예외
이 샘플에서는 형식화된 클라이언트를 사용할 때 예상되는 예외를 catch하는 방법을 보여 줍니다. 이 샘플은 계산기 서비스를 구현하는 [시작 하기를](../../../../docs/framework/wcf/samples/getting-started-sample.md) 기반으로 합니다. 이 샘플에서 클라이언트는 콘솔 애플리케이션(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플에서는 올바른 프로그램에서 처리해야 하는 두 가지 예상되는 예외 형식 `TimeoutException` 및 `CommunicationException`을 catch하고 처리하는 방법을 보여 줍니다.  
  
 WCF(Windows 통신 Foundation) 클라이언트의 통신 메서드에서 throw된 예외는 예상되거나 예기치 않은 것입니다. 예기치 않은 예외에는 `OutOfMemoryException`과 같은 치명적인 실패와 `ArgumentNullException` 또는 `InvalidOperationException` 등의 프로그래밍 오류가 포함됩니다. 일반적으로 예기치 않은 오류를 처리하는 유용한 방법은 없으므로 일반적으로 WCF 클라이언트 통신 메서드를 호출할 때 오류를 catch해서는 안 됩니다.  
  
 WCF 클라이언트의 통신 메서드에서 예상되는 `TimeoutException` `CommunicationException`예외에는 의 파생 `CommunicationException`클래스가 포함됩니다. 이는 WCF 클라이언트를 중단하고 통신 오류를 보고하여 안전하게 처리할 수 있는 통신 중에 문제가 있음을 나타냅니다. 어느 애플리케이션에서나 외부 요소에 의해 이런 오류가 발생할 수 있기 때문에 올바른 애플리케이션에서는 이런 예외를 catch할 수 있어야 하며, 이런 예외가 발생한 경우 복구할 수 있어야 합니다.  
  
 클라이언트에서 throw할 수 있는 `CommunicationException`의 파생 클래스가 몇 가지 있습니다. 경우에 따라 애플리케이션에서 이 중 일부를 catch하여 특수 처리를 수행하고, 나머지는 `CommunicationException`으로 처리할 수도 있습니다. 보다 한정된 예외 형식을 먼저 catch한 다음 이후의 catch 절에서 `CommunicationException`을 catch하면 됩니다.  
  
 클라이언트 통신 메서드를 호출하는 코드는 `TimeoutException` 및 `CommunicationException`을 캐치해야 합니다. 그런 오류를 처리하는 방법 중 하나는 클라이언트를 중단하고 통신 오류를 보고하는 것입니다.  
  
```csharp
try  
{  
    ...  
    double result = client.Add(value1, value2);  
    ...  
    client.Close();  
}  
catch (TimeoutException exception)  
{  
    Console.WriteLine("Got {0}", exception.GetType());  
    client.Abort();  
}  
catch (CommunicationException exception)  
{  
    Console.WriteLine("Got {0}", exception.GetType());  
    client.Abort();  
}  
```  
  
 예상된 예외가 발생한 경우 이후에 클라이언트를 사용할 수 있거나 사용하지 못할 수 있습니다. 클라이언트를 여전히 사용할 수 있는지 확인하려면 `State` 속성이 `CommunicationState`.Opened인지 확인합니다. 아직 열려 있다면 여전히 사용 가능한 것입니다. 그렇지 않다면 클라이언트를 중단하고 이에 대한 참조를 모두 해제해야 합니다.  
  
> [!CAUTION]
> 예외가 발생한 후에 세션이 있는 클라이언트를 더 이상 사용하지 못하게 되는 경우가 많으며, 세션이 없는 클라이언트는 예외가 발생한 후에도 계속 사용 가능한 경우가 많습니다. 하지만 항상 적용되는 사항은 아니기 때문에 예외가 발생한 후에도 클라이언트를 계속 사용해 보려면 `State` 속성을 확인하여 클라이언트가 아직 열려 있는지 확인해야 합니다.  
  
 샘플을 실행하면 작업 응답 및 예외가 클라이언트 콘솔 창에 표시됩니다.  
  
 클라이언트 프로세스에서는 두 개의 시나리오를 실행하며, 각 시나리오에서는 `Add` 뒤에 `Divide`를 호출하려 합니다. 첫 번째 시나리오에서는 `Divide`에 대한 호출을 수행하기 전에 클라이언트를 중단하여 네트워크 문제를 시뮬레이션합니다. 두 번째 시나리오에서는 시간 제한을 메서드가 완료되기에 충분하지 않은 짧은 값으로 설정하여 시간 초과 조건을 발생시킵니다. 클라이언트 프로세스로부터의 예상 출력은 다음과 같습니다.  
  
```output
Add(100,15.99) = 115.99  
Simulated network problem occurs...  
Got System.ServiceModel.CommunicationObjectAbortedException  
Add(100,15.99) = 115.99  
Set timeout too short for method to complete...  
Got System.TimeoutException  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. Windows 통신 기초 [샘플에 대한 일회성 설치 절차를](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)수행했어야 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 또는 교차 컴퓨터 구성에서 샘플을 실행하려면 Windows [통신 기반 샘플 실행의 지침을 따르십시오.](../../../../docs/framework/wcf/samples/running-the-samples.md)  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대한 WCF(Windows 통신 재단) 및 WF(Windows 워크플로우 재단) 샘플로](https://www.microsoft.com/download/details.aspx?id=21459) 이동하여 모든 WCF(Windows 통신 재단) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\ExpectedExceptions`  
