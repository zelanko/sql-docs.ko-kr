---
title: '빠른 시작: SQL Server의 확장 이벤트'
description: 이 빠른 시작은 간단한 성능 모니터링 시스템인 확장 이벤트를 통해 데이터를 수집하여 SQL Server 문제를 모니터링하고 해결하는 데 도움이 됩니다.
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xevents
ms.topic: quickstart
f1_keywords:
- sql11.ssms.XeNewEventSession.General.f1
- sql11.ssms.XeNewEventSession.Events.f1
- sql11.ssms.XeNewEventSession.Targets.f1
- sql11.ssms.XeNewEventSession.Advanced.f1
ms.assetid: 7bb78b25-3433-4edb-a2ec-c8b2fa58dea1
author: MightyPen
ms.author: genemi
ms.reviewer: maghan
ms.date: 04/16/2020
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 37fdafe41500e8b146aed8e9840ee3027cc86281
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481384"
---
# <a name="quickstart-extended-events-in-sql-server"></a>빠른 시작: SQL Server의 확장 이벤트

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

확장 이벤트는 사용자가 SQL Server 문제를 모니터링하고 해결하는 데 필요한 데이터를 수집할 수 있도록 하는 간단한 성능 모니터링 시스템입니다. 확장 이벤트 아키텍처에 대해 자세히 알아보려면 [확장 이벤트 개요](extended-events.md)를 참조하세요.  이 문서는 확장 이벤트를 사용해 본 적이 없고 몇 분 내에 이벤트 세션을 만들려는 SQL 개발자를 대상으로 합니다. 확장 이벤트를 사용하면 SQL 시스템 및 애플리케이션의 내부 작업에 대한 세부 정보를 볼 수 있습니다. 확장 이벤트 세션을 만들 때는 다음을 지정합니다.

- 관심 있는 항목
- 원하는 데이터를 시스템에 보고할 방법

이 문서에서는 다음을 수행합니다.

- 스크린샷을 사용하여 SSMS.exe에서의 클릭을 통해 이벤트 세션을 만드는 방법을 보여 줍니다.
- 해당 Transact-SQL 문과 스크린샷을 관련시킵니다.
- 이벤트 세션에 대한 클릭 및 T-SQL의 용어 및 개념에 대해 자세히 설명합니다.
- 이벤트 세션을 테스트하는 방법을 보여 줍니다.
- 결과에 대한 대체 방법을 설명합니다.
  - 결과의 스토리지 캡처
  - 처리된 결과와 처리되지 않은 결과 비교
  - 다양한 방법 및 다양한 시간 단위의 결과를 보기 위한 도구
- 사용 가능한 모든 이벤트를 검색하는 방법을 보여 줍니다.
- 확장 이벤트를 위한 DMV(동적 관리 뷰)에 포함된 기본 키와 외래 키 관계를 제공합니다.
- 자세한 내용을 볼 수 있는 관련 문서를 소개합니다.

블로그 및 기타 비공식 대화에서는 확장 이벤트를 약어 *xevents* 로 부르기도 합니다.

> [!NOTE]
> 코드 샘플을 포함하여 Azure SQL Database의 확장 이벤트에 대한 자세한 내용은 [SQL Database의 확장 이벤트](/azure/azure-sql/database/xevent-db-diff-from-svr)를 참조하세요.

## <a name="preparations-before-demo"></a>데모 전 준비 작업

예정된 데모를 실제로 수행하기 전에 다음과 같은 사전 지식이 필요합니다.

1. [SSMS(SQL Server Management Studio) 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)

   매월 SSMS의 최신 월별 업데이트를 설치해야 합니다.
