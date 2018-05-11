---
title: SQL Server 2014 릴리스 정보 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2018
ms.prod: sql
ms.prod_service: sql
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: f9a8d57f209e5c8c813fd08c8faff6ce5504c97b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]
이 문서는 관련된 서비스 팩을 포함하여 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 릴리스로 알려진 문제를 설명합니다.

## <a name="sql-server-2014-service-pack-2-sp2"></a>SQL Server 2014 서비스 팩 2(SP2)

SQL Server 2014 SP2는 SQL Server 2014 SP1 CU7에 대해 릴리스된 핫픽스의 롤업을 포함합니다. 성능, 확장성을 중심으로 향상된 기능 및 고객 및 SQL 커뮤니티의 피드백을 기반으로 하는 진단을 포함합니다.

### <a name="performance-and-scalability-improvements-in-sp2"></a>SP2의 향상된 성능 및 확장성

|기능|Description|참조 항목|
|---|---|---|
|자동 소프트 NUMA 분할|NUMA 노드당 8개 이상의 CPU를 보고하는 시스템에 소프트 NUMA를 자동으로 구성할 수 있습니다.|[soft-NUMA(SQL Server)](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)|
|Buffer Pool Extension|8TB 이상으로 SQL Server 버퍼 풀을 확장할 수 있습니다.|[버퍼 풀 확장](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension)|
|동적 메모리 개체 크기 조정| 노드 및 코어 수에 따라 메모리 개체를 동적으로 분할합니다. 이 기능은 추적 플래그 8048 게시물 SQL 2014 SP2의 필요가 없습니다.|[동적 메모리 개체 크기 조정](https://blogs.msdn.microsoft.com/sql_server_team/dynamic-memory-object-scaling/)|
|DBCC CHECK* 명령에 대한 MAXDOP 힌트|이러한 향상은 sp_configure 값이 아닌 MAXDOP 설정을 사용하여 DBCC CHECKDB를 실행하는 데 유용합니다.|[힌트(Transact-SQL) - 쿼리](https://docs.microsoft.com/sql/t-sql/queries/hints-transact-sql-query)|
|SOS_RWLock 스핀 잠금 개선|SOS_RWLock에 대한 스핀 잠금의 필요를 제거하고 대신 메모리 내 OLTP와 유사한 잠금 없는 기술을 사용합니다. |[SOS_RWLock 재설계](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)|
|공간 네이티브 구현|공간 쿼리 성능이 크게 향상합니다.|[SQL Server 2012 및 2014의 공간 성능 향상](https://support.microsoft.com/help/3107399/spatial-performance-improvements-in-sql-server-2012-and-2014)

### <a name="supportability-and-diagnostics-improvements-in-sp2"></a>SP2의 지원 가능성 및 진단 향상

|기능|Description|참조 항목|
|---|---|---|
|AlwaysON 시간 제한 로깅|현재 시간 및 예상된 갱신 시간이 기록되도록 임대 시간 제한 메시지에 대한 새 로깅 기능을 추가했습니다. |[향상된 AlwaysOn 가용성 그룹 임대 시간 제한 진단](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)
|AlwaysON XEvent 및 성능 카운터|AlwaysOn을 사용하여 대기 시간 문제를 해결할 때 진단을 개선하기 위한 새로운 AlwaysON XEvent 및 성능 카운터 |[KB 3107172](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve) 및 [KB 3107400](https://support.microsoft.com/help/3107400/improved-tempdb-spill-diagnostics-in-showplan-xml-schema-in-sql-server)
|변경 내용 추적 정리|새 저장 프로시저 sp_flush_CT_internal_table_on_demand는 요청 시 변경 내용 추적 내부 테이블을 정리합니다.|[KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)
|데이터베이스 복제|새 DBCC 명령을 사용하여 데이터 없이 스키마, 메타데이터 및 통계를 복제하여 기존 프로덕션 데이터베이스의 문제를 해결합니다. 복제된 데이터베이스는 프로덕션 환경에서 사용할 수 없습니다.|[KB 3177838](https://support.microsoft.com/help/3177838/how-to-use-dbcc-clonedatabase-to-generate-a-schema-and-statistics-only)
|DMF 추가|새 DMF sys.dm_db_incremental_stats_properties는 증분 통계에 대한 파티션당 정보를 노출합니다.|[KB 3170114](https://support.microsoft.com/help/3170114/update-to-add-dmf-sys-dm-db-incremental-stats-properties-in-sql-server)
|SQL Server에서 입력 버퍼를 검색하기 위한 DMF|이제 세션/요청(sys.dm_exec_input_buffer)에 대한 입력 버퍼를 검색하기 위한 새 DMF를 사용할 수 있습니다. 이는 DBCC INPUTBUFFER와 기능적으로 동일합니다.|[sys.dm_exec_input_buffer](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql)
|복제를 위한 DROP DDL 지원|트랜잭션 복제 게시에서 아티클로 포함된 테이블을 데이터베이스 및 게시에서 삭제하도록 허용합니다.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)
|SQL 서비스 계정에 대한 IFI 권한|IFI(인스턴트 파일 초기화)가 SQL Server 서비스 시작 시 적용되는지 확인합니다.|[데이터베이스 파일 초기화](https://docs.microsoft.com/sql/relational-databases/databases/database-instant-file-initialization)
|메모리 부여 - 문제 처리|메모리 경합을 방지하도록 해당 메모리 부여를 제한하여 쿼리를 실행하는 동안 진단 힌트를 활용할 수 있습니다.|[KB 3107401](https://support.microsoft.com/help/3107401/new-query-memory-grant-options-are-available-min-grant-percent-and-max)
|연산자당 쿼리 실행 경량 프로파일링 |실제 행 수와 같은 연산자당 쿼리 실행 통계 수집을 최적화합니다.|[개발자 선택 사항: 쿼리 진행률 - 언제, 어디서나](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)
|쿼리 실행 진단|읽은 실제 행은 이제 쿼리 성능 문제 해결을 개선하기 위해 쿼리 실행 계획에서 보고됩니다.|[KB 3107397](https://support.microsoft.com/help/3107397/improved-diagnostics-for-query-execution-plans-that-involve-residual-p)
|tempdb 분산에 대한 쿼리 실행 진단|Hash Warning 및 Sort Warning은 이제 물리적 I/O 통계, 사용되는 메모리 및 영향을 받는 행을 추적하는 추가 열을 갖습니다. |[temptdb 분산 진단 개선](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve)
|Tempdb 지원 가능성 |서버 시작 시 tempdb 파일 수 및 tempdb 데이터 파일 변경 내용에 대한 새 Errorlog 메시지를 사용합니다.|[KB 2963384](https://support.microsoft.com/help/2963384/fix-sql-server-crashes-when-the-log-file-of-tempdb-database-is-full-in)


또한 다음 수정 사항을 참조하세요.
- Xevent 호출 스택은 이제 절대 주소 대신 모듈 이름 및 오프셋을 포함합니다.
- 진단 XE와 DMV 간의 향상된 상관 관계 - Query_hash 및 query_plan_hash는 쿼리를 고유하게 식별하는 데 사용됩니다. DMV에서는 이를 varbinary(8)으로 정의하는 반면 XEvent에서는 UINT64로 정의합니다. SQL 서버에 "서명되지 않은 bigint"가 없으므로 캐스팅이 항상 작동하지는 않습니다. 이러한 향상 기능은 INT64로 정의된 경우를 제외하고 query_hash와 query_plan_hash에 해당하는 새 XEvent 작업/필터 열을 소개합니다. 이 수정 사항으로 XE와 DMV 간에 쿼리의 상관 관계를 지정할 수 있습니다.
- BULK INSERT 및 BCP에서 UTF-8에 대한 지원 - UTF-8 문자 집합으로 인코딩된 데이터 내보내기 및 가져오기에 대한 지원은 이제 BULK INSERT 및 BCP에서 활성화됩니다.

### <a name="download-pages-and-more-information-for-sp2"></a>SP2에 대한 다운로드 페이지 및 추가 정보

- [Microsoft SQL Server 2014용 서비스 팩 2 다운로드](https://www.microsoft.com/download/details.aspx?id=53168)
- [SQL Server 2014 서비스 팩 2 사용 가능](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2012 SP2 Express](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2014 SP2 기능 팩](https://www.microsoft.com/download/details.aspx?id=53164)
- [SQL Server 2014 SP2 보고서 작성기](https://www.microsoft.com/download/details.aspx?id=53163)
- [Microsoft SharePoint용 SQL Server 2014 SP2 Reporting Services 추가 기능](https://www.microsoft.com/download/details.aspx?id=53162)
- [SQL Server 2014 SP2 의미 체계 언어 통계 ](https://www.microsoft.com/download/details.aspx?id=53165)
- [SQL Server 2014 서비스 팩 2 릴리스 정보](https://support.microsoft.com/help/3171021/sql-server-2014-service-pack-2-release-information)

## <a name="sql-server-2014-service-pack-1-sp1"></a>SQL Server 2014 서비스 팩 1(SP1)

SQL Server 2014 SP1은 CU 5를 포함하여 SQL Server 2014 CU 1에서 제공하는 수정 사항뿐만 아니라 SQL Server 2012 SP2에서 이전에 제공한 수정 사항의 롤업을 포함합니다.

> [!NOTE]
> SQL Server 인스턴스에 활성화된 SSISDB 카탈로그가 있고, SP1로 업그레이드할 때 설치 오류가 발생하는 경우 [SQL Server 2014 SP1을 설치할 때 오류 912 또는 3417](https://support.microsoft.com/help/3018269/error-912-or-3417-when-you-install-sql-server-2014-sp1-build-12-0-4050/)에서 이 문제에 대해 설명한 지침을 따릅니다.

### <a name="download-pages-and-more-information-for-sp1"></a>SP1에 대한 다운로드 페이지 및 추가 정보

- [Microsoft SQL Server 2014용 서비스 팩 1 다운로드](https://www.microsoft.com/download/details.aspx?id=46694)
- [SQL Server 2014 서비스 팩 1 릴리스됨 – 업데이트됨](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2014-service-pack-1-has-released-updated/)
- [Microsoft SQL Server 2014 SP1 Express](https://www.microsoft.com/download/details.aspx?id=46697)
- [Microsoft SQL Server 2014 SP1 기능 팩](https://www.microsoft.com/download/details.aspx?id=46696)


## <a name="before-you-install-sql-server-2014-rtm"></a>SQL Server 2014 RTM을 설치하기 전 확인 사항

### <a name="limitations-and-restrictions-in-sql-server-2014-rtm"></a>SQL Server 2014 RTM의 제한 사항

1.  SQL Server 2014 CTP 1에서 SQL Server 2014 RTM으로 업그레이드할 수 없습니다.  
2.  SQL Server 2014 CTP 1은 SQL Server 2014 RTM과 함께 설치할 수 없습니다.  
3.  SQL Server 2014 CTP 1 데이터베이스를 SQL Server 2014 RTM에 연결하거나 복원할 수 없습니다.  

**해결 방법:** 없습니다.

#### <a name="upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm"></a>SQL Server 2014 CTP 2에서 SQL Server RTM으로 업그레이드
업그레이드는 완전히 지원됩니다. 특히 다음을 수행할 수 있습니다.

1.  SQL Server 2014 CTP 2 데이터베이스를 SQL Server 2014 RTM 인스턴스에 연결합니다.    
2.  SQL Server 2014 CTP 2에서 만든 데이터베이스 백업을 SQL Server 2014 RTM 인스턴스로 복원합니다.    
3.  SQL Server 2014 RTM으로 전체 업그레이드를 수행합니다.
4.  SQL Server 2014 RTM으로 롤링 업그레이드를 수행합니다. 롤링 업그레이드를 시작하기 전에 수동 장애 조치(failover) 모드로 전환해야 합니다. 자세한 내용은 [최소 작동 중지 및 데이터 손실로 가용성 그룹 서버 업그레이드 및 업데이트](http://msdn.microsoft.com/library/dn178483.aspx)를 참조하세요.    
5.  SQL Server 2014 CTP 2에서 설치된 트랜잭션 성능 컬렉션 집합에 의해 수집된 데이터는 SQL Server 2014 RTM에서 SQL Server Management Studio를 통해 볼 수 없으며 그 반대의 경우도 마찬가지입니다.
  
#### <a name="downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>SQL Server 2014 RTM에서 SQL Server 2014 CTP 2로의 다운그레이드  
이 작업은 지원되지 않습니다.  
  
**해결 방법:** 다운그레이드에 대한 해결 방법은 없습니다. SQL Server 2014 RTM으로 업그레이드하기 전에 데이터베이스를 백업하는 것이 좋습니다.  
  
#### <a name="incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>SQL Server 2014 미디어/ISO/CAB의 잘못된 버전의 StreamInsight Client  
잘못된 버전의 StreamInsight.msi 및 StreamInsightClient.msi가 SQL Server 미디어/ISO/CAB의 다음 경로에 있습니다(StreamInsight\\\<Architecture\>\\\<Language ID\>).  
  
**해결 방법:** [SQL Server 2014 Feature Pack 다운로드 페이지](http://go.microsoft.com/fwlink/?LinkID=306709)에서 올바른 버전을 다운로드하여 설치합니다.  
  
### <a name="ProdDoc"></a>제품 설명서 RTM
  
일부 언어에서 보고서 작성기 및 PowerPivot 콘텐츠를 사용할 수 없습니다. 

**문제:** 보고서 작성기 콘텐츠는 다음 언어에서 사용할 수 없습니다.  
  
-   그리스어(el-GR)  
-   노르웨이어(복말)(nb-NO)  
-   핀란드어(fi-FI)  
-   덴마크어(da-DK)  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서는 제품과 함께 제공된 CHM 파일에서 이 콘텐츠를 이 언어로 볼 수 있었습니다. 그러나 이 CHM 파일은 더 이상 제품과 함께 제공되지 않으며 MSDN에서만 보고서 작성기 콘텐츠를 볼 수 있습니다. MSDN에서는 이러한 언어를 지원하지 않습니다. 보고서 작성기도 TechNet에서 제거되었으며 해당 지원되는 언어로 더 이상 제공되지 않습니다.  
  
**해결 방법:** 없습니다.  
  
**문제:** PowerPivot 콘텐츠는 다음 언어로 제공되지 않습니다.
  
-   그리스어(el-GR)  
-   노르웨이어(복말)(nb-NO)  
-   핀란드어(fi-FI)  
-   덴마크어(da-DK)  
-   체코어(cs-CZ)  
-   헝가리어(hu-HU)  
-   네덜란드어(네덜란드)(nl-NL)  
-   폴란드어(pl-PL)  
-   스웨덴어(sv-SE)  
-   터키어(tr-TR)  
-   포르투갈어(포르투갈)(pt-PT)  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서는 이 콘텐츠가 TechNet에서 제공되었으며, 해당 언어로 볼 수 있었습니다. 이 콘텐츠가 TechNet에서 제거되었으며 해당 지원되는 언어로 더 이상 제공되지 않습니다.  
  
**해결 방법:** 없습니다.  
  
### <a name="DBEngine"></a>데이터베이스 엔진(RTM)
  
#### <a name="changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>SQL Server 2014 RTM의 Standard Edition에 대한 변경 사항  
SQL Server 2014 Standard의 변경 사항은 다음과 같습니다.  
  
-   버퍼 풀 확장 기능을 사용하면 최대 4배의 구성된 메모리를 사용할 수 있습니다.    
-   최대 메모리가 64GB에서 128GB로 증가했습니다.  
 
#### <a name="memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>메모리 최적화 관리자가 호환되지 않는 것으로 기본 제약 조건에 플래그를 지정함  
**문제:** SQL Server Management Studio에서 메모리 최적화 관리자는 모든 기본 제약 조건에 호환되지 않음 플래그를 지정합니다. 일부 기본 제약 조건은 메모리 액세스에 최적화된 테이블에서 지원되지 않습니다. 메모리 최적화 관리자는 지원되는 유형의 기본 제약 조건과 지원되지 않는 유형의 기본 제약 조건을 구분하지 않습니다. 지원되는 기본 제약 조건에는 고유하게 컴파일된 저장 프로시저 내에서 지원되는 모든 상수, 식 및 기본 제공 함수가 포함됩니다. 고유하게 컴파일된 저장 프로시저에서 지원되는 함수 목록을 보려면 [고유하게 컴파일된 저장 프로시저에서 지원되는 구문](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx)을 참조하세요.  
  
**해결 방법:** 메모리 최적화 관리자를 사용하여 블로커를 식별하려면 호환되는 기본 제약 조건을 무시합니다. 메모리 최적화 관리자를 사용하여 다른 블로커를 제외하고 호환되는 기본 제약 조건이 있는 테이블을 마이그레이션하려면 다음 단계를 수행하십시오.  
  
1.  테이블 정의에서 기본 제약 조건을 제거합니다.    
2.  메모리 최적화 관리자를 사용하여 테이블에 대한 마이그레이션 스크립트를 생성합니다.    
3.  마이그레이션 스크립트에서 기본 제약 조건을 다시 추가합니다.    
4.  마이그레이션 스크립트를 실행합니다.  
  
#### <a name="informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>정보 메시지 "파일 액세스 거부됨"이 SQL Server 2014 오류 로그에서 오류로 잘못 보고됨  

            **문제:** 메모리 최적화 테이블을 포함하는 데이터베이스가 있는 서버를 다시 시작하면 다음과 같은 유형의 오류 메시지가 SQL Server 2014 오류 로그에 표시될 수 있습니다.  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
이 메시지는 사실상 정보 메시지이며 사용자 작업이 필요하지 않습니다.  
  
**해결 방법:** 없습니다. 이 메시지는 정보 제공용입니다.  
  
#### <a name="missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>메모리 최적화 테이블의 포함된 열이 누락된 인덱스 정보에서 잘못 보고됨  

            **문제:** SQL Server 2014에서는 메모리 최적화 테이블에 대한 쿼리의 누락된 인덱스를 검색하는 경우, 누락된 인덱스를 SHOWPLAN_XML에서 보고하고 sys.dm_db_missing_index_details 등의 누락된 인덱스 DMV에서도 보고합니다. 포함된 열이 누락된 인덱스 정보에 들어 있는 경우도 있습니다. 모든 열이 메모리 최적화 테이블의 모든 인덱스와 함께 암시적으로 포함되므로 메모리 최적화 인덱스를 사용하여 포함된 열을 명시적으로 지정할 수 없습니다.  
  

            **해결 방법** : 메모리 최적화 테이블의 인덱스를 사용하여 INCLUDE 절을 지정하지 마세요.  
  
#### <a name="missing-index-details-omit-missing-indexes-when-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>해시 인덱스가 있지만 쿼리에 적합하지 않은 경우 누락된 인덱스가 누락된 인덱스 정보에서 생략됨  

            **문제:** 쿼리에서 참조되는 메모리 최적화 테이블의 열에 해시 인덱스가 있지만 이 인덱스를 쿼리에 사용할 수 없는 경우, SQL Server 2014에서 누락된 인덱스가 SHOWPLAN_XML과 sys.dm_db_missing_index_details DMV에 보고되지 않을 수도 있습니다.  
  
특히 쿼리에 인덱스 키 열의 하위 집합이 포함된 같음 조건자가 있거나 인덱스 키 열이 포함된 같지 않음 조건자가 있는 경우, 해시 인덱스를 그대로 사용할 수 없으며 쿼리를 효율적으로 실행하려면 다른 인덱스가 필요합니다.  
  
**해결 방법:** 해시 인덱스를 사용하는 경우 쿼리와 쿼리 계획을 조사하여 쿼리에서 인덱스 키의 하위 집합이나 같지 않음 조건자에 대한 Index Seek 연산을 활용할 수 있는지 여부를 확인합니다. 인덱스 키의 하위 집합에서 검색해야 하는 경우, 비클러스터형 인덱스를 사용하거나 검색해야 하는 정확한 열에서 해시 인덱스를 사용합니다. 같지 않음 조건자에서 검색해야 하는 경우에는 해시 대신 비클러스터형 인덱스를 사용합니다.  
  
#### <a name="failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 경우 메모리 최적화 테이블과 메모리 최적화 테이블 변수를 동일한 쿼리에서 사용하면 실패함  

            **문제:** READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 경우, 사용자 트랜잭션 컨텍스트 외부의 동일한 문에서 메모리 최적화 테이블과 메모리 최적화 테이블 변수 둘 다에 액세스하면 다음과 같은 오류 메시지가 나타날 수 있습니다.  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**해결 방법** : 테이블 변수와 함께 테이블 힌트 WITH (SNAPSHOT)을 사용하거나, 다음 문을 사용하여 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 데이터베이스 옵션을 ON으로 설정합니다.  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>고유하게 컴파일된 저장 프로시저의 프로시저 및 쿼리 실행 통계에서 작업자 시간이 1000의 배수로 기록됨  
**문제:** sp_xtp_control_proc_exec_stats 또는 sp_xtp_control_query_exec_stats를 사용하여 고유하게 컴파일된 저장 프로시저에 대한 프로시저 또는 쿼리 실행 통계를 수집하도록 설정한 후, sys.dm_exec_procedure_stats 및 sys.dm_exec_query_stats DMV에서 *_worker_time이 1,000의 배수로 보고됩니다. 작업자 시간이 500마이크로초 미만인 쿼리 실행은 worker_time 0으로 보고됩니다.  
  
**해결 방법:** 없습니다. 고유하게 컴파일된 저장 프로시저의 단기 실행 쿼리에 대한 실행 통계 DMV에 보고되는 worker_time에 의존하지 마십시오.  
  
#### <a name="error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>긴 식이 포함된 고유하게 컴파일된 저장 프로시저에 대한 SHOWPLAN_XML의 오류  
**문제:** 고유하게 컴파일된 저장 프로시저에 긴 식이 포함된 경우, T-SQL 옵션 SET SHOWPLAN_XML ON을 사용하거나 Management Studio에서 '예상 실행 계획 표시' 옵션을 사용하여 프로시저에 대한 SHOWPLAN_XML을 가져오면 다음과 같은 오류가 발생할 수 있습니다.  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**해결 방법:** 다음의 두 가지 해결 방법이 권장됩니다.  
  
1.  다음 예와 유사하게 식에 괄호를 추가합니다.  
  
    다음 식을 사용하는 대신  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    다음과 같은 식을 작성합니다.  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  실행 계획용으로 약간 단순화된 식을 사용하여 두 번째 프로시저를 만듭니다. 계획의 일반적인 모양이 동일해야 합니다. 예를 들어 다음 식을 사용하는 대신  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    다음과 같은 식을 작성합니다.  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>고유하게 컴파일된 저장 프로시저에서 DATEPART 및 관련 함수와 함께 문자열 매개 변수 또는 변수를 사용하면 오류가 발생함  
**문제:** DATEPART, DAY, MONTH, YEAR 등의 기본 제공 함수와 함께 문자열 매개 변수나 변수를 사용하는 고유하게 컴파일된 저장 프로시저를 사용하는 경우 datetimeoffset이 고유하게 컴파일된 저장 프로시저에서 지원되지 않는다는 오류 메시지가 나타납니다.  
  
**해결 방법:** 문자열 매개 변수 또는 변수를 datetime2 형식의 새로운 변수에 할당하고 DATEPART, DAY, MONTH 또는 YEAR 함수에서 해당 변수를 사용합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>네이티브 컴파일 관리자가 DELETE FROM 절에 플래그를 잘못 지정함  
**문제:** 네이티브 컴파일 관리자가 저장 프로시저 내부의 DELETE FROM 절에 플래그를 호환되지 않는 것으로 잘못 지정합니다.  
  
**해결 방법:** 없습니다.  
  
#### <a name="register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>SSMS를 통해 등록하면 일치하지 않는 인스턴스 ID가 있는 DAC 메타데이터가 추가됨  
**문제:** SQL Server Management Studio를 통해 데이터 계층 응용 프로그램 패키지(.dacpac)를 등록하거나 삭제할 때 sysdac * 테이블이 제대로 업데이트되지 않아 사용자가 데이터베이스에 대한 dacpac 기록을 쿼리할 수 없게 됩니다.  instance_id for sysdac_history_internal 및 sysdac_instances_internal이 일치하지 않아 조인이 허용되지 않습니다.  
  
**해결 방법** : 이 문제는 [데이터 계층 응용 프로그램 프레임워크](https://www.microsoft.com/download/details.aspx?id=42295)의 Feature Pack을 재배포하면 해결됩니다.  업데이트가 적용된 후 모든 새 기록 항목은 sysdac_instances_internal 테이블에서 instance_id에 대해 나열된 값을 사용합니다.  
  
일치하지 않는 instance_id 값 문제가 이미 발생한 경우 일치하지 않는 값을 수정하는 유일한 방법은 MSDB 데이터베이스에 쓸 수 있는 권한을 가진 사용자로 서버에 연결하고 instance_id 값을 일치하도록 업데이트하는 것입니다.  동일한 데이터베이스에 대해 등록 및 등록 취소 이벤트가 여러 번 발생한 경우 시간/날짜를 확인하여 현재 instance_id 값과 일치하는 레코드가 무엇인지 파악해야 할 수 있습니다.  
  
1.  MSDB 업데이트 권한이 있는 로그인을 사용하여 SQL Server Management Studio에서 서버에 연결합니다.    
2.  MSDB 데이터베이스를 사용하여 새 쿼리를 엽니다.    
3.  이 쿼리를 실행하여 활성 dac 인스턴스를 모두 확인합니다.  수정할 인스턴스를 찾고 instance_id를 기록해 둡니다.  
  
    `select * from` sysdac_instances_internal  
  
4.  다음 쿼리를 실행하여 모든 기록 항목을 확인합니다.  
  
    `select * from` sysdac_history_internal  
  
5.  수정할 인스턴스에 해당하는 행을 식별합니다. 
6.  sysdac_history_internal.instance_id 값을 3단계에서 기록해 놓은 값(sysdac_instances_internal 테이블의 값)으로 업데이트합니다.  
  
    `update` sysdac_history_internal `set` instance_id = '\<3단계의 값\>' `where` \<업데이트할 행과 일치하는 식\>  
  
### <a name="SSRS"></a>Reporting Services(RTM)
  
#### <a name="the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>SQL Server 2012 Reporting Services 기본 모드 보고서 서버가 SQL Server 2014 Reporting Services SharePoint 구성 요소와 함께 실행될 수 없음  
**문제:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 구성 요소가 동일한 서버에 설치되어 있으면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드 Windows 서비스 ‘SQL Server Reporting Services’(ReportingServicesService.exe)가 시작되지 않습니다.  
  
**해결 방법:** : [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 구성 요소를 제거하고 Microsoft SQL Server 2012 Reporting Services Windows 서비스를 다시 시작합니다.  
  
**추가 정보:**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드는 다음 조건 중 하나와 함께 실행될 수 없습니다.  
  
-   SharePoint 제품용[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능    
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스  
  
함께 설치하면 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드 Windows 서비스가 시작되지 않습니다. Windows 이벤트 로그에 여기에 표시된 것과 비슷한 오류 메시지가 표시됩니다.  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
자세한 내용은 [SQL Server 2014 Reporting Services 팁, 요령 및 문제 해결](http://go.microsoft.com/fwlink/?LinkID=391254)을 참조하십시오.  
  
#### <a name="required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>다중 노드 SharePoint 팜을 SQL Server 2014 Reporting Services로 업그레이드하는 데 필요한 순서  
**문제:** SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능의 모든 인스턴스 전에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스의 인스턴스가 업그레이드되면 다중 노드 팜에서 보고서 렌더링이 실패합니다.  
  
**해결 방법:** 다중 노드 SharePoint 팜에서 다음을 수행합니다.  
  
1.  먼저 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능의 모든 인스턴스를 업그레이드합니다.    
2.  그런 다음 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스의 모든 인스턴스를 업그레이드합니다.  
  
자세한 내용은 [SQL Server 2014 Reporting Services 팁, 요령 및 문제 해결](http://go.microsoft.com/fwlink/?LinkID=391254)을 참조하십시오.  
  
### <a name="AzureVM"></a>Microsoft Azure Virtual Machines의 SQL Server 2014 RTM  
  
#### <a name="the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>Microsoft Azure에서 가용성 그룹 수신기를 구성하면 Azure 복제본 추가 마법사에서 오류를 반환함  
**문제:** 가용성 그룹에 수신기가 있는 경우 Microsoft Azure에서 수신기를 구성하려고 하면 Azure 복제본 추가 마법사에서 오류를 반환합니다.  
  
이 문제는 가용성 그룹 수신기가 Azure 서브넷을 포함하여 가용성 그룹 복제본을 호스팅하는 모든 서브넷에서 IP 주소를 하나씩 할당해야 하기 때문입니다.  
  
**해결 방법:**  
  
1.  수신기 페이지에서 가용성 그룹 복제본을 호스팅할 Azure 서브넷의 사용 가능한 고정 IP 주소를 가용성 그룹 수신기에 할당합니다.  
  
    이렇게 하면 마법사가 Microsoft Azure에서 복제본을 추가하는 작업을 완료할 수 있습니다.  
  
2.  마법사가 완료된 후 [Microsoft Azure에서 AlwaysOn 가용성 그룹을 위한 수신기 구성](http://msdn.microsoft.com/library/dn376546.aspx)에 설명된 대로 Microsoft Azure에서 수신기의 구성을 완료해야 합니다.  
  
### <a name="SSAS"></a>Analysis Services(RTM)
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>SQL Server 2014에서 구성된 새로운 SharePoint 2010 팜에 대해 MSOLAP.5를 다운로드 및 설치하고 등록해야 함  
**문제점:**  
  
-   SharePoint 2010의 경우 SQL Server 2014 RTM 배포에서 구성된 SQL Server 2014 팜에서 구성된 새로운 SharePoint 2013 팜에 대해 MSOLAP.5를 다운로드 및 설치하고 등록해야 합니다. 연결 문자열에서 참조된 공급자가 설치되지 않았기 때문에 PowerPivot 통합 문서가 데이터 모델에 연결할 수 없습니다.  
  
**해결 방법:**  
  
1.  [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 기능 팩에서 MSOLAP.5 공급자를 다운로드합니다. Excel Services를 실행하는 응용 프로그램 서버에서 공급자를 설치합니다. 자세한 내용은 [Microsoft SQL Server 2012 SP1 기능 팩](http://www.microsoft.com/download/details.aspx?id=35580)의 "Microsoft SQL Server 2012 SP1용 Microsoft Analysis Services OLE DB Provider" 섹션을 참조하십시오.  
  
2.  SharePoint Excel 서비스에서 신뢰할 수 있는 공급자로 MSOLAP.5를 등록합니다. 자세한 내용은 [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx)을 참조하세요.  
  
**추가 정보:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 에는 MSOLAP.6이 포함되어 있습니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서에서는 MSOLAP.5를 사용합니다. MSOLAP.5가 Excel 서비스를 실행하는 컴퓨터에 설치되어 있지 않으면 Excel 서비스에서 데이터 모델을 로드할 수 없습니다.  
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>SQL Server 2014에서 구성된 새로운 SharePoint 2013 팜에 대해 MSOLAP.5를 다운로드 및 설치하고 등록해야 함  
**문제점:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 배포에서 구성된 SharePoint 2013 팜의 경우, 연결 문자열에서 참조된 공급자가 설치되지 않았기 때문에 MSOLAP.5 공급자를 참조하는 Excel 통합 문서에서 테이블 형식 데이터 모델에 연결할 수 없습니다.  
  
**해결 방법:**  
  
1.  [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 기능 팩에서 MSOLAP.5 공급자를 다운로드합니다. Excel Services를 실행하는 응용 프로그램 서버에서 공급자를 설치합니다. 자세한 내용은 [Microsoft SQL Server 2012 SP1 기능 팩](http://www.microsoft.com/download/details.aspx?id=35580)의 "Microsoft SQL Server 2012 SP1용 Microsoft Analysis Services OLE DB Provider" 섹션을 참조하십시오.  
  
2.  SharePoint Excel 서비스에서 신뢰할 수 있는 공급자로 MSOLAP.5를 등록합니다. 자세한 내용은 [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx)을 참조하세요.  
  
**추가 정보:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 에는 MSOLAP.6이 포함되어 있습니다. 그러나 SQL Server 2014 PowerPivot 통합 문서에서는 MSOLAP.5를 사용합니다. MSOLAP.5가 Excel 서비스를 실행하는 컴퓨터에 설치되어 있지 않으면 Excel 서비스에서 데이터 모델을 로드할 수 없습니다.  
  
#### <a name="corrupt-data-refresh-schedules-rtm"></a>데이터 새로 고침 일정 손상(RTM)
**문제점:**  
  
-   새로 고침 일정을 업데이트하면 일정이 손상되어 사용할 수 없게 됩니다.  
  
**해결 방법:**  
  
1.  Microsoft Excel에서 사용자 지정 고급 속성의 선택을 취소합니다. 다음 기술 자료 문서 [KB 2927748](http://support.microsoft.com/kb/2927748)의 “해결 방법” 섹션을 참조하세요.  
  
**추가 정보:**  
  
-    통합 문서에 대한 데이터 새로 고침 일정을 업데이트할 때 새로 고침 일정의 직렬화된 길이가 원래 일정의 직렬화된 길이보다 짧은 경우 버퍼 크기가 제대로 업데이트되지 않고 새 일정 정보가 이전 일정 정보와 병합되어 일정이 손상됩니다.  
  
### <a name="DQS"></a>Data Quality Services(RTM)
  
#### <a name="no-cross-version-support-for-data-quality-services-in-master-data-services"></a>MDS(Master Data Services)의 Data Quality Services에 대한 버전 간 지원 없음  
**문제:** 다음과 같은 시나리오는 지원되지 않습니다.  
  
-   Data Quality Services 2012가 설치된 SQL Server 2012에서 SQL Server 데이터베이스 엔진 데이터베이스에 호스트된 Master Data Services 2014  
  
-   Data Quality Services 2014가 설치된 SQL Server 2014에서 SQL Server 데이터베이스 엔진 데이터베이스에 호스트된 Master Data Services 2012  
  
**해결 방법:** 데이터베이스 엔진 데이터베이스 및 Data Quality Services와 동일한 버전의 Master Data Services를 사용합니다.  
  
### <a name="UA"></a>업그레이드 관리자 문제(RTM)
  
#### <a name="sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>SQL Server 2014 업그레이드 관리자가 SQL Server Reporting Services에 대해 관련이 없는 업그레이드 문제를 보고함  
**문제:** SQL Server 2014 미디어에서 제공된 SSUA(SQL Server 업그레이드 관리자)가 SQL Server Reporting Services 서버를 분석할 때 여러 오류를 잘못 보고합니다.  
  
**해결 방법:** 이 문제는 [SSUA용 SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709)에서 제공되는 SQL Server 업그레이드 관리자에서 해결되었습니다.  
  
#### <a name="sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>SQL Server 2014 업그레이드 관리자가 SQL Server Integration Services 서버를 분석할 때 오류를 보고함  
**문제:** SQL Server 2014 미디어에서 제공된 SSUA(SQL Server 업그레이드 관리자)가 SQL Server Integration Services 서버를 분석할 때 오류를 보고합니다.  사용자에게 표시되는 오류는 다음과 같습니다.  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**해결 방법:** 이 문제는 [SSUA용 SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709)에서 제공되는 SQL Server 업그레이드 관리자에서 해결되었습니다.  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]