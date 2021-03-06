---
title: Service Trace Viewer 도구(SvcTraceViewer.exe)
ms.date: 03/30/2017
ms.assetid: 9027efd3-df8d-47ed-8bcd-f53d55ed803c
ms.openlocfilehash: 543b0e714343cdb8078861ceb31e4f8035e20afd
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72321207"
---
# <a name="service-trace-viewer-tool-svctraceviewerexe"></a>Service Trace Viewer 도구(SvcTraceViewer.exe)

Wcf (Windows Communication Foundation) 서비스 추적 뷰어 도구를 사용 하면 WCF에 의해 생성 된 진단 추적을 분석할 수 있습니다. Service Trace Viewer는 WCF 서비스 문제를 진단, 복구 및 확인할 수 있도록 로그에서 추적 메시지를 쉽게 병합 하 고, 보고, 필터링 하는 방법을 제공 합니다.

## <a name="configuring-tracing"></a>추적 구성

진단 추적은 애플리케이션을 실행하는 동안 발생하는 상황을 보여 주는 정보를 제공합니다. 이름에서 알 수 있듯이 소스에서 대상까지의 작업뿐 아니라 중간 지점의 작업도 추적할 수 있습니다.

응용 프로그램의 구성 파일 (웹 호스팅 응용 프로그램용 web.config 또는 자체 호스팅 응용 프로그램의 경우 *Appname*)을 사용 하 여 추적을 구성할 수 있습니다. 예를 들면 다음과 같습니다.

```xml
<system.diagnostics>
    <trace autoflush="true" />
    <sources>
            <source name="System.ServiceModel"
                    switchValue="Information, ActivityTracing"
                    propagateActivity="true">
            <listeners>
               <add name="sdt"
                   type="System.Diagnostics.XmlWriterTraceListener"
                   initializeData= "SdrConfigExample.e2e" />
            </listeners>
         </source>
    </sources>
</system.diagnostics>
```

이 예제에서는 추적 수신기의 이름과 형식을 지정합니다. 수신기 이름은 `sdt`로 지정되고 표준 .NET Framework 추적 수신기(System.Diagnostics.XmlWriterTraceListener)는 형식으로 추가됩니다. @No__t_0 특성은 수신기가 `SdrConfigExample.e2e` 되는 로그 파일의 이름을 설정 하는 데 사용 됩니다. 로그 파일에 대해 단순한 파일 이름 대신 정규화된 경로를 사용할 수 있습니다.

예제에서는 루트 디렉터리에 SdrConfigExample.e2e라는 파일을 만듭니다. "WCF 추적 파일 열기 및 보기" 섹션에 설명 된 대로 추적 뷰어를 사용 하 여 파일을 여는 경우 전송 된 모든 메시지를 볼 수 있습니다.

추적 수준은 `switchValue` 설정에 의해 제어됩니다. 다음 표에서는 사용할 수 있는 추적 수준에 대해 설명합니다.

|추적 수준|설명|
|-----------------|-----------------|
|Critical|-빠른 오류 및 이벤트 로그 항목을 기록 하 고 상관 관계 정보를 추적 합니다. 다음은 Critical 수준을 사용할 수 있는 경우에 대한 일부 예제입니다.<br />-처리 되지 않은 예외로 인해 AppDomain이 종료 되었습니다.<br />-응용 프로그램을 시작 하지 못합니다.<br />-오류를 발생 시킨 메시지는 Myapp.exe 프로세스에서 발생 한 것입니다.|
|Error|-모든 예외를 로깅합니다. 다음과 같은 경우에 Error 수준을 사용할 수 있습니다.<br />-잘못 된 캐스트 예외로 인해 코드가 손상 되었습니다.<br />-"끝점을 만들지 못했습니다." 예외로 인해 응용 프로그램이 시작 될 때 실패할 수 있습니다.|
|경고|-이후에 오류 또는 심각한 오류가 발생할 수 있는 조건이 있습니다. 다음과 같은 경우에 이 수준을 사용할 수 있습니다.<br />-제한 설정에서 허용 하는 것 보다 많은 요청을 응용 프로그램에서 수신 합니다.<br />-수신 큐는 구성 된 용량의 98%입니다.|
|Information|-시스템 상태 모니터링 및 진단, 성능 측정 또는 프로 파일링에 유용한 메시지가 생성 됩니다. 용량 계획 및 성능 관리에 이러한 정보를 사용할 수 있습니다. 다음과 같은 경우에 이 수준을 사용할 수 있습니다.<br />-메시지가 AppDomain에 도달 하 여 deserialize 된 후 오류가 발생 했습니다.<br />-HTTP 바인딩을 만드는 동안 오류가 발생 했습니다.|
|자세히|-사용자 코드 및 서비스에 대 한 디버그 수준 추적입니다. 다음과 같은 경우에 이 수준을 설정합니다.<br />-오류가 발생 했을 때 코드에서 호출 된 메서드를 확실히 알 수 없습니다.<br />-잘못 된 끝점이 구성 되었으며, 예약 저장소의 항목이 잠겨 있어 서비스를 시작 하지 못했습니다.|
|ActivityTracing|처리 동작과 구성 요소 간의 흐름 이벤트입니다.<br /><br /> 이 수준에서 관리자와 개발자가 같은 애플리케이션 도메인의 애플리케이션을 서로 연결할 수 있습니다.<br /><br /> -작업 경계에 대 한 추적: start/stop.<br />-전송에 대 한 추적입니다.|

 `add`를 사용하여 사용할 추적 수신기의 이름과 형식을 지정할 수 있습니다. 예제 구성에서 수신기 이름은 `sdt`로 지정되고 표준 .NET Framework 추적 수신기(`System.Diagnostics.XmlWriterTraceListener`)는 형식으로 추가됩니다. `initializeData`를 사용하여 해당 수신기의 로그 파일 이름을 설정합니다. 또한 단순한 파일 이름 대신 정규화된 경로를 사용할 수 있습니다.

.NET Framework 4.8부터 일부 고대비 테마의 ComboBox 컨트롤은 올바른 색으로 표시 됩니다. *Svctraceviewer.exe* 파일에서 다음 설정을 제거 하 여이 변경 내용을 사용 하지 않도록 설정할 수 있습니다.

```xml
<AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
```

## <a name="using-the-service-trace-viewer-tool"></a>Service Trace Viewer 도구 사용

### <a name="opening-and-viewing-wcf-trace-files"></a>WCF 추적 파일 열기 및 보기

서비스 추적 뷰어는 다음 세 가지 파일 형식을 지원합니다.

