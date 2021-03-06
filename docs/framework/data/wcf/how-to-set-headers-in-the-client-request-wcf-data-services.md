---
title: '방법: 클라이언트 요청의 헤더 설정(WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing requests
ms.assetid: 3d55168d-5901-4f48-8117-6c93da3ab5ae
ms.openlocfilehash: 9267f0e5b68823516764891a40e1435c1325b77f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174344"
---
# <a name="how-to-set-headers-in-the-client-request-wcf-data-services"></a>방법: 클라이언트 요청의 헤더 설정(WCF Data Services)
WCF 데이터 서비스 클라이언트 라이브러리를 사용하여 OData(개방형 데이터 프로토콜)를 지원하는 데이터 서비스에 액세스하면 클라이언트 라이브러리는 데이터 서비스로 전송되는 요청 메시지에 필요한 HTTP 헤더를 자동으로 설정합니다. 하지만 클라이언트 라이브러리는 데이터 서비스에 청구 기반 인증이나 쿠키가 필요한 경우와 같은 특정 상황에서 필요한 메시지 헤더를 설정하지 못합니다. 자세한 내용은 [Securing WCF Data Services](securing-wcf-data-services.md#clientAuthentication)을 참조하세요. 이런 경우에는 전송하기 전에 요청 메시지의 메시지 헤더를 수동으로 설정해야 합니다. 이 항목의 예제에서는 데이터 서비스로 전송하기 전에 요청 메시지에 새로운 헤더를 추가하도록 <xref:System.Data.Services.Client.DataServiceContext.SendingRequest> 이벤트를 처리하는 방법을 설명합니다.  
  
 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스와 클라이언트 데이터 클래스는 [WCF 데이터](quickstart-wcf-data-services.md)서비스 빠른 시작을 완료할 때 만들어집니다. OData 웹 사이트에 게시된 [Northwind 샘플 데이터 서비스를](https://services.odata.org/Northwind/Northwind.svc/) 사용할 수도 있습니다. 이 샘플 데이터 서비스는 읽기 전용이며 변경 내용을 저장하려고 하면 오류가 반환됩니다. OData 웹 사이트의 샘플 데이터 서비스는 익명 인증을 허용합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Data.Services.Client.DataServiceContext.SendingRequest>이벤트에 대한 처리기를 등록한 다음 데이터 서비스에 대해 쿼리를 실행합니다.  
  
> [!NOTE]
> 데이터 서비스에서 모든 요청의 메시지 헤더를 수동으로 설정하도록 요구하는 경우 데이터 서비스를 나타내는 엔터티 컨테이너(이 경우에는 <xref:System.Data.Services.Client.DataServiceContext.SendingRequest>)에서 `OnContextCreated` 부분 메서드를 재정의하여 `NorthwindEntities` 이벤트 처리기를 등록하는 것이 좋습니다.  
  
[!code-csharp[Astoria Northwind Client#RegisterHeadersQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#registerheadersquery)]
[!code-vb[Astoria Northwind Client#RegisterHeadersQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#registerheadersquery)]
  
## <a name="example"></a>예제  
 다음 메서드가 <xref:System.Data.Services.Client.DataServiceContext.SendingRequest> 이벤트를 처리하고 인증 헤더를 요청에 추가합니다.  
  
 [!code-csharp[Astoria Northwind Client#OnSendingRequest](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#onsendingrequest)]  
 [!code-vb[Astoria Northwind Client#OnSendingRequest](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#onsendingrequest)]  
  
## <a name="see-also"></a>참고 항목

- [WCF Data Services 보안](securing-wcf-data-services.md)
- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
