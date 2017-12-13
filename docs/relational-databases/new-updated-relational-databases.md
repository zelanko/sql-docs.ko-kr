---
title: "업데이트됨 - 관계형 데이터베이스 문서 | Microsoft Docs"
description: "관계형 데이터베이스 설명서에서 최근에 변경된 업데이트된 콘텐츠의 일부를 표시합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 1fbc7affa833eb34b6e13e28b229d47ac0b05a5c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>새로 추가되었거나 최근에 업데이트됨: 관계형 데이터베이스 문서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-09-28** &nbsp;부터 &nbsp; **2017-12-02**
- *주제 영역:* &nbsp; **관계형 데이터베이스**




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SSMS XEvent Profiler 사용](extended-events/use-the-ssms-xe-profiler.md)
2. [SQL 마법사로 플랫 파일 가져오기](import-export/import-flat-file-wizard.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [tempdb 데이터베이스](#TitleNum_1)
2. [메모리 관리 아키텍처 가이드](#TitleNum_2)
3. [통계](#TitleNum_3)
4. [sp_server_diagnostics (Transact-SQL)](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>1. &nbsp; [tempdb 데이터베이스](databases/tempdb-database.md)

*업데이트됨: 2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 121.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c8bb5f9c40625aaf955295e5b5d03e4257e6c6b 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d  (PR=4039  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=ef1fa818beea435f58986af3379853dc28f5efd8) -->



**tempdb 성능 최적화**

 tempdb 데이터베이스의 크기와 물리적인 배치는 시스템 성능에 영향을 줄 수 있습니다. 예를 들어 tempdb에 대해 정의된 크기가 너무 작으면 사용자가 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작할 때마다 시스템의 처리 로드 중 일부가 작업을 지원하는 데 필요한 크기로 tempdb를 자동 증가시키기 위해 소모될 수 있습니다.

 가능한 경우 [database instant file initialization--../../relational-databases/databases/database-instant-file-initialization.md)를 사용하여 데이터 파일 확장 작업의 성능을 향상시킵니다.

 환경의 일반적인 작업량을 수용할 수 있는 값으로 파일 크기를 설정하여 모든 tempdb 파일에 충분한 공간을 미리 할당합니다. 이렇게 하면 tempdb가 너무 자주 확장되어 성능에 영향을 주는 것을 방지할 수 있습니다. tempdb 데이터베이스가 자동 증가되도록 설정해야 하지만 이 기능은 예기치 않은 예외 발생 시 디스크 공간을 늘리기 위해 사용해야 합니다.

 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)]가 여유 공간이 더 많은 파일에서 할당을 선호하는 비례 채우기 알고리즘을 사용하기 때문에 데이터 파일은 각 [filegroup--../../relational-databases/databases/database-files-and-filegroups.md#filegroups) 내에서 동일한 크기여야 합니다. tempdb를 동일한 크기의 여러 데이터 파일로 나누면 tempdb를 사용하는 작업에서 높은 수준의 병렬 효율성을 얻을 수 있습니다.

 파일 증가분을 적정 크기로 설정하여 tempdb 데이터베이스 파일 증가 단위가 너무 작지 않게 합니다. tempdb에 기록되는 데이터 양에 비해 파일 증가 단위가 너무 작으면 tempdb가 지속적으로 확장되어 성능에 영향을 줍니다.

 현재 tempdb 크기 및 성장 매개 변수를 확인하려면 다음 쿼리를 사용합니다.
```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeinMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-memory-management-architecture-guidememory-management-architecture-guidemd"></a>2. &nbsp; [메모리 관리 아키텍처 가이드](memory-management-architecture-guide.md)

*업데이트됨: 2017-11-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 75.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 dd47431ca47eab16af40e41adaeeaf3fc5fb7461 445f013af3bdad65dd3eaf837db7f744b43e8f97  (PR=4113  ,  Filename=memory-management-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



이전 버전의 SQL Server(..!NCLUDE-NotShown--ssVersion2005--../includes/ssversion2005-md.md)], ..!NCLUDE-NotShown--ssKatmai--../includes/ssKatmai-md.md)] 및 ..!NCLUDE-NotShown--ssKilimanjaro--../includes/ssKilimanjaro-md.md)])에서 메모리 할당은 5가지 메커니즘을 사용하여 수행되었습니다.
-  **단일 페이지 할당자(SPA)**는 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 프로세스에서 8KB 이하인 메모리 할당만 포함합니다. *max server memory(MB)* 및 *min server memory(MB)* 구성 옵션은 SPA가 사용한 실제 메모리의 한계를 결정했습니다. 버퍼 풀은 SPA의 메커니즘이자 동시에 가장 큰 단일 페이지 할당 소비자였습니다.
-  **다중 페이지 할당자(MPA)**: 8KB 이상을 요청하는 메모리 할당입니다.
-  **CLR 할당자**: SQL CLR 힙 및 CLR 초기화 중에 생성되는 전역 할당을 포함합니다.
-  ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 프로세스에서 **[thread stacks--../relational-databases/memory-management-architecture-guide.md#stacksizes)**에 대한 메모리 할당입니다.
-  **직접 Windows 할당(DWA)**: Windows에 직접 요청된 메모리 할당입니다. 여기에는 Windows 힙 사용 및 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 프로세스로 로드되는 모듈에 의한 직접 가상 할당이 포함됩니다. 이러한 메모리 할당 요청의 예로는 확장 저장 프로시저 DLL의 할당, 자동화 프로시저(sp_OA 호출)를 사용하여 만든 개체 및 연결된 서버 공급자의 할당이 있습니다.

..!NCLUDE-NotShown--ssSQL11--../includes/sssql11-md.md)]부터 단일 페이지 할당, 다중 페이지 할당 및 CLR 할당은 모두 **"임의 크기" 페이지 할당자**에 통합되며 *max server memory (MB)* 및 *min server memory (MB)* 구성 옵션에 의해 제어되는 메모리 제한에 포함됩니다. 이 변경으로 인해 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 메모리 관리자를 통과하는 모든 메모리 요구 사항에 대해 보다 정확한 크기 조정 기능이 제공되었습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-statisticsstatisticsstatisticsmd"></a>3. &nbsp; [통계](statistics/statistics.md)

*업데이트됨: 2017-11-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_2) | [다음](#TitleNum_4))

<!-- Source markdown line 48.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1dbe3bd6fdfcd27cf4a597cac5a4a09821b51ba7 971cfccf75fbc8842a0ef020a2bc93992c5f4ad9  (PR=4087  ,  Filename=statistics.md  ,  Dirpath=docs\relational-databases\statistics\  ,  MergeCommitSha40=9fbe5403e902eb996bab0b1285cdade281c1cb16) -->



> [!NOTE]
> NCLUDE - NotShown - ssNoVersion - .. / .. / includes / ssnoversion - md.md)]의 히스토그램은 통계 개체의 키 열 집합에 있는 첫 번째 열의 단일 열에 대해서만 빌드됩니다.

쿼리 최적화 프로그램에서는 히스토그램을 만들기 위해 열 값을 정렬하고 고유한 각 열 값과 일치하는 값의 수를 계산한 다음 열 값을 최대 200개의 연속적인 히스토그램 단계로 집계합니다. 각 히스토그램 단계의 범위는 열 값에서 상한 열 값까지입니다. 범위는 경계 값 자체를 제외하고 경계 값 사이의 모든 가능한 열 값을 포함합니다. 정렬된 열 값 중 가장 낮은 값은 첫 번째 히스토그램 단계의 상한 값입니다.

자세히 살펴보면 NCLUDE-NotShown - ssNoVersion - .. / .. / includes / ssnoversion-md.md)]는 다음과 같은 세 단계로 정렬된 열 값 집합에서 **히스토그램**을 만듭니다.

- **히스토그램 초기화**: 첫 번째 단계에서 정렬된 집합의 시작 부분에서 시작하는 일련의 값이 처리되고 *range_high_key*, *equal_rows*, *range_rows* 및 *distinct_range_rows*의 최대 200개 값이 수집됩니다(이 단계에서 *range_rows* 및 *distinct_range_rows*는 항상 0임). 모든 입력이 모두 소모되거나 200개의 값이 발견되면 첫 번째 단계가 종료됩니다.
- **버킷 병합으로 스캔**: 통계 키의 맨 앞줄에 있는 각 추가 값은 두 번째 단계에서 정렬된 순서로 처리됩니다. 각 연속 값은 마지막 범위에 추가되거나 끝에 있는 새 범위가 작성됩니다(입력 값이 정렬되어 있기 때문에 가능합니다). 새 범위가 만들어지면 한 쌍의 기존 인접 범위가 단일 범위로 축소됩니다. 이러한 범위 쌍은 정보 손실을 최소화하기 위해 선택됩니다. 이 메서드는 히스토그램의 단계 수를 최소화하면서 경계 값 간의 차이를 최대화하기 위해 *최대 차이* 알고리즘을 사용합니다. 범위를 축소한 후 단계 수는 이 단계에서 200으로 유지됩니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-spserverdiagnostics-transact-sqlsystem-stored-proceduressp-server-diagnostics-transact-sqlmd"></a>4. &nbsp; [sp_server_diagnostics(Transact-SQL)](system-stored-procedures/sp-server-diagnostics-transact-sql.md)

*업데이트됨: 2017-11-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_3))

<!-- Source markdown line 157.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d0d97efbb0b16638d0120af9ac5e66ec3bcfa391 b98735ec26a091f8c8c58ca1790243be7942e038  (PR=4052  ,  Filename=sp-server-diagnostics-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=45e4efb7aa828578fe9eb7743a1a3526da719555) -->



아래의 예제 쿼리는 테이블의 요약 출력을 읽습니다.
```sql
SELECT create_time,
       component_name,
       state_desc
FROM SpServerDiagnosticsResult;
```

아래의 예제 쿼리는 테이블의 각 구성 요소의 자세한 출력을 읽습니다.
```sql
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult
where component_name like 'resource'
go

-- Nonpreemptive waits
```







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(3+14): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(87 + 0): **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(5+4): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(2+2): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(10+9): **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(2+4): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(4+2): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(21+0): **SQL 작업 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(5+1): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