- WCF 추적 파일 (. .Svclog)

- 이벤트 추적 파일(.etl)

- 심홍색 추적 파일

 서비스 추적 뷰어를 사용하면 지원되는 모든 추적 파일을 열고, 추가 추적 파일을 추가 및 통합하거나, 동시에 추적 파일 그룹을 열고 병합할 수 있습니다.

##### <a name="to-open-a-trace-file"></a>추적 파일을 열려면

1. 명령 창을 사용 하 여 서비스 추적 뷰어를 시작 하 여 WCF 설치 위치 (C:\Program Files\Microsoft SDKs\Windows\v6.0\Bin)로 이동한 다음 `SvcTraceViewer.exe`을 입력 합니다.

> [!NOTE]
> Service Trace Viewer 도구는 .svclog 및 .stvproj라는 두 개의 파일 형식과 연결됩니다. 파일 확장명을 등록 및 등록 취소하기 위해 명령줄에 두 매개 변수를 사용할 수 있습니다.
>
> /register: 파일 확장명 ".svclog" 및 ".stvproj"의 연결을 SvcTraceViewer.exe와 함께 등록합니다.
>
> /unregister: 파일 확장명 ".svclog" 및 ".stvproj"의 연결을 SvcTraceViewer.exe와 함께 등록 취소합니다.

1. Service Trace Viewer가 시작 되 면 **파일** 을 클릭 한 다음 **열기**를 가리킵니다. 추적 파일이 저장되는 위치로 이동합니다.

2. 열려는 추적 파일을 두 번 클릭합니다.

    > [!NOTE]
    > 여러 추적 파일을 클릭할 때 Shift를 누르면 동시에 선택하여 열 수 있습니다. Service Trace Viewer는 모든 파일의 콘텐츠를 병합하여 하나의 보기로 표시합니다. 예를 들어, 클라이언트와 서비스 모두의 추적 파일을 열 수 있습니다. 이는 구성 시 메시지 로깅 및 동작 전파를 사용할 경우 유용합니다. 이렇게 하면 클라이언트와 서비스 사이의 메시지 교환을 검사할 수 있습니다. 여러 파일을 뷰어로 끌어 오거나 **프로젝트** 탭을 사용할 수도 있습니다. 자세한 내용은 프로젝트 관리 섹션을 참조 하세요.

3. 열려 있는 컬렉션에 추적 파일을 더 추가 하려면 **파일** 을 클릭 한 다음 **추가**를 가리킵니다. 열려 있는 창에서 추적 파일의 위치를 찾고 추가하려는 파일을 두 번 클릭합니다.

> [!CAUTION]
> 200MB보다 큰 추적 로그 파일을 로드하지 않는 것이 좋습니다. 이 제한보다 큰 파일을 로드하면 컴퓨터의 리소스에 따라 로딩 프로세스를 수행하는 데 시간이 오래 걸릴 수 있습니다. Service Trace Viewer 도구가 오랜 시간 동안 응답하지 않거나 컴퓨터의 메모리가 부족할 수 있습니다. 이 문제를 방지하려면 부분 로드를 구성하는 것이 좋습니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 "큰 추적 파일 로드" 단원을 참조하십시오.

#### <a name="event-tracing-and-crimson-tracing"></a>이벤트 추적 및 심홍색 추적

뷰어의 네이티브 형식은 WCF에서 내보내는 동작 추적 형식입니다. 다른 형식으로 내보낸 추적은 뷰어가 이를 표시하기 전에 전환되어야 합니다. 현재 동작 추적 형식 외에도 뷰어는 이벤트 추적 및 심홍색 추적을 지원합니다.

특정 동작 추적이 포함되지 않은 파일을 열 때 뷰어는 파일 변환을 시도합니다. 변환된 추적 데이터를 포함할 파일의 이름 및 위치를 지정해야 합니다. 데이터가 변환되고 나면 뷰어가 새 파일의 콘텐츠를 표시합니다.

> [!NOTE]
> 변환을 위해서는 변환된 추적 데이터를 저장할 디스크 공간이 필요합니다. 변환을 시작하기 전에 데이터를 저장할 충분한 디스크 공간이 있는지 확인하십시오. 그렇지 않으면 변환에 실패합니다.

### <a name="managing-projects"></a>프로젝트 관리

뷰어는 여러 추적 파일 보기를 활용할 수 있도록 프로젝트를 지원합니다. 예를 들어, 클라이언트 추적 파일 및 서비스 추적 파일이 있는 경우 이를 프로젝트에 추가할 수 있습니다. 그러면 프로젝트를 열 때마다 프로젝트 내의 모든 추적 파일이 동시에 로드됩니다.

프로젝트를 관리하는 방법은 두 가지입니다.

- **파일** 메뉴에서 프로젝트를 열고, 저장 하 고, 닫을 수 있습니다.

- **프로젝트** 탭에서 프로젝트에 파일을 추가할 수 있습니다.

### <a name="viewing-wcf-traces"></a>WCF 추적 보기

WCF는 활동 추적 형식을 사용 하 여 추적을 내보냅니다. 동작 추적 모델에서 개별 추적은 각 목적에 따라 동작별로 그룹화됩니다. 논리 제어 흐름은 활동 간에 전달됩니다. 예를 들어, 애플리케이션의 수명 동안 많은 &quot;메시지 보내기 동작&quot;이 나타나고 사라집니다. 추적 및 작업 보기와 서비스 추적 뷰어의 사용자 인터페이스에 대 한 자세한 내용은 [서비스 추적 뷰어를 사용 하 여 상관 관계 추적 및 문제 해결](./diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)을 참조 하세요.

#### <a name="switching-to-different-views"></a>다른 보기로 전환

Service Trace Viewer는 다음과 같이 여러 보기를 제공합니다. 이러한 도구는 뷰어의 왼쪽 창에 탭으로 표시 되며 **보기** 메뉴에서 액세스할 수도 있습니다.

- 동작 보기

- 프로젝트 보기

- 메시지 보기

- 그래프 뷰

##### <a name="activity-view"></a>동작 보기

추적 파일이 열리면 추적을 활동으로 그룹화 하 고 왼쪽 창의 **활동** 보기에 표시할 수 있습니다.

활동 **보기는** 활동 이름, 활동의 추적 수, 기간 시간, 시작 시간 및 종료 시간을 표시 합니다.

나열된 활동 중 하나를 클릭하면 이 활동의 추적이 오른쪽 추적 창에 표시됩니다. 그러면 추적을 선택하여 세부 정보를 볼 수 있습니다.

