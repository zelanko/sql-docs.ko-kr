---
title: 확장 이벤트의 대상 데이터에 대한 고급 보기
description: SQL Server Management Studio의 고급 기능을 사용하여 확장 이벤트의 대상 데이터를 자세히 살펴볼 수 있습니다. 데이터를 보고, 내보내고, 조작할 수 있습니다.
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 16671290ed86def1b013a77d991487dfdad26a10
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85779498"
---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>SQL Server 확장 이벤트의 대상 데이터 고급 보기

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]


이 문서에는 SQL Server Management Studio(SSMS.exe)의 고급 기능을 사용하여 확장 이벤트에서 대상 데이터를 상세하게 보는 방법이 나와 있습니다. 이 문서에서는 다음을 수행하는 방법을 설명합니다.


- 다양한 방법으로 대상 데이터 보기 및 열기
- 확장 이벤트에 대한 특별한 메뉴 또는 도구 모음을 사용하여 다양한 형식으로 대상 데이터 내보내기
- 데이터 보기 동안 또는 내보내기 전에 데이터 조작



### <a name="prerequisites"></a>사전 요구 사항

현재 문서에서는 이벤트 세션을 만들고 시작하는 방법은 이미 알고 있다고 가정합니다. 이벤트 세션을 만드는 방법은 다음 문서에서 이미 설명했습니다.