2. Microsoft SQL Server 2014 이상에 로그인합니다.
3. 사용자 계정에 [서버 사용 권한](../../t-sql/statements/grant-server-permissions-transact-sql.md)**ALTER ANY EVENT SESSION** 이 있는지 확인합니다.

  확장 이벤트 관련 보안 및 사용 권한에 대한 자세한 내용은 이 문서 뒷부분에 있는 [부록](#appendix1)을 확인하세요.

## <a name="demo-of-ssms-integration"></a>SSMS 통합 데모

SSMS.exe는 확장 이벤트에 대한 최상의 UI(사용자 인터페이스)를 제공합니다. UI를 사용하면 확장 이벤트에 대해 Transact-SQL 또는 DMV(동적 관리 뷰)를 사용할 필요가 없으므로 많은 사용자에게 유용합니다.

이 섹션에서는 확장 이벤트를 만들고 이 이벤트에서 보고하는 데이터를 보는 UI 단계를 볼 수 있습니다. 단계를 마친 후에는 이해도를 높이기 위해 이 단계와 관련된 개념을 읽을 수 있습니다.

### <a name="steps-of-demo"></a>데모 단계

작업을 수행하지 않으려는 경우에도 단계를 이해할 수 있습니다. **새 세션** 대화 상자가 시작됩니다. 다음과 같은 4개의 페이지를 처리합니다.

- 일반
- 이벤트
- 데이터 스토리지
- 고급

추후 SSMS UI가 변경될 경우 텍스트와 지원되는 스크린샷이 약간 달라질 수 있습니다. 불일치하거나 약간 달라진 경우에도 설명에 대한 스크린샷은 유효합니다.

1. SSMS와 연결합니다.

2. 개체 탐색기에서 **관리** > **확장 이벤트** > **새 세션** 을 클릭합니다. 두 개가 서로 비슷하지만 **새 세션 마법사** 보다 **새 세션** 대화 상자를 사용하는 것이 좋습니다.

3. 왼쪽 위에서 **일반** 페이지를 클릭합니다. 그런 다음 *세션 이름* 입력란에 **YourSession** 또는 원하는 이름을 입력합니다. **확인** 단추는 데모 마지막에 눌러야 하므로 아직 누르지 *마세요*.

   ![새 세션 > 일반 > 세션 이름](../../relational-databases/extended-events/media/xevents-session-newsessions-10-general-ssms-yoursessionnode.png)

4. 왼쪽 위에서 **이벤트** 페이지를 클릭한 다음 **선택** 단추를 클릭합니다.

   ![새 세션 > 이벤트 > 선택 > 이벤트 라이브러리, 선택한 이벤트](../../relational-databases/extended-events/media/xevents-session-newsessions-14-events-ssms-rightclick-not-wizard.png)

5. **이벤트 라이브러리** 영역의 드롭다운 목록에서 **이벤트 이름만** 을 선택합니다.
    - 입력란에 **sql** 을 입력하면 *contains* 연산자를 사용하여 사용 가능한 이벤트의 긴 목록을 필터링하고 줄일 수 있습니다.
    - 스크롤하여 **sql_statement_completed** 이벤트를 클릭합니다.
    - 오른쪽 화살표 단추 **>** 를 클릭하여 이벤트를 **선택한 이벤트** 상자로 이동합니다.

6. **이벤트** 페이지에서 맨 오른쪽에 있는 **구성** 단추를 클릭합니다.

   다음 스크린샷은 더 쉽게 볼 수 있도록 왼쪽이 잘려 있어 **이벤트 구성 옵션** 영역을 볼 수 있습니다.

    ![새 세션 > 이벤트 > 구성 > 필터(조건자) > 필드](../../relational-databases/extended-events/media/xevents-session-newsessions-20b-events-ssms-yoursessionnode.png)

7. **필터(조건자)** 탭을 클릭합니다. 그런 다음 **절을 추가하려면 여기를 클릭하세요.** 를 클릭하여 HAVING 절을 포함하는 모든 SQL SELECT 문을 캡처합니다.

8. **필드** 드롭다운 목록에서 **sqlserver.sql_text** 를 선택합니다.
   - **연산자** 에 대해 LIKE 연산자를 선택합니다.
   - **값** 에 **%SELECT%HAVING%** 을 입력합니다.

   > [!NOTE]
   > 이 두 부분의 이름에서 *sqlserver* 는 패키지 이름이고 *sql_text* 는 필드 이름입니다. 이전에 선택한 *sql_statement_completed* 이벤트는 선택한 필드와 같은 패키지에 있어야 합니다.

9. 왼쪽 위에서 **데이터 스토리지** 페이지를 클릭합니다.

10. **대상** 영역에서 **대상을 추가하려면 여기를 클릭하세요.** 를 클릭합니다.
    - **형식** 드롭다운 목록에서 **event_file** 을 선택합니다.
    - 즉, 사용자가 볼 수 있는 파일에 이벤트 데이터가 저장됩니다.
    
    > [!NOTE]
    > SQL Server의 온-프레미스 인스턴스에서 데이터 스토리지 대상으로 Azure Blob Storage를 사용할 수 없습니다.

    ![새 세션 &gt; 데이터 스토리지 &gt; 대상 &gt; 유형 &gt; event_file](../../relational-databases/extended-events/media/xevents-session-newsessions-30-datastorage-ssms-yoursessionnode.png)

11. **속성** 영역의 **서버의 파일 이름** 입력란에 전체 경로 및 파일 이름을 입력합니다.
    - 파일 이름 확장명은 *.xel* 이어야 합니다.
    - 작은 테스트의 파일 크기는 1MB 미만이어야 합니다.

    ![새 세션 > 고급 > 최대 디스패치 대기 시간 > 확인](../../relational-databases/extended-events/media/xevents-session-newsessions-40-advanced-ssms-yoursessionnode.png)

12. 왼쪽 위에서 **고급** 페이지를 클릭합니다.
    - **최대 디스패치 대기 시간** 을 3초 미만으로 줄입니다.
    - 마지막으로 아래쪽의 **확인** 단추를 클릭합니다.

13. **개체 탐색기** 로 돌아가서 **관리** > **세션** 을 확장하고 **YourSession** 에 대한 새 노드를 확인합니다.

    ![개체 탐색기의 관리 > 확장 이벤트 > 세션에 있는 새 *이벤트 세션* YourSession의 노드](../../relational-databases/extended-events/media/xevents-session-newsessions-50-objectexplorer-ssms-yoursessionnode.png)

#### <a name="edit-your-event-session"></a>이벤트 세션 편집

SSMS **개체 탐색기** 에서 해당 노드를 마우스 오른쪽 단추로 클릭하고 **속성** 을 클릭하여 이벤트 세션을 편집할 수 있습니다. 동일한 다중 페이지 대화 상자가 표시됩니다.

### <a name="corresponding-t-sql-for-your-event-session"></a>이벤트 세션에 대한 해당 T-SQL

SSMS UI를 사용하여 이벤트 세션을 만든 T-SQL 스크립트를 생성했습니다. 다음과 같이 생성된 스크립트를 확인할 수 있습니다.

- 세션 노드를 마우스 오른쪽 단추로 클릭하고 **세션 스크립팅** > **CREATE** > **클립보드** 를 클릭합니다.
- 텍스트 편집기에 붙여넣습니다.

다음은 UI를 클릭하여 생성된 *YourSession* 에 대한 T-SQL CREATE EVENT SESSION 문입니다.

```sql
CREATE EVENT SESSION [YourSession]
    ON SERVER
    ADD EVENT sqlserver.sql_statement_completed
    (
        ACTION(sqlserver.sql_text)
        WHERE
        ( [sqlserver].[like_i_sql_unicode_string]([sqlserver].[sql_text], N'%SELECT%HAVING%')
        )
    )
    ADD TARGET package0.event_file
    (SET
        filename = N'C:\Junk\YourSession_Target.xel',
        max_file_size = (2),
        max_rollover_files = (2)
    )
    WITH (
        MAX_MEMORY = 2048 KB,
        EVENT_RETENTION_MODE = ALLOW_MULTIPLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY = 3 SECONDS,
        MAX_EVENT_SIZE = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY = OFF,
        STARTUP_STATE = OFF
    );
GO
```

#### <a name="pre-drop-of-the-event-session"></a>이벤트 세션의 Pre-DROP

이름이 이미 있는 경우 CREATE EVENT SESSION 문 앞에서 DROP EVENT SESSION을 조건부로 실행할 수 있습니다.

```sql
IF EXISTS (SELECT *
      FROM sys.server_event_sessions
      WHERE name = 'YourSession')
BEGIN
    DROP EVENT SESSION YourSession
          ON SERVER;
END
go
```

#### <a name="alter-to-start-and-stop-the-event-session"></a>이벤트 세션을 시작 및 중지하는 ALTER

만들어진 이벤트 세션은 기본적으로 자동으로 실행되지 않습니다. 언제든지 다음 T-SQL ALTER EVENT SESSION 문을 사용하여 이벤트 세션을 시작하거나 중지할 수 있습니다.

```sql
ALTER EVENT SESSION [YourSession]
      ON SERVER
    --ON DATABASE
    STATE = START;   -- STOP;
```

SQL Server 인스턴스가 시작될 때 이벤트 세션이 자동으로 시작되도록 설정할 수 있습니다. CREATE EVENT SESSION의 **STARTUP STATE = ON** 키워드를 참조하세요.

- SSMS UI는 **새 세션** > **일반** 페이지에 해당 확인란을 제공합니다.

## <a name="test-your-event-session"></a>이벤트 세션 테스트

다음 간단한 단계를 통해 이벤트 세션을 테스트합니다.

1. SSMS **개체 탐색기** 에서 이벤트 세션 노드를 마우스 오른쪽 단추로 클릭한 다음 **세션 시작** 을 클릭합니다.
2. 다음 `SELECT...HAVING` 문을 두 번 실행합니다.
    - 두 번 실행 중 `HAVING Count` 값을 2와 3으로 전환하여 사용하는 것이 좋습니다. 이렇게 하면 결과의 차이점을 볼 수 있습니다.
3. 세션 노드를 마우스 오른쪽 단추로 클릭한 다음 **세션 중지** 를 클릭합니다.
4. 다음 하위 섹션에서 [결과 선택 및 확인 방법](#select-the-full-results-xml-37)을 읽어 보세요.

```sql
SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o
            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) >= 3   --2     -- Try both values during session.
    ORDER BY
        c.name;
```

이해를 돕기 위해 앞에서 설명한 SELECT...HAVING의 대략적인 결과를 제공합니다.

```
/*** Approximate output, 6 rows, all HAVING Count >= 3:
name                   Count-Per-Column-Repeated-Name
---------------------  ------------------------------
event_group_type       4
event_group_type_desc  4
event_session_address  5
event_session_id       5
is_trigger_event       4
trace_event_id         3
**_/
```

<a name="select-the-full-results-xml-37"/>

### <a name="select-the-full-results-as-xml"></a>전체 결과를 XML로 선택

SSMS에서 다음 T-SQL SELECT를 실행하여 각 행에서 한 이벤트 항목에 관한 데이터를 제공하는 결과를 반환합니다. CAST AS XML을 사용하면 결과를 쉽게 확인할 수 있습니다.

> [!NOTE]
> 이벤트 시스템은 항상 지정한 _.xel* event_file 파일 이름에 long 형식의 숫자를 추가합니다. 파일에서 다음 SELECT를 실행하기 전에 먼저 시스템에 의해 지정된 전체 이름을 복사하고 SELECT에 붙여넣습니다.

```sql
SELECT
        object_name,
        file_name,
        file_offset,
        event_data,
        'CLICK_NEXT_CELL_TO_BROWSE_XML RESULTS!'
                AS [CLICK_NEXT_CELL_TO_BROWSE_XML_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]
                -- TODO: In ssms.exe results grid, double-click this xml cell!
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\Junk\YourSession_Target_0_131085363367310000.xel',
            null, null, null
        );
```

위의 SELECT는 지정된 이벤트 행의 전체 결과를 확인하는 두 가지 방법을 제공합니다.

- SSMS에서 SELECT를 실행하고 **event_data_XML** 열에서 셀을 클릭합니다. 이 기능은 매우 유용합니다.
- **event_data** 열의 셀에서 긴 XML 문자열을 복사합니다. Notepad.exe와 같은 간단한 텍스트 편집기에 붙여넣고 XML 확장명을 가진 파일에 문자열을 저장합니다. 그런 다음 브라우저에서 .XML 파일을 엽니다.

#### <a name="display-of-results-for-one-event"></a>하나의 이벤트에 대한 결과 표시

다음은 XML 형식으로 결과의 일부를 확인합니다. 여기서는 더 간단히 표시하기 위해 XML을 편집했습니다. `<data name="row_count">` 의 값은 `6`이며 이는 앞에서 표시된 6개의 결과 행에 해당합니다. 또한 전체 SELECT 문도 볼 수 있습니다.

```xml
<event name="sql_statement_completed" package="sqlserver" timestamp="2016-05-24T04:06:08.997Z">
  <data name="duration">
    <value>111021</value>
  </data>
  <data name="cpu_time">
    <value>109000</value>
  </data>
  <data name="physical_reads">
    <value>0</value>
  </data>
  <data name="last_row_count">
    <value>6</value>
  </data>
  <data name="offset">
    <value>0</value>
  </data>
  <data name="offset_end">
    <value>584</value>
  </data>
  <data name="statement">
    <value>SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o

            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) &gt;= 3   --2     -- Try both values during session.
    ORDER BY
        c.name</value>
  </data>
</event>
```

## <a name="ssms-to-display-results"></a>결과를 표시하는 SSMS

SSMS UI에는 확장 이벤트에서 캡처된 데이터를 보는 데 사용할 수 있는 여러 가지 고급 기능이 있습니다. 자세한 내용은 다음을 참조하세요.

- [SQL Server 확장 이벤트의 대상 데이터 고급 보기](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)

기본적으로 상황에 맞는 메뉴 옵션인 **대상 데이터 보기** 및 **라이브 데이터 감시** 에서 시작합니다.

### <a name="view-target-data"></a>대상 데이터 보기

SSMS **개체 탐색기** 에서 이벤트 세션 노드 아래의 대상 노드를 마우스 오른쪽 단추로 클릭할 수 있습니다. 상황에 맞는 메뉴에서 **대상 데이터 보기** 를 클릭합니다. 데이터가 표시됩니다.

이벤트에서 새 데이터가 보고될 때 디스플레이가 업데이트되지 않습니다. 그러나 **대상 데이터 보기** 를 다시 클릭할 수 있습니다.

![대상 데이터 보기, SSMS의 관리 > 확장 이벤트 > 세션 > YourSession > package0.event_file, 마우스 오른쪽 단추 클릭](../../relational-databases/extended-events/media/xevents-viewtargetdata-ssms-targetnode-61.png)

### <a name="watch-live-data"></a>라이브 데이터 감시

SSMS **개체 탐색기** 에서 이벤트 세션 노드를 마우스 오른쪽 단추로 클릭할 수 있습니다. 상황에 맞는 메뉴에서 **라이브 데이터 감시** 를 클릭합니다. 실시간으로 계속 들어오는 데이터를 표시합니다.

![라이브 데이터 감시, SSMS의 관리 > 확장 이벤트 > 세션 > YourSession, 마우스 오른쪽 단추 클릭](../../relational-databases/extended-events/media/xevents-watchlivedata-ssms-yoursessionnode-63.png)

## <a name="scenarios"></a>시나리오

확장 이벤트의 효과적인 사용에 대한 많은 시나리오를 제공합니다. 다음 문서는 쿼리 중 발생한 잠금과 관련된 예제 시나리오를 제공합니다.

다음 문서에서는 잠금 평가에 대한 이벤트 세션 시나리오에 대해 설명합니다. 또한 이 문서에서는 **\@dbid** 사용 및 동적 `EXECUTE (@YourSqlString)` 사용에 대한 고급 기술도 보여 줍니다.

- [가장 많은 잠금이 발생한 개체 찾기](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)
  - 이 시나리오에서는 사용자에게 표시하기 전에 원시 이벤트 데이터를 처리하는 대상 package0.histogram을 사용합니다.
- [잠금을 보유한 쿼리 파악](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)
  - 이 시나리오에서는 이벤트 쌍이 sqlserver.lock_acquire 및 lock_release인 [target package0.pair_matching](/previous-versions/sql/sql-server-2016/ff878062(v=sql.130))을 사용합니다.

## <a name="terms-and-concepts-in-extended-events"></a>확장 이벤트의 용어 및 개념

다음 표에서는 확장 이벤트에 사용된 용어를 나열하고 그 의미를 설명합니다.

| 용어 | Description |
| :--- | :---------- |
| 이벤트 세션 | 하나 이상의 이벤트와 동작 및 대상 등 지원되는 항목에 대한 구성입니다. CREATE EVENT SESSION 문은 각 이벤트 세션을 생성합니다. 이벤트 세션이 원하는 대로 시작 및 중지되도록 변경할 수 있습니다. <br/> <br/> 이벤트 세션을 *세션* 이라고 하는 경우도 있으며 컨텍스트상 구분이 필요한 경우에는 *이벤트 세션* 이라고 합니다. <br/> <br/> 이벤트 세션에 대한 자세한 내용은 다음에서 설명되어 있습니다. [SQL Server 확장 이벤트 세션](../../relational-databases/extended-events/sql-server-extended-events-sessions.md). |
| 이벤트 | 활성 이벤트 세션에서 감시하는 시스템의 특정 항목입니다. <br/> <br/> 예를 들어 *sql_statement_completed* 이벤트는 지정한 T-SQL 문이 완료되는 시점을 나타냅니다. 이벤트는 지속 시간 및 기타 데이터를 보고할 수 있습니다. |
| 대상 | 캡처한 이벤트에서 출력 데이터를 수신하는 항목입니다. 대상은 데이터를 표시합니다. <br/> <br/> 예제에는 *event_file* 및 간편한 메모리 *ring_buffer* 가 있습니다. 조금 더 복잡한 *histogram* 대상은 표시하기 전에 데이터를 일부 처리합니다. <br/> <br/> 모든 대상을 모든 이벤트 세션에 대해 사용할 수 있습니다. 자세한 내용은 [SQL Server에서 확장 이벤트에 대한 대상](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md)을 참조하세요. |
| action | 이벤트에 알려진 필드입니다. 필드의 데이터가 대상으로 전송됩니다. 작업 필드는 *조건자 필터* 와 밀접한 관련이 있습니다. |
| 조건자 필터 | 이벤트 필드의 데이터 테스트는 이벤트 항목 중 관심 있는 하위 집합만 대상으로 전송되도록 하는 데 사용됩니다. <br/> <br/> 예를 들어 T-SQL 문에 *HAVING* 문자열이 포함된 *sql_statement_completed* 이벤트 항목만 필터에 포함할 수 있습니다. |
| 패키지 | 이벤트의 핵심과 관련된 항목 집합의 각 항목에 연결된 이름 한정자입니다. <br/> <br/> 예를 들어 패키지에는 T-SQL 텍스트에 대한 이벤트가 있을 수 있습니다. 하나의 이벤트가 GO로 구분된 일괄 처리의 모든 T-SQL과 관련될 수 있습니다. 한편 개별 T-SQL 문에 대한 이벤트도 있습니다. 또한 모든 T-SQL 문에 대해 시작 및 완료 이벤트가 있습니다. <br/> <br/> 이벤트에 적합한 필드는 이벤트가 있는 패키지에도 있습니다. 대부분의 대상은 *package0* 에 있으며 다른 여러 패키지의 이벤트와 함께 사용됩니다. |

## <a name="how-to-discover-the-available-events-in-packages"></a>패키지에서 사용할 수 있는 이벤트를 검색하는 방법

다음 T-SQL SELECT는 이름에 'sql'이라는 세 자가 포함된 각 사용 가능 이벤트에 대해 행을 반환합니다. 물론 LIKE 값을 편집하여 다른 이벤트 이름을 검색할 수 있습니다. 이 행은 이벤트가 포함된 패키지의 이름을 지정합니다.

```sql
SELECT   -- Find an event you want.
        p.name         AS [Package-Name],
        o.object_type,
        o.name         AS [Object-Name],
        o.description  AS [Object-Descr],
        p.guid         AS [Package-Guid]
    FROM
              sys.dm_xe_packages  AS p
        JOIN  sys.dm_xe_objects   AS o
                ON  p.guid = o.package_guid
    WHERE
        o.object_type = 'event'   --'action'  --'target'
        AND
        p.name LIKE '%'
        AND
        o.name LIKE '%sql%'
    ORDER BY
        p.name, o.object_type, o.name;
```

다음 화면에서는 반환된 행을 보여 주며 여기에서 열 이름 = 값 형식으로 편집합니다. 데이터는 앞의 예제 단계에 사용된 *sql statement_completed* 이벤트에서 가져옵니다. Object-Descr 열에 대한 문장이 특히 유용합니다.

```
Package-Name = sqlserver
object_type  = event
Object-Name  = sql_statement_completed
Object-Descr = Occurs when a Transact-SQL statement has completed.
Package-Guid = 655FD93F-3364-40D5-B2BA-330F7FFB6491
```

### <a name="ssms-ui-for-search"></a>검색을 위한 SSMS UI

다른 검색 옵션은 이전 스크린샷에서 보여 준 SSMS UI **새 세션** > **이벤트** > **이벤트 라이브러리** 대화 상자를 사용하는 것입니다.

### <a name="sql-trace-event-classes-with-extended-events"></a>SQL 추적 이벤트 클래스 및 확장 이벤트

SQL 추적 이벤트 클래스 및 열과 함께 확장 이벤트를 사용하는 설명은 다음에서 제공합니다. [SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)

### <a name="event-tracing-for-windows-etw-with-extended-events"></a>ETW(Windows용 이벤트 추적) 및 확장 이벤트

ETW(Windows용 이벤트 추적)에서 확장 이벤트 사용에 대한 설명은 다음 문서를 참조하세요.

- [Windows용 이벤트 추적 대상](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [확장 이벤트를 사용하여 시스템 작업 모니터링](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)

## <a name="additional-items"></a>추가 항목

이 섹션에서는 몇 가지 기타 항목에 대해 간단하게 설명합니다.

### <a name="event-sessions-installed-with-sql-server"></a>SQL Server와 함께 설치되는 이벤트 세션

SQL Server는 몇 가지 확장 이벤트를 기본으로 제공합니다. 이 확장 이벤트는 모두 SQL 시스템이 시작될 때마다 시작하도록 구성되어 있습니다. 이러한 이벤트 세션은 시스템 오류 발생 시 도움이 되는 데이터를 수집합니다. 이러한 이벤트 세션은 모든 확장 이벤트와 마찬가지로 아주 적은 양의 리소스만 사용하므로 계속 실행하는 것이 좋습니다.

이러한 이벤트 세션은 SSMS **개체 탐색기** 의 **관리** > **확장 이벤트** > **세션** 에서 볼 수 있습니다.  2016년 6월을 기준으로 설치되는 이벤트 세션 목록은 다음과 같습니다.

- AlwaysOn_health
- system_health
- telemetry_events

### <a name="powershell-provider-for-extended-events"></a>확장 이벤트에 대한 PowerShell 공급자

SQL Server PowerShell 공급자를 사용하여 SQL Server 확장 이벤트를 관리할 수 있습니다. 자세한 내용은 다음을 참조하세요. [확장 이벤트에 PowerShell 공급자 사용](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)

### <a name="system-views-for-extended-events"></a>확장 이벤트에 대한 시스템 뷰

확장 이벤트에 대한 시스템 뷰는 다음과 같습니다.

- *카탈로그 뷰:* CREATE EVENT SESSION에서 정의된 이벤트 세션에 대한 정보가 표시됩니다.

- *DMV(동적 관리 뷰):* 현재 실행 중인 이벤트 세션에 대한 정보가 표시됩니다.

[SQL Server 확장 이벤트에 대한 시스템 뷰의 SELECT 및 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) 은 다음에 대한 정보를 제공합니다.

- 뷰를 서로 조인하는 방법
- 뷰의 몇 가지 유용한 SELECT
- 다음 항목 간의 상관 관계:
  - 뷰 열
  - CREATE EVENT SESSION 절
  - SSMS UI 컨트롤

## <a name="appendix-selects-to-ascertain-permission-owner-in-advance"></a><a name="appendix1"></a> 부록: 사용 권한 소유자를 미리 확인하기 위한 SELECT

이 문서에 언급된 사용 권한은 다음과 같습니다.

- ALTER ANY EVENT SESSION
- VIEW SERVER STATE
- CONTROL SERVER

다음 Transact-SQL SELECT 문은 이러한 권한을 가진 사용자를 보고할 수 있습니다.

### <a name="union-direct-permissions-plus-role-derived-permissions"></a>UNION 직접 권한 및 역할에서 파생된 사용 권한

다음 SELECT... UNION ALL 문은 이벤트 세션을 만들고 확장 이벤트에 대한 시스템 카탈로그 뷰를 쿼리하는 데 필요한 사용 권한을 가진 행을 반환합니다.

```sql
-- Ascertain who has the permissions listed in the ON clause.
-- 'CONTROL SERVER' permission includes the permissions
-- 'ALTER ANY EVENT SESSION' and 'VIEW SERVER STATE'.
SELECT
        'Owner-is-Principal'  AS [Type-That-Owns-Permission],
        NULL                  AS [Role-Name],
        prin.name             AS [Owner-Name],

        perm.permission_name
            COLLATE Latin1_General_CI_AS_KS_WS
            AS [Permission-Name]
    FROM
             sys.server_permissions  AS perm
        JOIN sys.server_principals   AS prin

            ON prin.principal_id = perm.grantee_principal_id
    WHERE
        perm.permission_name IN
            ('ALTER ANY EVENT SESSION',
            'VIEW SERVER STATE',
            'CONTROL SERVER')
UNION ALL

-- Plus check for members of the 'sysadmin' fixed server role,
-- because 'sysadmin' includes the 'CONTROL SERVER' permission.
SELECT
        'Owner-is-Role'
        , prin.name  -- [Role-Name]
        , CAST( (IsNull(pri2.name, N'No members'))
            AS nvarchar(128))
        , NULL
    FROM
        sys.server_role_members  AS rolm
        RIGHT OUTER JOIN sys.server_principals    AS prin
            ON prin.principal_id = rolm.role_principal_id
        LEFT OUTER JOIN sys.server_principals     AS pri2
            ON rolm.member_principal_id = pri2.principal_id
    WHERE
        prin.name = 'sysadmin'
    ORDER BY
        1,2,3,4;
```

### <a name="has_perms_by_name-function"></a>HAS_PERMS_BY_NAME 함수

다음 SELECT는 사용 권한을 보고합니다. 기본 제공 함수 [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md)을 사용합니다.

또한 일시적으로 다른 계정에 대한 *가장* 권한이 있는 경우 [EXECUTE AS LOGIN](../../t-sql/statements/execute-as-transact-sql.md) 및 REVERT 문의 주석을 제거하여 다른 계정을 조회할 수 있습니다.

```sql
--EXECUTE AS LOGIN = 'AccountNameHere';
SELECT HAS_PERMS_BY_NAME
    (
       null
       , null
       , 'ALTER ANY EVENT SESSION'
    );
--REVERT;
```

### <a name="security-links"></a>보안 링크

다음은 이러한 SELECT 및 사용 권한과 관련된 문서에 대한 링크입니다.

- 기본 제공 함수 [HAS_PERMS_BY_NAME(Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)에 대한 세부 정보
- [sys.fn_my_permissions(Transact-SQL)](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)
- [GRANT 서버 사용 권한(Transact-SQL)](../../t-sql/statements/grant-server-permissions-transact-sql.md)
- [sys.server_principals(Transact-SQL)](../system-catalog-views/sys-server-principals-transact-sql.md)
- 블로그: [효과적인 데이터베이스 엔진 사용 권한](https://social.technet.microsoft.com/wiki/contents/articles/15180.effective-database-engine-permissions.aspx)
- 모든 SQL Server 사용 권한 계층을 PDF로 표시하는 확대 가능한 [포스터](https://aka.ms/sql-permissions-poster)

## <a name="links-to-supporting-information"></a>지원 정보에 대한 링크

- [sys.fn_xe_file_target_read_file(Transact-SQL)](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)