**Ctrl** 또는 **Shift** 키를 누르고 원하는 활동을 클릭 하 여 여러 활동을 선택할 수 있습니다. 추적 창에는 선택된 활동의 모든 추적이 표시됩니다.

활동을 두 번 클릭 하 여 **그래프** 보기에 표시할 수 있습니다. 또 다른 방법은 활동을 선택 하 고 **그래프** 뷰로 전환 하는 것입니다.

> [!NOTE]
> 활동 "000000000000"은 그래프 보기에 표시할 수 없는 특별 한 활동입니다. 다른 모든 활동이 연결되므로, 이 활동을 표시하면 성능에 심각한 영향을 미칩니다.

열 제목을 클릭하여 동작 목록을 정렬할 수 있습니다. 경고 추적이 포함된 동작의 배경은 노란색이고 오류 추적이 포함된 동작의 배경은 빨간색입니다.

동작에는 다른 형식이 있으며, 각 형식은 각 동작의 왼쪽에 있는 아이콘에 해당합니다. 각 의미에 대해서는 추적 아이콘 이해 단원을 참조하십시오.

##### <a name="project-view"></a>프로젝트 보기

이 보기를 사용하면 현재 프로젝트의 추적 파일을 관리할 수 있습니다. 자세한 내용은 프로젝트 관리 단원을 참조하십시오.

##### <a name="message-view"></a>메시지 보기

이 보기를 사용 하면 Action, Date/Time, Process, 활동 및 From/To를 비롯 한 모든 메시지 로그 추적을 보고 연결 된 메시지 로그 추적의 세부 정보로 이동할 수 있습니다. 메시지 흐름을 쉽게 탐색할 수 있도록 작업 경계, 프로세스/스레드 또는 송신 & 수신 별로 메시지 로그 추적을 그룹화 할 수 있습니다.

##### <a name="graph-view"></a>그래프 뷰

이 보기는 지정 된 작업에 대 한 추적 데이터를 차트 형식으로 표시 합니다. 차트 형식을 사용하면 여러 동작 간 데이터의 이동에 따른 이벤트의 단계별 실행 및 이들 간의 상호 관계를 볼 수 있습니다.

**그래프** 뷰로 전환 하려면 **작업 보기에서 작업을** 선택 하 고 **작업** 탭을 클릭 하거나 **메시지** 보기에서 메시지 로그 추적을 클릭 합니다. 여러 추적 파일이 로드되고 해당 동작에 두 개 이상 파일의 추적이 포함되는 경우 모든 관련 추적이 그래프 보기에 나타납니다. 활동 및 메시지 로그 추적을 두 번 클릭 하면 **그래프** 보기도 표시 됩니다.

**그래프** 뷰에서 각 세로 열은 활동을 나타내며 열의 각 블록은 추적을 나타냅니다. 활동은 프로세스 또는 스레드별로 그룹화됩니다. 동작 사이의 작은 화살표는 전송을 나타냅니다. 프로세스 사이의 큰 화살표는 메시지 교환을 나타냅니다. 선택 항목의 활동은 항상 노란색입니다.

###### <a name="selecting-traces-in-the-graph"></a>그래프에서 추적 선택

1. 그래프에서 블록을 클릭합니다.

2. 위쪽 및 아래쪽 키를 사용하여 인접 추적을 선택합니다.

3. 추적 창 및 세부 정보 창에서 추적 정보를 확인합니다.

###### <a name="expanding-or-collapsing-activity-transfers"></a>동작 전송 확장명 또는 축소

선택 항목의 활동이 다른 활동으로 전송될 때 활동 전송을 확장할 수 있습니다. 이를 통해 전송을 따라갈 수 있습니다.

동작 전송을 확장 또는 축소하려면

1. 전송 아이콘의 왼쪽에 있는 "+" 기호를 사용 하 여 전송 추적을 찾습니다.

2. "+"를 클릭 하거나 키보드를 사용 하 여 **Ctrl** 및 "+"를 누릅니다.

3. 다음 동작이 그래프에 나타납니다.

4. "-"가 전송 아이콘의 왼쪽에 나타납니다. "-" 기호를 클릭 하거나 Ctrl과 "-"를 누르면 활동 전송이 축소 됩니다.

> [!NOTE]
> 동작에 여러 개의 전송이 있고 그 전송 중에 하나를 확장하면 루트에서 새 동작으로 이어지는 동작이 표시됩니다. 이러한 새 활동은 축소된 형식으로 표시됩니다. 이러한 활동의 세부 정보를 확인하려면 그래프의 헤더에서 확장 아이콘을 클릭하여 활동을 세로로 확장하십시오.

###### <a name="expanding-or-collapsing-activities-vertically"></a>활동을 세로로 확장 또는 축소

뷰어는 동작을 축소함으로써 동작 그래프에서 불필요한 세부 정보를 숨깁니다. 축소된 활동에서는 개별 추적이 표시되지 않습니다. 전송 추적만 나타납니다. 동작에서의 모든 추적을 보려면 그래프의 헤더에서 동작의 확장명 기호를 클릭하여 동작을 세로로 확장하십시오.

동작을 세로로 확장 또는 축소하려면

1. 활동 머리글에서 "+" 아이콘을 클릭 하 여 활동을 세로로 확장 합니다.

2. 모든 추적이 그래프에 표시됩니다.

3. 활동 머리글에서 "-" 아이콘을 클릭 하 여 활동을 세로로 축소 합니다.

4. 중요한 전송, 메시지 로그, 경고 및 예외 추적이 활동에 표시됩니다.

###### <a name="options"></a>옵션

그래프 뷰의 **옵션** 메뉴에서 두 옵션을 선택할 수 있습니다.

- 동작 경계 추적 표시: 선택하지 않을 경우 그래프에서 동작 경계 추적을 무시합니다.

- 메시지가 아닌 자세한 추적 표시: 선택하지 않을 경우 메시지 추적을 제외한 자세한 수준 추적을 무시합니다. 대부분의 경우 정보 표시 수준 추적은 분석에 있어 중요성이 낮습니다. 이 옵션은 정보 표시 수준 추적을 분석하지 않을 경우와 더 중요한 추적에 중점을 두려는 경우에만 유용합니다.

###### <a name="layout-mode"></a>레이아웃 모드

뷰어에는 두 가지 레이아웃 모드인 **프로세스** 와 **스레드**가 있습니다. 이 설정은 조직의 가장 큰 단위를 정의합니다. 기본 레이아웃 모드는 **프로세스**이며,이는 활동을 그래프의 프로세스로 그룹화 하는 것을 의미 합니다.

