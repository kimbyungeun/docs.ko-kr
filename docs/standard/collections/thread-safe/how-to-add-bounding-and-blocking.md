---
title: '방법: 컬렉션에 한계 지정 및 차단 기능 추가'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- thread-safe collections, custom blocking collections
ms.assetid: 4c2492de-3876-4873-b5a1-000bb404d770
ms.openlocfilehash: 33c0b5a93a9c63e3e743a04e69bb7353ac69fa8a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2020
ms.locfileid: "75711287"
---
# <a name="how-to-add-bounding-and-blocking-functionality-to-a-collection"></a>방법: 컬렉션에 한계 지정 및 차단 기능 추가
이 예제에서는 클래스에서 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=nameWithType> 인터페이스를 구현한 다음, 클래스 인스턴스를 <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType>의 내부 스토리지 메커니즘으로 사용하여 사용자 지정 컬렉션 클래스에 한계 지정 및 차단 기능을 추가하는 방법을 보여 줍니다. 한계 지정 및 차단에 대한 자세한 내용은 [BlockingCollection 개요](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)를 참조하십시오.  
  
## <a name="example"></a>예제  
 사용자 지정 컬렉션 클래스는 우선 순위 수준이 <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>개 개체의 배열로 표시되는 기본 우선 순위 큐입니다. 각 큐 내에서 추가로 정렬이 수행되지는 않습니다.  
  
 클라이언트 코드에서 다음 세 가지 작업이 시작됩니다. 첫 번째 작업은 실행 중 언제든지 취소할 수 있도록 키보드 스트로크를 폴링합니다. 두 번째 작업은 공급자 스레드입니다. 이 작업에서는 새 항목을 차단 컬렉션에 추가하고 임의 값에 기반하여 각 항목에 우선 순위를 부여합니다. 세 번째 작업은 컬렉션에서 제공되는 대로 항목을 제거합니다.  
  
 이러한 스레드 중 하나가 다른 스레드보다 빠르게 실행되도록 함으로써 애플리케이션의 동작을 조정할 수 있습니다. 공급자가 더 빠르게 실행되는 경우 차단 컬렉션에 포함된 항목이 생성자에 지정한 항목 개수에 이미 도달되었으면 한계 지정 기능으로 인해 항목이 차단 컬렉션에 추가되지 않습니다. 소비자가 더 빠르게 실행되는 경우 차단 기능으로 인해 새 항목이 추가될 때까지 소비자가 기다리게 됩니다.  
  
 [!code-csharp[CDS_BlockingCollection#06](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/prodcon.cs#06)]  
  
 기본적으로 <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType>의 스토리지는 <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>입니다.  
  
## <a name="see-also"></a>참고 항목

- [스레드로부터 안전한 컬렉션](../../../../docs/standard/collections/thread-safe/index.md)