[빠른 시작: SQL Server의 확장 이벤트](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


이 문서에서는 또한 SSMS의 가장 최신 릴리스를 설치했다고 가정합니다. 설치 도움말은 다음을 참조하세요.

- [SSMS(SQL Server Management Studio) 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)



### <a name="differences-with-azure-sql-database"></a>Azure SQL 데이터베이스와의 차이점


두 제품, Microsoft SQL Server와 Azure SQL 데이터베이스는 확장 이벤트 구현 및 기능에서 높은 수준의 패리티가 있습니다. 그러나 SSMS UI(사용자 인터페이스)에 영향을 주는 몇 가지 차이점이 있습니다.


- SQL 데이터베이스의 경우 로컬 디스크 드라이브의 파일은 package0.event_file의 대상이 될 수 없습니다. 대신, Azure Storage 컨테이너를 사용해야 합니다. 따라서 SQL 데이터베이스에 연결된 경우, SSMS UI는 로컬 경로 및 파일 이름 대신 스토리지 컨테이너를 요청합니다.


- SSMS UI에서 **라이브 데이터 감시** 확인란이 회색으로 표시되고 비활성화되어 있으면 SQL 데이터베이스에 해당 기능을 사용할 수 없기 때문입니다.


- 몇 가지 확장 이벤트는 SQL Server와 함께 설치됩니다. **세션** 노드에서 **AlwaysOn_health** 등을 확인할 수 있습니다. 이러한 이벤트는 SQL 데이터베이스에는 없기 때문에 SQL 데이터베이스에 연결되어 있을 때는 표시되지 않습니다.


현재 문서는 SQL Server의 관점에서 작성되었습니다. 이 문서에서 사용하는 event_file 대상은 차이점 중 하나입니다. 중요한 차이점 또는 불분명한 차이점은 추가로 설명합니다.


Azure SQL 데이터베이스와 관련된 확장 이벤트에 대한 설명은 다음을 참조하세요.

- [Azure SQL 데이터베이스의 확장 이벤트](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)



## <a name="a-general-options"></a>A. 일반 옵션


일반적으로 고급 옵션은 다음과 같은 방법으로 액세스됩니다.


- **파일** > **열기** > **파일**의 일반 메뉴입니다.
- **개체 탐색기** 에서 **관리** > **확장 이벤트**에서 마우스 오른쪽 단추로 클릭합니다.
- **확장 이벤트**특별 메뉴와 확장 이벤트의 특별 도구 모음이 나타납니다.
- 대상 데이터가 표시되는 탭 창에서 마우스 오른쪽 단추로 클릭합니다.



## <a name="b-bring-target-data-into-ssms-for-display"></a>B. 대상 데이터를 표시하기 위해 SSMS로 가져오기


SSMS UI에 event_file 대상 데이터를 가져오는 방법에는 여러 가지가 있습니다. event_file 대상을 지정할 때 해당 파일 경로 및 이름을 설정합니다.

- .XEL은 파일 이름의 확장명입니다.


- 시스템은 이벤트 세션이 시작될 때마다 새 파일 이름에 큰 정수를 포함하여 세션이 시작되기 이전의 경우와 다른 고유한 파일 이름을 지정합니다.
  - *예:* Checkpoint_Begins_ES_0_131103935140400000.xel


- .XEL 내의 내용은 Notepad.exe를 사용하여 볼 수 있는 일반 텍스트가 아닙니다.
  - 원하는 경우 몇 가지 .XEL 파일을 함께 추가하는 방법은 **파일** > **열기** > **확장 이벤트 파일 병합**메뉴를 사용하면 됩니다.



SSMS는 모든 대상의 데이터를 표시할 수 있습니다. 하지만 여러 가지 대상에 따라 다르게 표시됩니다.

- *event_file:* event_file 대상의 데이터는 사용할 수 있는 다양한 기능으로 적절하게 표시됩니다.


- *ring_buffer:* 링 버퍼 대상의 데이터는 원시 XML로 표시됩니다.


- 다른 대상의 경우 표시하는 데 장점은 event_file의 장점과 ring_buffer의 장점 중간쯤에 있습니다.
  - 이러한 다른 대상에는 event_counter, histogram 및 pair_matching이 포함됩니다.


- *etw_classic_sync_target:* SSMS는 대상 유형 etw_classic_sync_target에서 데이터를 표시할 수 없습니다.



### <a name="b1-open-xel-with-menu-file--open--file"></a>B.1 파일 > 열기 > 파일 메뉴를 사용하여 .XEL 열기


표준 메뉴 **파일** > **열기** > **파일**을 사용하여 개별 .XEL 파일을 열 수 있습니다.

SSMS UI의 탭 모음으로 .XEL 파일을 끌어서 놓을 수도 있습니다.



### <a name="b2-view-target-data"></a>B.2 대상 데이터 보기


**대상 데이터 보기** 옵션에는 지금까지 캡처된 데이터가 표시됩니다.


**개체 탐색기** 창에서 노드를 확장한 다음 마우스 오른쪽 단추로 클릭합니다.

- **관리** > **확장 이벤트** > **세션** >  *[your-session]*  >  *[your-target-node]*  > **대상 데이터 보기**


대상 데이터가 SSMS의 탭 창에 표시됩니다. 다음 스크린샷에서 이 단계를 보여 줍니다.


![대상 > 대상 데이터 보기](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> **대상 데이터 보기** 에는 지정된 이벤트 세션의 *여러 .XEL 파일에서 누적된 데이터* 가 표시됩니다. 각 **시작**-**중지** 순환은 해당 이름에 나중 시간에서 파생된 정수가 포함된 파일을 만듭니다. 하지만 각 파일에 동일한 루트 이름을 공유합니다.



#### <a name="b3-watch-live-data"></a>B.3 라이브 데이터 감시


이벤트 세션이 현재 활성 상태인 경우 이벤트 데이터를 대상에서 받은 상태대로 실시간으로 감시하고 싶을 수 있습니다.


- **관리** > **확장 이벤트** > **세션** >  *[your-session]*  > **라이브 데이터 감시**


![세션 > 라이브 데이터 감시](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


데이터 표시가 업데이트되는 간격을 지정할 수 있습니다. 다음에서 **최대 디스패치 대기 시간** 을 참조하세요.

- **확장 이벤트** > **세션** >  *[your-session]*  > **속성** > **고급** > **최대 디스패치 대기 시간**



### <a name="b4-view-xel-with-sysfn_xe_file_target_read_file-function"></a>B.4 sys.fn_xe_file_target_read_file 함수를 사용하여 .XEL 보기


일괄 처리의 경우 다음 시스템 함수는 .XEL 파일의 레코드에 대한 XML을 생성할 수 있습니다.

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>C. 대상 데이터 내보내기


SSMS에서 대상 데이터를 추가한 후에 다음을 수행하여 다양한 형식으로 데이터를 내보낼 수 있습니다.


1. 데이터 표시에 포커스를 둡니다.

    - 갑자기 확장 이벤트에 대한 새 메뉴 항목 및 새 도구 모음이 모두 표시됩니다.

    ![확장 이벤트 > 내보내기 > (.csv, .xel 또는 테이블로)를 통해 표시된 데이터를 내보냅니다.](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. 새 메뉴 항목 **확장 이벤트**를 클릭합니다.
3. **내보내기**를 클릭한 다음 형식을 선택합니다.



## <a name="d-manipulate-data-in-the-display"></a>D. 표시되는 데이터 조작


SSMS UI는 단순히 데이터를 보는 것 외에 데이터를 조작하는 여러 방법을 제공합니다.



### <a name="d1-context-menus-in-the-data-display"></a>D.1 데이터 표시에서 상황에 맞는 메뉴


표시되는 데이터의 다른 위치를 마우스 오른쪽 단추로 클릭하면 상황에 맞는 다른 메뉴가 제공됩니다.



#### <a name="d11-right-click-a-data-cell"></a>D.1.1 데이터 셀을 마우스 오른쪽 단추로 클릭


다음 스크린샷은 데이터 표시에서 셀을 마우스 오른쪽 단추로 클릭하면 나타나는 콘텐츠 메뉴를 보여 줍니다. 또한 스크린샷에서 **복사** 의 확장 메뉴 항목도 보여 줍니다.


![데이터 표시에서 셀을 마우스 오른쪽 단추로 클릭](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>D.1.2 열 머리글을 마우스 오른쪽 단추로 클릭


다음 스크린샷은 **timestamp** 머리글을 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴가 표시되는 것을 보여 줍니다.


![데이터 표시에서 열 머리글을 마우스 오른쪽 단추로 클릭 및 세부 정보 표 표시](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


위 스크린샷에서는 확장 이벤트에 대한 특수한 도구 모음도 보여 줍니다. 세부 정보 단추의 밝기는 단추가 활성화되었음을 나타냅니다. 따라서 이미지에는 **세부 정보** 탭 및 표가 데이터 표시의 두 번째 부분으로 표시되어 있습니다.



### <a name="d2-choose-columns-merge-columns"></a>D.2 열 선택, 열 병합


**열 선택** 옵션으로 데이터 열을 표시 및 표시하지 않도록 제어할 수 있습니다. 다음 위치에서 **열 선택** 메뉴 항목을 찾을 수 있습니다.

- **확장 이벤트** 메뉴
- 확장 이벤트 도구 모음
- 데이터 표시에서 머리글의 상황에 맞는 메뉴


**열 선택**을 클릭하면 동일한 이름의 대화 상자가 표시됩니다.


![열 선택 대화 상자는 열 병합 옵션도 제공합니다.](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>D.2.1 열 병합


**열 선택** 대화 상자에는 아래 작업을 위해 여러 열을 하나로 병합하는 데 사용되는 섹션이 있습니다.

- 표시.
- 내보내기.



### <a name="d3-filters"></a>D.3 필터


확장 이벤트의 영역에서 지정할 수 있는 두 가지 주요 유형의 필터는 다음과 같습니다.

- *사전 대상 필터:* 이벤트 엔진에 의해 대상으로 전송되는 데이터 양을 줄이는 필터입니다.

- *사후 대상 필터:* 일부 대상 레코드를 표시에서 제외할 수 있도록 SSMS UI에서 선택할 수 있는 필터입니다.


SSMS 표시 필터는 다음과 같습니다.

- *timestamp* 열을 검사하는 **시간 범위** 필터
- *열 값* 필터


시간 필터와 열 필터 간의 관계는 부울 '*AND*'입니다.


![필터 대화 상자의 시간 범위 및 열 필터](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>D.4 그룹화 및 집계


데이터의 요약 집계를 위한 첫 단계는 지정된 열에서 값을 일치시켜 행을 그룹화하는 것입니다.



#### <a name="d41-grouping"></a>D.4.1 그룹화


확장 이벤트 도구 모음에서 **그룹화** 단추를 선택하면 지정된 열에 표시된 데이터를 그룹화하는 데 사용할 수 있는 대화 상자가 시작됩니다. 다음 스크린샷은 *이름* 열로 그룹화하는 데 사용되는 대화 상자를 보여 줍니다.

![도구 모음 > 그룹화 단추, 그룹화 대화 상자](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

그룹화가 완료된 후 다음과 같이 새로운 모양으로 표시가 바뀌었습니다.

![그룹화 후 새로운 표시 모양](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>D.4.2 집계


표시된 데이터를 그룹화한 후에 다른 열에서 데이터 집계를 진행할 수 있습니다.  다음은 그룹화된 데이터를 *개수*로 집계하고 있는 스크린샷입니다.

![도구 모음 > 집계 단추, 집계 대화 상자](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

집계를 완료한 후 다음과 같이 새로운 모양으로 표시가 바뀌었습니다.

![도구 모음 > 집계 단추, 집계 대화 상자](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>D.5 런타임 쿼리 계획 보기


**query_post_execution_showplan** 이벤트를 사용하면 SSMS UI에서 실제 쿼리 계획을 볼 수 있습니다. **세부 정보** 창이 표시되면 **쿼리 계획** 탭에서 쿼리 계획 그래프를 볼 수 있습니다. 쿼리 계획에서 노드 위에 포인터를 두면 노드에 대한 속성 이름 및 해당 값의 목록을 볼 수 있습니다.


![하나의 노드에 대한 속성 목록이 있는 쿼리 계획](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)

## <a name="see-also"></a>참고 항목

[XELite: XEL 파일 또는 라이브 SQL 스트림에서 XEvents를 읽을 수 있는 플랫폼 간 라이브러리](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/), 2019년 5월에 릴리스됨.

[Read-SQLXEvent PowerShell cmdlet](https://www.powershellgallery.com/packages/SqlServer), 2019년 7월에 릴리스됨