###### <a name="execution-list"></a>실행 목록

그래프에 표시할 프로세스 또는 스레드를 이 드롭다운 목록에서 선택할 수 있습니다. 예를 들어, A와 B라는 두 클라이언트의 추적 파일이 있고 서비스 하나가 열려 있으며 그래프에서 서비스 및 클라이언트 A만 표시하려는 경우, 목록에서 클라이언트 B의 선택을 취소할 수 있습니다.

#### <a name="viewing-trace-details"></a>추적 세부 정보 표시

추적 세부 정보를 보려면 추적 창에서 추적을 선택합니다. 자세한 정보가 세부 정보 창에 표시됩니다.

##### <a name="trace-pane"></a>추적 창

Service Trace Viewer에서 오른쪽 위 창이 추적 창입니다. 선택된 동작의 모든 추적을 추적 수준, 스레드 ID 및 프로세스 이름 등 추가 정보와 함께 나열합니다.

추적을 마우스 오른쪽 단추로 클릭 하 고 **클립보드로 추적 복사를**선택 하면 추적의 원시 XML을 클립보드로 복사할 수 있습니다.

##### <a name="detail-pane"></a>세부 정보 창

Service Trace Viewer에서 왼쪽 아래 창이 세부 정보 창입니다. 추적 세부 정보를 볼 수 있는 세 개의 탭을 제공합니다.

**서식이 지정** 된 보기에는 보다 체계적으로 정보가 표시 됩니다. 표와 트리의 알려진 모든 XML 요소를 나열하며 정보를 보다 쉽게 읽고 이해하도록 해줍니다.

**Xml** 뷰에는 선택한 추적에 해당 하는 xml이 표시 됩니다. 강조 표시 및 구문 색을 지원합니다. **찾기** 를 사용 하 여 문자열을 검색 하는 경우 검색 결과가 강조 표시 됩니다.

메시지 **보기에** 는 메시지 로그 추적에서 XML의 메시지 부분이 표시 됩니다. 메시지가 아닌 추적을 선택할 때는 표시되지 않습니다.

### <a name="filtering-wcf-traces"></a>WCF 추적 필터링

추적을 보다 쉽게 분석하기 위해 다음 방법으로 추적을 필터링할 수 있습니다.

- 필터 도구 모음은 미리 정의된 사용자 지정 필터에 대한 액세스를 제공합니다. **보기** 메뉴를 통해 사용 하도록 설정할 수 있습니다.

- 미리 정의 된 뷰어 필터를 사용 하 여 WCF 추적의 부분을 선택적으로 필터링 할 수 있습니다. 기본적으로 모든 인프라 추적이 전달될 수 있도록 설정되어 있습니다. 이 필터의 설정은 **보기** 메뉴의 **필터 옵션** 하위 메뉴에 정의 되어 있습니다.

- 사용자 지정 XPath 필터를 사용하면 필터링을 완벽하게 제어할 수 있습니다. **보기** 메뉴의 **사용자 지정 필터** 에서 정의할 수 있습니다.

모든 필터를 통해 전달되는 추적만 표시됩니다.

#### <a name="using-the-filter-toolbar"></a>필터 도구 모음 사용

필터 도구 모음은 도구의 맨 위에 표시됩니다. 표시 되지 않는 경우 **보기** 메뉴에서 활성화할 수 있습니다. 도구 모음에는 세 가지 구성 요소가 있습니다.

- 찾을 대상: **검색** 은 필터 작업에서 찾을 제목을 정의 합니다. 예를 들어, 프로세스 X의 컨텍스트에서 내보낸 모든 추적을 찾으려면이 필드를 X로 설정 하 고 **검색** 필드를 ' 프로세스 이름 '으로 설정 합니다. 시간 기반 필터를 선택하면 이 필드가 날짜/시간 선택기 컨트롤로 변경됩니다.

- 검색 위치: 이 필드는 적용할 필터의 형식을 정의합니다.

- 수준: 수준 설정은 필터에서 허용하는 최소 추적 수준을 정의합니다. 예를 들어, 수준을 오류 이상으로 설정하면 오류 및 위험 수준의 추적만 표시됩니다. 이 필터는 찾을 대상 및 검색 위치에서 정의된 조건과 결합합니다.

**지금 필터** 단추를 클릭 하면 필터 작업이 시작 됩니다. 일부 필터는 특히 큰 데이터 집합에 적용할 경우 완료할 때까지 시간이 오래 걸립니다. **작업** 메뉴의 상태 표시줄에 나타나는 **중지** 단추를 눌러 필터 작업을 취소할 수 있습니다.

**Clear** 단추는 미리 정의 된 필터와 사용자 지정 필터를 다시 설정 하 여 모든 추적이 통과할 수 있도록 합니다.

#### <a name="filter-options"></a>필터 옵션

뷰어는 보기에서 WCF 추적을 자동으로 제거할 수 있습니다. WCF의 특정 영역에서 내보내진 추적을 선택적으로 제거할 수 있습니다. 예를 들어, 보기에서 트랜잭션 관련 추적을 제거할 수 있습니다.

이 필터의 설정은 **보기** 메뉴의 **필터 옵션** 하위 메뉴에 정의 되어 있습니다.

#### <a name="custom-filters"></a>사용자 지정 필터

XPath(XML Path Language)에 익숙한 경우에는 이를 사용하여 관심 있는 모든 XML 요소에 대해 추적 데이터를 검색하도록 사용자 지정 필터를 구성할 수 있습니다. 필터는 필터 도구 모음을 통해 액세스할 수 있습니다.

사용자 지정 필터는 매개 변수를 포함할 수 있습니다. 또한 기존의 사용자 지정 필터를 가져올 수 있습니다.

##### <a name="creating-a-custom-filter"></a>사용자 지정 폴더 만들기

필터는 두 가지 방법으로 만들 수 있습니다.

###### <a name="creating-a-custom-filter-using-the-template-wizard"></a>템플릿 마법사를 사용하여 사용자 지정 필터 만들기

기존 추적을 클릭하고 추적의 구조에 기반한 필터를 만들 수 있습니다. 이 예제에서는 스레드 ID를 기반으로 사용자 지정 필터를 만듭니다.

1. 뷰어의 오른쪽 위 영역에 있는 추적 창에서 필터링하려는 요소가 포함된 추적을 선택합니다.

2. 추적 창 위쪽에 있는 **사용자 지정 필터 만들기** 단추를 클릭 합니다.

3. 표시되는 대화 상자에서 필터의 이름을 입력합니다. 이 예제에서는 `Thread ID`를 입력 합니다. 필터의 설명을 제공할 수도 있습니다.

4. 왼쪽의 트리 뷰에는 1단계에서 선택한 추적 레코드의 구조가 표시됩니다. 조건을 만들려는 요소를 찾으십시오. 이 예에서는 XPath: /E2ETraceEvent/System/Execution/@ThreadID 노드에 있는 ThreadID로 이동 합니다. 트리 뷰에서 ThreadID 특성을 두 번 클릭합니다. 이는 대화 상자의 오른쪽에 있는 특성에 대한 식을 만듭니다.

5. ThreadID 조건에 대 한 매개 변수 필드를 없음에서 ' {0} '로 변경 합니다. 이 단계를 통해 필터가 적용될 때 ThreadID 값이 구성되도록 할 수 있습니다. 필터 적용 방법 단원을 참조하십시오. 매개 변수는 4개까지 정의할 수 있습니다. 조건은 OR 연산자를 사용하여 결합됩니다.

6. **확인** 을 클릭 하 여 필터를 만듭니다.

> [!NOTE]
> 템플릿 마법사를 사용하여 필터를 만들고 나면 수동으로만 이를 편집할 수 있습니다. 이전에 만들어진 필터에 대한 마법사는 활성화할 수 없습니다. 또한 템플릿 마법사에서 만들어진 XPath 필터의 조건은 OR 연산자를 사용하여 결합됩니다. AND 연산이 필요한 경우 필터 식이 만들어진 후에 이를 편집할 수 있습니다.

###### <a name="creating-a-custom-filter-manually"></a>사용자 지정 필터 수동으로 만들기

사용자 지정 필터 메뉴에서 XPath 필터를 수동으로 입력할 수 있습니다.

1. 보기 메뉴에서 **사용자 지정 필터** 메뉴 항목을 클릭 합니다.

2. 표시 되는 대화 상자에서 **새로 만들기를 클릭 합니다.**

3. 최소한 필터 이름 및 XPath 식을 지정합니다.

4. **확인**을 클릭합니다.

###### <a name="applying-a-custom-filter"></a>사용자 지정 필터 적용

사용자 지정 필터가 만들어지면 필터 도구 모음을 통해 액세스할 수 있습니다. 필터 도구 모음에 있는 **검색** 대상 필드에 적용할 필터를 선택 합니다. 이전 예에서는 ‘스레드 ID’를 선택합니다.

1. **찾을 내용** 필드에서 원하는 값을 지정 합니다. 이 예제에서는 검색하려는 스레드의 ID를 입력합니다.

2. **지금 필터**를 클릭 하 고 작업의 결과를 확인 합니다.

필터에서 매개 변수를 여러 개 사용 하는 경우 **찾을 내용** 필드에서 구분자로 '; '을 사용 하 여 입력 합니다. 예를 들어, ‘1;findValue;text’ 문자열은 세 개의 매개 변수를 정의합니다. 뷰어는 필터의 {0} 매개 변수에 ' 1 '을 적용 합니다. ' findValue ' 및 ' text '는 각각 {1} 및 {2}에 적용 됩니다.

###### <a name="sharing-custom-filters"></a>사용자 지정 필터 공유

여러 세션 및 여러 사용자 간에 사용자 지정 필터를 공유할 수 있습니다. 필터를 정의 파일로 내보내고, 다른 위치에서 이 파일을 가져올 수 있습니다.

 사용자 지정 필터를 가져오려면

1. **보기** 메뉴에서 **사용자 지정 필터**를 클릭 합니다.

2. 열리는 대화 상자에서 **가져오기** 단추를 클릭 합니다.

3. 사용자 지정 필터 파일 (. stvcf)로 이동 하 고 파일을 클릭 한 다음 **열기** 단추를 클릭 합니다.

사용자 지정 필터를 내보내려면

1. 보기 메뉴에서 **사용자 지정 필터**를 클릭 합니다.

2. 대화 상자가 열리면 내보낼 필터를 선택합니다.

3. **내보내기** 단추를 클릭 합니다.

4. 사용자 지정 필터 정의 파일 (. stvcf)의 이름과 위치를 지정 하 고 **저장** 단추를 클릭 합니다.

> [!NOTE]
> 이러한 사용자 지정 필터는 서비스 추적 뷰어에서만 가져오고 내보낼 수 있습니다. 다른 도구로는 읽을 수 없습니다.

### <a name="finding-data"></a>데이터 찾기

뷰어는 데이터를 찾는 다음 방법을 제공합니다.

- 찾기 도구 모음은 가장 일반적인 찾기 옵션에 대한 신속한 액세스를 제공합니다.

- 찾기 대화 상자는 더 많은 찾기 옵션을 제공합니다. **편집** 메뉴 또는 짧은 키 Ctrl + F를 통해 액세스할 수 있습니다.

찾기 도구 모음은 뷰어의 맨 위에 나타납니다. 표시 되지 않는 경우 **보기** 메뉴에서 활성화할 수 있습니다. 도구 모음에는 두 개의 구성 요소가 있습니다.

- 찾을 내용: 검색 키워드를 입력할 수 있습니다.

- 찾는 위치: 검색 범위를 입력할 수 있습니다. 모든 동작에서 검색할지 현재 동작에서만 검색할지 선택할 수 있습니다.

찾기 대화 상자는 다음 두 개의 추가 옵션을 제공합니다.

- 대상 찾기:

  - "원시 로그 데이터" 옵션은 모든 원시 데이터에서 키워드를 검색 합니다.

  - "XML 텍스트" 및 "XML 특성" 옵션은 XML 요소만 검색 합니다.

  - "로그 된 메시지" 옵션은 메시지 에서만 키워드를 검색 합니다.

- 루트 작업 무시: 검색은 "000000000000" 활동에서 추적을 무시 합니다. 이렇게 하면 루트 동작에 수천 개의 추적(대부분 전송)이 포함되는 경우 대규모 추적 파일에서 성능이 향상됩니다.

### <a name="navigating-traces"></a>추적 탐색

추적은 애플리케이션 런타임 동안 단계별로 기록되므로 추적을 탐색하면 애플리케이션을 디버깅하는 데 도움을 줍니다. Service Trace Viewer는 추적을 탐색할 여러 가지 방법을 제공합니다.

#### <a name="step-forward-or-backward"></a>앞으로 가기 또는 뒤로 가기

각 추적을 프로그램의 코드 줄로 간주 하는 경우 앞으로는 Visual Studio IDE (통합 개발 환경)의 "프로시저 단위 실행"과 매우 유사 합니다. 차이점은 추적에서 뒤로 가기도 수행할 수 있다는 것입니다. 앞으로 가기란 동작 내에서 다음 추적으로 이동하는 것을 말합니다.

- 앞으로 가기: **활동** 메뉴를 사용 하거나 "F10"를 누릅니다. 추적 창에서 화살표 키 "down"을 사용할 수도 있습니다.

- 뒤로 이동: **활동** 메뉴를 사용 하거나 "F9"를 누릅니다. 추적 창에서 "위로" 화살표 키를 사용할 수도 있습니다.

> [!NOTE]
> 이렇게 하면 WCF 메시지에서 컴퓨터를 확장 하는 작업 Id를 전달할 수 있으므로 다른 프로세스 또는 다른 컴퓨터에서 발생 하는 작업으로 이동할 수 있습니다.

#### <a name="follow-transfer"></a>전송 이동

전송 추적은 추적 파일에서 특별한 추적입니다. 동작은 전송 추적에 의해 다른 동작으로 전송될 수 있습니다. 예를 들어 "활동 A"는 "활동 B"로 전송 될 수 있습니다. 이러한 경우 "To: Activity" 라는 이름의 "활동 A"의 전송 추적과 전송 아이콘이 있습니다. 이 전송 추적은 두 추적 간의 링크입니다. "활동 B"에서는 활동의 끝에 전송 추적이 있어 "활동 A"로 다시 전송 될 수도 있습니다. 이는 프로그램의 함수 호출과 유사합니다. A가 B를 호출하면 B가 반환되는 것입니다.

"전송 따르기"는 디버거의 "한 단계씩 코드 실행"과 유사 합니다. 이는 A에서 B로의 전송을 따릅니다. 이는 다른 추적에 아무런 영향을 주지 않습니다.

전송을 따르는 데는 마우스를 사용하는 것과 키보드를 사용하는 두 가지 방법이 있습니다.

- 마우스 사용: 추적 창에서 Transfer 추적을 두 번 클릭합니다.

- 키보드 사용: 전송 추적을 선택 하 고, **활동** 메뉴에서 "전송 이동"을 사용 하거나 "F11"를 누릅니다.

> [!NOTE]
> 많은 경우에 동작 A가 동작 B로 전송될 때, 동작 A는 동작 B가 동작 A로 다시 전송할 때까지 대기합니다. 이는 동작 B가 실제로 추적 중일 때 동작 A가 해당 기간 동안 추적을 기록하지 않는 것을 의미합니다. 그러나 동작 A가 대기하지 않고 추적 기록을 계속할 가능성도 있습니다. 또한 동작 B가 동작 A로 다시 전송되지 않을 수도 있습니다. 따라서 이런 점에서 동작 전송은 함수 호출과는 다릅니다. 그래프 보기에서 동작 전송을 더 잘 이해할 수 있습니다.

#### <a name="jump-to-next-or-previous-transfer"></a>다음 추적 및 이전 추적으로 이동

현재 동작을 분석하거나 여러 동작을 선택한 경우 선택한 동작을 분석할 때 전송할 동작을 신속하게 찾아야 할 경우가 있습니다. "다음 전송으로 이동"을 사용 하면 작업에서 다음 전송 추적을 찾을 수 있습니다. 전송 추적을 찾은 후에는 "전송 따르기"를 사용 하 여 다음 작업을 한 단계씩 실행 할 수 있습니다.

- 다음 전송으로 이동: **활동** 메뉴를 사용 하거나 "Ctrl + F10"를 누릅니다.

- 이전 전송으로 이동: **활동** 메뉴를 사용 하거나 "Ctrl + F9"를 누릅니다.

#### <a name="navigate-in-graph-view"></a>그래프 보기에서 탐색

작업 창 및 추적 창에서 탐색 하는 것은 디버깅과 유사 하지만 **그래프** 보기를 사용 하면 탐색에 훨씬 더 나은 환경을 제공 합니다. 자세한 내용은 "그래프 뷰" 섹션을 참조 하세요.

### <a name="loading-large-trace-files"></a>큰 추적 파일 로드

추적 파일은 매우 클 수 있습니다. 예를 들어 "자세한 정보" 수준에서 추적을 설정 하는 경우 몇 분 동안 실행 되는 추적 파일이 네트워크 속도 및 통신 패턴에 따라 쉽게 수백 메가바이트 또는 그 더 커질 수 있습니다.

Service Trace Viewer에서 매우 큰 추적 파일을 열 때는 시스템 성능에 좋지 않은 영향을 미칠 수 있습니다. 로드 속도 및 로드 이후의 응답 시간이 느려질 수 있습니다. 실제 속도는 하드웨어 구성에 따라 시간마다 다릅니다. 대부분의 PC에서 200M보다 큰 추적 파일을 로드하면 시스템 성능에 심각한 영향을 미칠 수 있습니다. 1G보다 더 큰 추적 파일의 경우 도구가 사용 가능한 모든 메모리를 전부 사용하거나 장시간 응답이 중지될 수 있습니다.

대량 추적 파일을 분석할 때 로드 및 응답 시간이 느려지는 것을 방지 하기 위해 서비스 추적 뷰어는 "부분 로딩" 이라는 기능을 제공 합니다 .이 기능을 사용 하면 한 번에 추적의 일부만 로드 됩니다. 예를 들어, 서버에서 며칠 동안 실행 중인 1GB가 넘는 추적 파일이 있을 수 있습니다. 일부 오류가 발생되어 추적을 분석하려는 경우 추적 파일을 모두 열 필요가 없습니다. 대신 오류가 발생할 수 있는 일정 기간 내에 추적을 로드할 수 있습니다. 범위가 더 작기 때문에 Service Trace Viewer 도구는 파일을 보다 빨리 로드할 수 있으며, 사용자는 더 작은 데이터 집합을 사용하여 오류를 식별할 수 있습니다.

#### <a name="enabling-partial-loading"></a>부분 로드 사용

수동으로 부분 로드를 활성화할 필요가 없습니다. 로드하려는 추적 파일의 전체 크기가 40MB를 초과하면, Service Trace Viewer는 사용자가 로드하려는 해당 부분을 선택할 수 있도록 부분 로드 대화 상자를 자동으로 표시합니다.

> [!NOTE]
> 추적이 시간 범위에서 균등하게 분산되지 않으므로 부분 로드 도구 모음에서 지정하는 기간의 길이가 표시된 로드 크기에 비례하지 않을 수 있습니다. 실제 로드 크기는 부분 로드 대화 상자의 예측 크기보다 작을 수 있습니다.

#### <a name="adjusting-partial-loading"></a>부분 로드 조정

추적 파일을 부분적으로 로드하고 나면 로드할 데이터 집합을 변경해야 할 수 있습니다. 뷰어의 맨 위에 있는 부분 로드 도구 모음을 조정하여 이를 수행할 수 있습니다.

1. 마우스로 도구 모음을 이동하거나 시작 및 종료 시간을 입력합니다.

2. **조정** 단추를 클릭 합니다.

## <a name="understanding-trace-icons"></a>추적 아이콘 이해

다음은 서비스 추적 뷰어 도구가 **활동** 보기, **그래프** 뷰 및 **추적** 창에서 다른 항목을 나타내는 데 사용 하는 아이콘 목록입니다.

> [!NOTE]
> 분류 되지 않은 일부 추적 (예: "메시지를 닫음")에는 아이콘이 없습니다.

### <a name="activity-tracing-traces"></a>동작 추적

|아이콘|설명|
|----------|-----------------|
|![경고 추적](./media/7457c4ed-8383-4ac7-bada-bcb27409da58.gif "7457c4ed-8383-4ac7-bada-bcb27409da58")|경고 추적: 경고 수준으로 보내진 추적입니다.|
|![오류 추적](./media/7d908807-4967-4f6d-9226-d52125db69ca.gif "7d908807-4967-4f6d-9226-d52125db69ca")|오류 추적: 오류 수준으로 보내진 추적입니다.|
|![작업 시작 추적:](./media/8a728f91-5f80-4a95-afe8-0b6acd6e0317.gif "8a728f91-5f80-4a95-afe8-0b6acd6e0317")|동작 시작 추적: 동작의 시작을 표시하는 추적입니다. 여기에는 동작의 이름이 포함됩니다. 애플리케이션 디자이너 또는 개발자의 경우 각 프로세스 또는 스레드의 동작 ID당 하나의 동작 시작 추적을 정의해야 합니다.<br /><br /> 동작 ID가 추적 상관 관계를 위해 추적 소스 간에 전파되는 경우 각 추적 소스의 동일한 동작 ID에 대해 여러 시작이 표시됩니다. ActivityTracing이 추적 소스에 사용되면 시작 추적이 내보내집니다.|
|![활동 중단 추적](./media/a0493e95-653e-4af8-84a4-4d09a400bc31.gif "a0493e95-653e-4af8-84a4-4d09a400bc31")|동작 중지 추적: 동작의 종료를 표시하는 추적입니다. 이어야 합니다. 여기에는 동작의 이름이 포함됩니다. 애플리케이션 디자이너 또는 개발자의 경우 각 추적 소스의 동작 ID당 하나의 동작 중지 추적을 정의해야 합니다. 해당 추적 소스에서 내보낸 동작 중지 후에는 추적 시간의 세분성이 충분히 작지 않은 경우를 제외하고 지정된 추적 소스에서 추적이 표시되지 않습니다. 이 경우 시간이 동일한 두 개의 추적(중지 포함)이 표시될 때 인터리브될 수 있습니다. 동작 ID가 추적 상관 관계를 위해 추적 소스 간에 전파되는 경우 각 추적 소스의 동일한 동작 ID에 대해 여러 중지가 표시됩니다. ActivityTracing이 추적 소스에 사용되면 중지 추적이 내보내집니다.|
|![활동 일시 중단 추적](./media/6f7f4191-df2b-4592-8998-8379769e2d32.gif "6f7f4191-df2b-4592-8998-8379769e2d32")|동작 일시 중단 추적: 동작이 일시 중단된 시간을 표시하는 추적입니다. 동작이 다시 시작될 때까지 일시 중단된 동작에서 내보낸 추적이 없습니다. 일시 중단된 동작은 추적 소스 범위에 있는 해당 동작에서 발생하는 프로세스가 없음을 의미합니다. 일시 중단/다시 시작 추적은 프로파일링에 유용합니다. ActivityTracing이 추적 소스에 사용되면 일시 중단 추적이 내보내집니다.|
|![작업 다시 시작 추적](./media/1060d9d2-c9c8-4e0a-9988-cdc2f7030f17.gif "1060d9d2-c9c8-4e0a-9988-cdc2f7030f17")|동작 다시 시작 추적: 동작이 일시 중단된 후에 다시 시작된 시간을 표시하는 추적입니다. 해당 동작에서 추적을 다시 내보낼 수 있습니다. 일시 중단/다시 시작 추적은 프로파일링에 유용합니다. ActivityTracing이 추적 소스에 사용되면 다시 시작 추적이 내보내집니다.|
|![](./media/b2d9850e-f362-4ae5-bb8d-9f6f3ca036a5.gif "B2d9850e-f362-4ae5-bb8d-9f6f3ca036a5") 전송|전송: 논리 제어 흐름이 하나의 동작에서 다른 동작으로 전송될 때 내보낸 추적입니다. 전송이 발생한 동작은 전송이 향하는 동작과 평행하게 작업을 계속 수행할 수 있습니다. ActivityTracing이 추적 소스에 사용되면 전송 추적이 내보내집니다.|
|(./media/1df215cb-b344-4f36-a20d-195999bda741.gif "1Df215cb-b344-4f36-a20d-195999bda741") ![에서 전송]|전송 시작: 다른 동작에서 현재 동작으로의 전송을 정의하는 추적입니다.|
|(./media/74255b6e-7c47-46ef-8e53-870c76b04c3f.gif "74255B6e-7c47-46ef-8e53-870c76b04c3f") ![로 전송]|전송 대상: 현재 동작에서 다른 동작으로의 논리 제어 흐름의 전송을 정의하는 추적입니다.|

### <a name="wcf-traces"></a>WCF 추적

|아이콘|설명|
|----------|-----------------|
|![메시지 로그 추적](./media/7c66e994-2476-4260-a0db-98948b9af197.gif "7c66e994-2476-4260-a0db-98948b9af197")|메시지 로그 추적: `System.ServiceModel.MessageLogging` 추적 소스를 사용 하는 경우 메시지 로깅 기능을 통해 WCF 메시지가 기록 될 때 내보내지는 추적입니다. 이 추적을 클릭하면 메시지가 표시됩니다. 메시지에 대해 구성할 수 있는 4개의 로깅 지점은 ServiceLevelSendRequest, TransportSend, TransportReceive 및 ServiceLevelReceiveRequest이며, 메시지 로그 추적의 `messageSource` 특성으로도 지정할 수 있습니다.|
|![메시지 수신 추적](./media/de4f586c-c5dd-41ec-b1c3-ac56b4dfa35c.gif "de4f586c-c5dd-41ec-b1c3-ac56b4dfa35c")|수신 된 메시지 추적: `System.ServiceModel` 추적 소스가 정보 또는 세부 정보 표시 수준에서 사용 되는 경우 WCF 메시지가 수신 될 때 내보내는 추적입니다. 이 추적은 동작 **그래프** 보기에서 메시지 상관 관계 화살표를 보는 데 필요 합니다.|
|![메시지 전송 추적](./media/558943c4-17cf-4c12-9405-677e995ac387.gif "558943c4-17cf-4c12-9405-677e995ac387")|전송 된 메시지 추적: `System.ServiceModel` 추적 소스가 정보 또는 자세한 수준에서 사용 하도록 설정 된 경우 WCF 메시지가 전송 될 때 내보내는 추적입니다. 이 추적은 동작 **그래프** 보기에서 메시지 상관 관계 화살표를 보는 데 필요 합니다.|

### <a name="activities"></a>활동

|아이콘|설명|
|----------|-----------------|
|![활동](./media/wcfc-defaultactivityc.gif "wcfc_defaultActivityc")|동작: 현재 동작이 제네릭 동작임을 나타냅니다.|
|![루트 활동](./media/5dc8e0eb-1c32-4076-8c66-594935beaee9.gif "5dc8e0eb-1c32-4076-8c66-594935beaee9")|루트 동작: 프로세스의 루트 동작을 나타냅니다.|

### <a name="wcf-activities"></a>WCF 동작

|아이콘|설명|
|----------|-----------------|
|![환경 활동](./media/29fa00ac-cf78-46e5-822d-56222fff61d1.gif "29fa00ac-cf78-46e5-822d-56222fff61d1")|환경 활동: WCF 호스트 또는 클라이언트를 만들거나, 열거나, 닫는 활동입니다. 이러한 단계 중에 발생한 오류는 이 동작에 나타납니다.|
|![Listen 활동](./media/d7b135f6-ec7d-45d7-9913-037ab30e4c26.gif "d7b135f6-ec7d-45d7-9913-037ab30e4c26")|Listen 활동: 수신기와 관련된 추적을 기록하는 동작입니다. 이 활동 내에서 수신기 정보 및 연결 요청을 볼 수 있습니다.|
|![바이트 수신 작업](./media/2f628580-b80f-45a7-925b-616c96426c0e.gif "2f628580-b80f-45a7-925b-616c96426c0e")|바이트 수신 동작: 두 엔드포인트 간의 연결에서 수신되는 들어오는 바이트와 관련된 모든 추적을 그룹화하는 동작입니다. 이 동작은 http.sys와 같은 동작 ID를 전파하는 전송 동작들을 상호 연결시키는 데 반드시 필요합니다. 중단과 같은 연결 오류가 이 동작에 나타납니다.|
|![메시지 처리 작업](./media/wcfc-executionactivityiconc.GIF "wcfc_ExecutionActivityIconc")|메시지 처리 작업: WCF 메시지 작성과 관련 된 추적을 그룹화 하는 작업입니다. 잘못된 봉투 또는 메시지로 인해 발생한 오류가 이 동작에 나타납니다. 이 동작 내에서 호출자로부터 동작 ID가 전파되었는지 여부를 확인하기 위해 메시지 헤더를 검사할 수 있습니다. 호출자로부터 활동 ID가 전파된 경우 작업 처리 활동(다음 아이콘)으로 전송할 때 호출자와 호출 수신자의 추적 간 상관 관계에 대해 전파된 활동 ID를 해당 활동에 할당할 수도 있습니다.|
|![메시지 로그 추적](./media/7c66e994-2476-4260-a0db-98948b9af197.gif "7c66e994-2476-4260-a0db-98948b9af197")|프로세스 동작 활동: 두 끝점에서 WCF 요청과 관련 된 모든 추적을 그룹화 하는 활동입니다. 구성의 두 엔드포인트에서 `propagateActivity`가 `true`로 설정되면 두 개의 엔드포인트에서 모든 추적이 직접 상관 관계에 대해 하나의 동작으로 병합됩니다. 해당 동작에는 전송 또는 보안 처리로 인해 발생한 오류가 포함되며, 응답이 있는 경우 사용자 코드 경계로 확장됩니다.|
|![메시지 처리 작업](./media/wcfc-executionactivityiconc.GIF "wcfc_ExecutionActivityIconc")|사용자 코드 실행 동작: 요청을 처리하기 위해 사용자 코드 추적을 그룹화하는 동작입니다.|

## <a name="troubleshooting"></a>문제 해결

레지스트리에 쓸 수 있는 권한이 없는 경우 "`svctraceviewer /register`" 명령을 사용 하 여 도구를 등록할 때 "Microsoft Service Trace Viewer가 시스템에 등록 되지 않았습니다." 라는 오류 메시지가 표시 됩니다. 이 경우 레지스트리에 쓰기 액세스 권한이 있는 계정을 사용하여 로그인해야 합니다.

또한 Service Trace Viewer 도구는 어셈블리 폴더에 있는 SvcTraceViewer.exe.settings 파일에 사용자 지정 필터 및 필터 옵션 같은 일부 설정을 씁니다. 이 파일에 대한 읽기 권한이 없으면 이 도구를 시작할 수 있지만 설정을 로드할 수는 없습니다.

.etl 파일을 열 때 "하나 이상의 추적을 처리하는 동안 알 수 없는 오류가 발생했습니다."라는 오류 메시지가 표시되면 .etl 파일의 형식이 잘못되었음을 의미합니다.

아랍어 운영 체제를 사용하여 작성된 추적 로그를 여는 경우 시간 필터가 작동하지 않을 수 있습니다. 예를 들어, 2005년은 아랍어 달력으로 1427년에 해당합니다. 그러나 Service Trace Viewer 도구 필터에서 지원하는 시간 범위는 1752 이전의 날짜를 지원하지 않습니다. 즉, 필터에서 올바른 날짜를 선택하지 못할 수도 있습니다. 이 문제를 해결 하려면 XPath 식을 사용 하 여 특정 시간 범위를 포함 하는 사용자 지정 필터 (**보기/사용자 지정**필터)를 만들 수 있습니다.

## <a name="see-also"></a>참조

- [Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결](./diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
- [추적 구성](./diagnostics/tracing/configuring-tracing.md)
- [엔드투엔드 추적](./diagnostics/tracing/end-to-end-tracing.md)
