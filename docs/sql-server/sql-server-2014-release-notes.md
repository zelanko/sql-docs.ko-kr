---
title: "SQL Server 2014 릴리스 정보 | Microsoft 문서"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d6d229c14056f9157bd219ba6cbb7590eb14a7b7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/08/2017

---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
이 릴리스 정보 문서에서는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]을 설치하거나 문제를 해결하기 전에 읽어야 할 알려진 문제에 대해 설명합니다.  
  
## <a name="top"></a>내용  
[1.0 설치하기 전](#BeforeInstall)  
  
[2.0 제품 설명서](#ProdDoc)  
  
[3.0 데이터베이스 엔진](#DBEngine)  
  
[4.0 Reporting Services](#SSRS)  
  
[5.0 Microsoft Azure Virtual Machines의 SQL Server 2014](#AzureVM)  
  
[6.0 Analysis Services](#SSAS)  
  
[7.0 Data Quality Services](#DQS)  
  
[8.0 업그레이드 관리자](#UA)  
  
## <a name="BeforeInstall"></a>1.0 설치하기 전  
  
### <a name="11-limitations-and-restrictions-in-sql-server-2014-rtm"></a>1.1 SQL Server 2014 RTM의 제한 사항  
  
#### <a name="111-general-limitations-and-restrictions"></a>1.1.1 일반 제한 사항  
  
1.  SQL Server 2014 CTP 1에서 SQL Server 2014 RTM으로 업그레이드할 수 없습니다.  
  
2.  SQL Server 2014 CTP 1은 SQL Server 2014 RTM과 함께 설치할 수 없습니다.  
  
3.  SQL Server 2014 CTP 1 데이터베이스를 SQL Server 2014 RTM에 연결하거나 복원할 수 없습니다.  
  
**해결 방법:** 없습니다.  
  
#### <a name="12-considerations-for-upgrading-sql-server-2014-ctp-2-to-sql-server-2014-rtm-and-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2 SQL Server 2014 CTP 2에서 SQL Server 2014 RTM으로 업그레이드하고 SQL Server 2014 RTM에서 SQL Server 2014 CTP 2로 다운그레이드할 때의 고려 사항  
  
#### <a name="121-upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm-is-fully-supported"></a>1.2.1 SQL Server 2014 CTP 2에서 SQL Server RTM으로 업그레이드할 수 있음  
특히 다음을 수행할 수 있습니다.  
  
1.  SQL Server 2014 CTP 2 데이터베이스를 SQL Server 2014 RTM 인스턴스에 연결합니다.  
  
2.  SQL Server 2014 CTP 2에서 만든 데이터베이스 백업을 SQL Server 2014 RTM 인스턴스로 복원합니다.  
  
3.  SQL Server 2014 RTM으로 전체 업그레이드를 수행합니다.  
  
4.  SQL Server 2014 RTM으로 롤링 업그레이드를 수행합니다. 롤링 업그레이드를 시작하기 전에 수동 장애 조치(failover) 모드로 전환해야 합니다. 자세한 내용은 [최소 작동 중지 및 데이터 손실로 가용성 그룹 서버 업그레이드 및 업데이트](http://msdn.microsoft.com/library/dn178483.aspx) 를 참조하십시오.  
  
5.  SQL Server 2014 CTP 2에서 설치된 트랜잭션 성능 컬렉션 집합에 의해 수집된 데이터는 SQL Server 2014 RTM에서 SQL Server Management Studio를 통해 볼 수 없으며 그 반대의 경우도 마찬가지입니다. SQL Server 2014 CTP 2에서 설치된 컬렉션 집합에 의해 수집된 데이터를 보려면 SQL Server 2014 CTP 2에서 SQL Server Management Studio를 사용하고, SQL Server 2014 RTM에서 설치된 컬렉션 집합에 의해 수집된 데이터를 보려면 SQL Server 2014 RTM에서 SQL Server Management Studio를 사용하십시오.  
  
### <a name="122-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2.2 SQL Server 2014 RTM에서 SQL Server 2014 CTP 2로의 다운그레이드  
이는 지원되지 않습니다.  
  
**해결 방법:** 다운그레이드에 대한 해결 방법은 없습니다. SQL Server 2014 RTM으로 업그레이드하기 전에 데이터베이스를 백업하는 것이 좋습니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="13-incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>1.3 SQL Server 2014 미디어/ISO/CAB의 잘못된 버전의 StreamInsight Client  
잘못된 버전의 StreamInsight.msi 및 StreamInsightClient.msi가 SQL Server 미디어/ISO/CAB의 다음 경로에 있습니다(StreamInsight\\\<Architecture\>\\\<Language ID\>).  
  
**해결 방법:** [SQL Server 2014 Feature Pack 다운로드 페이지](http://go.microsoft.com/fwlink/?LinkID=306709)에서 올바른 버전을 다운로드하여 설치합니다.  
  
## <a name="ProdDoc"></a>2.0 제품 설명서  
  
### <a name="21-report-builder-content-is-not-available-in-some-languages"></a>2.1 일부 언어에서 보고서 작성기 콘텐츠를 사용할 수 없음  
**문제:** 보고서 작성기 콘텐츠는 다음 언어에서 사용할 수 없습니다.  
  
-   그리스어(el-GR)  
  
-   노르웨이어(복말)(nb-NO)  
  
-   핀란드어(fi-FI)  
  
-   덴마크어(da-DK)  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서는 제품과 함께 제공된 CHM 파일에서 이 콘텐츠를 이 언어로 볼 수 있었습니다. 그러나 이 CHM 파일은 더 이상 제품과 함께 제공되지 않으며 MSDN에서만 보고서 작성기 콘텐츠를 볼 수 있습니다. MSDN에서는 이러한 언어를 지원하지 않습니다. 보고서 작성기도 TechNet에서 제거되었으며 해당 지원되는 언어로 더 이상 제공되지 않습니다.  
  
**해결 방법:** 없습니다.  
  
### <a name="22-powerpivot-content-is-not-available-in-some-languages"></a>2.2 일부 언어에서 PowerPivot 콘텐츠를 사용할 수 없음  
**문제:** 파워 피벗 콘텐츠는 다음 언어로 제공되지 않습니다.  
  
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
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="DBEngine"></a>3.0 데이터베이스 엔진  
  
### <a name="31-changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>3.1 SQL Server 2014 RTM의 Standard Edition에 대한 변경 사항  
SQL Server 2014 Standard의 변경 사항은 다음과 같습니다.  
  
-   버퍼 풀 확장 기능을 사용하면 최대 4배의 구성된 메모리를 사용할 수 있습니다.  
  
-   최대 메모리가 64GB에서 128GB로 증가했습니다.  
  
### <a name="32-in-memory-oltp-issues"></a>3.2 메모리 내 OLTP 문제  
  
#### <a name="321-memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>3.2.1 메모리 최적화 관리자가 호환되지 않는 것으로 기본 제약 조건에 플래그를 지정함  
**문제:** SQL Server Management Studio에서 메모리 최적화 관리자는 모든 기본 제약 조건에 호환되지 않음 플래그를 지정합니다. 일부 기본 제약 조건은 메모리 액세스에 최적화된 테이블에서 지원되지 않습니다. 메모리 최적화 관리자는 지원되는 유형의 기본 제약 조건과 지원되지 않는 유형의 기본 제약 조건을 구분하지 않습니다. 지원되는 기본 제약 조건에는 고유하게 컴파일된 저장 프로시저 내에서 지원되는 모든 상수, 식 및 기본 제공 함수가 포함됩니다. 고유하게 컴파일된 저장 프로시저에서 지원되는 함수 목록을 보려면 [고유하게 컴파일된 저장 프로시저에서 지원되는 구문](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx)을 참조하세요.  
  
**해결 방법:** 메모리 최적화 관리자를 사용하여 블로커를 식별하려면 호환되는 기본 제약 조건을 무시하시기 바랍니다. 메모리 최적화 관리자를 사용하여 다른 블로커를 제외하고 호환되는 기본 제약 조건이 있는 테이블을 마이그레이션하려면 다음 단계를 수행하십시오.  
  
1.  테이블 정의에서 기본 제약 조건을 제거합니다.  
  
2.  메모리 최적화 관리자를 사용하여 테이블에 대한 마이그레이션 스크립트를 생성합니다.  
  
3.  마이그레이션 스크립트에서 기본 제약 조건을 다시 추가합니다.  
  
4.  마이그레이션 스크립트를 실행합니다.  
  
#### <a name="322-informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>3.2.2 정보 메시지 "파일 액세스 거부됨"이 SQL Server 2014 오류 로그에서 오류로 잘못 보고됨  
**문제:** 메모리 액세스에 최적화된 테이블을 포함하는 데이터베이스가 있는 서버를 다시 시작하면 다음과 같은 유형의 오류 메시지가 SQL Server 2014 오류 로그에 표시될 수 있습니다.  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
  
이 메시지는 사실상 정보 메시지이며 사용자 작업이 필요하지 않습니다.  
  
**해결 방법:** 없습니다. 이 메시지는 정보 제공용입니다.  
  
#### <a name="323-missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>3.2.3 메모리 액세스에 최적화된 테이블의 포함된 열이 누락된 인덱스 정보에서 잘못 보고됨  
**문제:** SQL Server 2014에서는 메모리 액세스에 최적화된 테이블에 대한 쿼리의 누락된 인덱스를 검색하는 경우, 누락된 인덱스를 SHOWPLAN_XML에서 보고하고 sys.dm_db_missing_index_details 등의 누락된 인덱스 DMV에서도 보고합니다. 포함된 열이 누락된 인덱스 정보에 들어 있는 경우도 있습니다. 모든 열이 메모리 액세스에 최적화된 테이블의 모든 인덱스와 함께 암시적으로 포함되므로 메모리 액세스에 최적화된 인덱스를 사용하여 포함된 열을 명시적으로 지정할 수 없습니다.  
  
**해결 방법** : 메모리 액세스에 최적화된 테이블의 인덱스를 사용하여 INCLUDE 절을 지정하지 마세요.  
  
#### <a name="324-missing-index-details-omit-missing-indexes-if-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>3.2.4 해시 인덱스가 있지만 쿼리에 적합하지 않은 경우 누락된 인덱스가 누락된 인덱스 정보에서 생략됨  
**문제:** 쿼리에서 참조되는 메모리 액세스에 최적화된 테이블의 열에 해시 인덱스가 있지만 이 인덱스를 쿼리에 사용할 수 없는 경우, SQL Server 2014에서 누락된 인덱스가 SHOWPLAN_XML과 sys.dm_db_missing_index_details DMV에 보고되지 않을 수도 있습니다.  
  
특히 쿼리에 인덱스 키 열의 하위 집합이 포함된 같음 조건자가 있거나 인덱스 키 열이 포함된 같지 않음 조건자가 있는 경우, 해시 인덱스를 그대로 사용할 수 없으며 쿼리를 효율적으로 실행하려면 다른 인덱스가 필요합니다.  
  
**해결 방법:** 해시 인덱스를 사용하는 경우 쿼리와 쿼리 계획을 조사하여 쿼리에서 인덱스 키의 하위 집합이나 같지 않음 조건자에 대한 Index Seek 연산을 활용할 수 있는지 여부를 확인합니다. 인덱스 키의 하위 집합에서 검색해야 하는 경우, 비클러스터형 인덱스를 사용하거나 검색해야 하는 정확한 열에서 해시 인덱스를 사용합니다. 같지 않음 조건자에서 검색해야 하는 경우에는 해시 대신 비클러스터형 인덱스를 사용합니다.  
  
#### <a name="325-failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>3.2.5 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 경우 메모리 액세스에 최적화된 테이블과 메모리 액세스에 최적화된 테이블 변수를 동일한 쿼리에서 사용하면 실패함  
**문제:** READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 경우, 사용자 트랜잭션 컨텍스트 외부의 동일한 문에서 메모리 액세스에 최적화된 테이블과 메모리 액세스에 최적화된 테이블 변수 둘 다에 액세스하면 다음과 같은 오류 메시지가 나타날 수 있습니다.  
  
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
  
#### <a name="326-procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>3.2.6 고유하게 컴파일된 저장 프로시저의 프로시저 및 쿼리 실행 통계에서 작업자 시간이 1000의 배수로 기록됨  
**문제:** sp_xtp_control_proc_exec_stats 또는 sp_xtp_control_query_exec_stats를 사용하여 고유하게 컴파일된 저장 프로시저에 대한 프로시저 또는 쿼리 실행 통계를 수집하도록 설정한 후, sys.dm_exec_procedure_stats 및 sys.dm_exec_query_stats DMV에서 *_worker_time이 1,000의 배수로 보고됩니다. 작업자 시간이 500마이크로초 미만인 쿼리 실행은 worker_time 0으로 보고됩니다.  
  
**해결 방법:** 없습니다. 고유하게 컴파일된 저장 프로시저의 단기 실행 쿼리에 대한 실행 통계 DMV에 보고되는 worker_time에 의존하지 마십시오.  
  
#### <a name="327-error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>3.2.7 긴 식이 포함된 고유하게 컴파일된 저장 프로시저에 대한 SHOWPLAN_XML의 오류  
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
  
#### <a name="328-using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>3.2.8 고유하게 컴파일된 저장 프로시저에서 DATEPART 및 관련 함수와 함께 문자열 매개 변수 또는 변수를 사용하면 오류가 발생함  
**문제:** 고유하게 컴파일된 저장 프로시저 내에서 DATEPART, DAY, MONTH, YEAR 등의 기본 제공 함수와 함께 (var)char 또는 n(var)char과 같은 문자열 데이터 형식이 있는 매개 변수나 변수를 사용하면, datetimeoffset 데이터 형식이 고유하게 컴파일된 저장 프로시저에서 지원되지 않는다는 오류 메시지가 나타납니다.  
  
**해결 방법:** 문자열 매개 변수 또는 변수를 datetime2 형식의 새로운 변수에 할당하고 DATEPART, DAY, MONTH 또는 YEAR 함수에서 해당 변수를 사용합니다. 예를 들어  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="329-native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>3.2.9 네이티브 컴파일 관리자가 DELETE FROM 절에 플래그를 잘못 지정함  
**문제:** 네이티브 컴파일 관리자가 저장 프로시저 내부의 DELETE FROM 절에 플래그를 호환되지 않는 것으로 잘못 지정합니다.  
  
**해결 방법:** 없습니다.  
  
### <a name="33-register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>3.3 SSMS를 통해 등록하면 일치하지 않는 인스턴스 ID가 있는 DAC 메타데이터가 추가됨  
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
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="SSRS"></a>4.0 Reporting Services  
  
### <a name="41-the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>4.1 SQL Server 2012 Reporting Services 기본 모드 보고서 서버가 SQL Server 2014 Reporting Services SharePoint 구성 요소와 함께 실행될 수 없음  
**문제:**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드 Windows 서비스 ‘SQL Server Reporting Services’(ReportingServicesService.exe)가 시작되지 않습니다.  
  
**해결 방법:** : [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 구성 요소를 제거하고 Microsoft SQL Server 2012 Reporting Services Windows 서비스를 다시 시작합니다.  
  
**추가 정보:**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드는 다음 중 하나와 함께 실행될 수 없습니다.  
  
-   SharePoint 제품용[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스  
  
함께 설치하면 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드 Windows 서비스가 시작되지 않습니다. Windows 이벤트 로그에 다음과 비슷한 오류 메시지가 표시됩니다.  
  
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
  
### <a name="42-required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>4.2 다중 노드 SharePoint 팜을 SQL Server 2014 Reporting Services로 업그레이드하는 데 필요한 순서  
**문제:** SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능의 모든 인스턴스 전에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스의 인스턴스가 업그레이드되면 다중 노드 팜에서 보고서 렌더링이 실패합니다.  
  
**해결 방법:** 다중 노드 SharePoint 팜에서 다음을 수행합니다.  
  
1.  먼저 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능의 모든 인스턴스를 업그레이드합니다.  
  
2.  그런 다음 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스의 모든 인스턴스를 업그레이드합니다.  
  
자세한 내용은 [SQL Server 2014 Reporting Services 팁, 요령 및 문제 해결](http://go.microsoft.com/fwlink/?LinkID=391254)을 참조하십시오.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="AzureVM"></a>5.0 Microsoft Azure Virtual Machines의 SQL Server 2014 RTM  
  
### <a name="51-the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>5.1 Microsoft Azure에서 가용성 그룹 수신기를 구성하면 Azure 복제본 추가 마법사에서 오류를 반환함  
**문제:** 가용성 그룹에 수신기가 있는 경우 Microsoft Azure에서 수신기를 구성하려고 하면 Azure 복제본 추가 마법사에서 오류를 반환합니다.  
  
그 이유는 가용성 그룹 수신기가 Azure 서브넷을 포함하여 가용성 그룹 복제본을 호스팅하는 모든 서브넷에서 IP 주소를 하나씩 할당해야 하기 때문입니다.  
  
**해결 방법:**  
  
1.  수신기 페이지에서 가용성 그룹 복제본을 호스팅할 Azure 서브넷의 사용 가능한 고정 IP 주소를 가용성 그룹 수신기에 할당합니다.  
  
    이렇게 하면 마법사가 Microsoft Azure에서 복제본을 추가하는 작업을 완료할 수 있습니다.  
  
2.  마법사가 완료된 후 [Microsoft Azure에서 AlwaysOn 가용성 그룹을 위한 수신기 구성](http://msdn.microsoft.com/library/dn376546.aspx)에 설명된 대로 Microsoft Azure에서 수신기의 구성을 완료해야 합니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="SSAS"></a>6.0 Analysis Services  
  
### <a name="61-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>6.1 SQL Server 2014에서 구성된 새로운 SharePoint 2010 팜에 대해 MSOLAP.5를 다운로드 및 설치하고 등록해야 함  
**문제점:**  
  
-   SQL Server 2014 RTM 배포에서 구성된 SharePoint 2010 팜의 경우, 연결 문자열에서 참조된 공급자가 설치되지 않았기 때문에 PowerPivot 통합 문서가 데이터 모델에 연결할 수 없습니다.  
  
**해결 방법:**  
  
1.  [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 기능 팩에서 MSOLAP.5 공급자를 다운로드합니다. Excel Services를 실행하는 응용 프로그램 서버에서 공급자를 설치합니다. 자세한 내용은 [Microsoft SQL Server 2012 SP1 기능 팩](http://www.microsoft.com/download/details.aspx?id=35580)의 "Microsoft SQL Server 2012 SP1용 Microsoft Analysis Services OLE DB Provider" 섹션을 참조하십시오.  
  
2.  SharePoint Excel 서비스에서 신뢰할 수 있는 공급자로 MSOLAP.5를 등록합니다. 자세한 내용은 [MSOLAP.5를 Excel 서비스에서 신뢰할 수 있는 데이터 공급자로 추가](http://technet.microsoft.com/library/hh758436.aspx)를 참조하십시오.  
  
**추가 정보:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 에는 MSOLAP.6이 포함되어 있습니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서에서는 MSOLAP.5를 사용합니다. MSOLAP.5가 Excel 서비스를 실행하는 컴퓨터에 설치되어 있지 않으면 Excel 서비스에서 데이터 모델을 로드할 수 없습니다.  
  
### <a name="62-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>6.2 SQL Server 2014에서 구성된 새로운 SharePoint 2013 팜에 대해 MSOLAP.5를 다운로드 및 설치하고 등록해야 함  
**문제점:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 배포에서 구성된 SharePoint 2013 팜의 경우, 연결 문자열에서 참조된 공급자가 설치되지 않았기 때문에 MSOLAP.5 공급자를 참조하는 Excel 통합 문서에서 테이블 형식 데이터 모델에 연결할 수 없습니다.  
  
**해결 방법:**  
  
1.  [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 기능 팩에서 MSOLAP.5 공급자를 다운로드합니다. Excel Services를 실행하는 응용 프로그램 서버에서 공급자를 설치합니다. 자세한 내용은 [Microsoft SQL Server 2012 SP1 기능 팩](http://www.microsoft.com/download/details.aspx?id=35580)의 "Microsoft SQL Server 2012 SP1용 Microsoft Analysis Services OLE DB Provider" 섹션을 참조하십시오.  
  
2.  SharePoint Excel 서비스에서 신뢰할 수 있는 공급자로 MSOLAP.5를 등록합니다. 자세한 내용은 [MSOLAP.5를 Excel 서비스에서 신뢰할 수 있는 데이터 공급자로 추가](http://technet.microsoft.com/library/hh758436.aspx)를 참조하십시오.  
  
**추가 정보:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 에는 MSOLAP.6이 포함되어 있습니다. 그러나 SQL Server 2014 PowerPivot 통합 문서에서는 MSOLAP.5를 사용합니다. MSOLAP.5가 Excel 서비스를 실행하는 컴퓨터에 설치되어 있지 않으면 Excel 서비스에서 데이터 모델을 로드할 수 없습니다.  
  
### <a name="63-corrupt-data-refresh-schedules"></a>6.3 데이터 새로 고침 일정 손상  
**문제점:**  
  
-   새로 고침 일정을 업데이트하면 일정이 손상되어 사용할 수 없게 됩니다.  
  
**해결 방법:**  
  
1.  Microsoft Excel에서 사용자 지정 고급 속성의 선택을 취소합니다. 다음 기술 자료 문서 [KB 2927748](http://support.microsoft.com/kb/2927748)의 “해결 방법” 섹션을 참조하십시오.  
  
**추가 정보:**  
  
-   통합 문서에 대한 데이터 새로 고침 일정을 업데이트할 때 새로 고침 일정의 직렬화된 길이가 원래 일정의 직렬화된 길이보다 짧은 경우 버퍼 크기가 제대로 업데이트되지 않고 새 일정 정보가 이전 일정 정보와 병합되어 일정이 손상됩니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="DQS"></a>7.0 Data Quality Services  
  
### <a name="71-no-cross-version-support-for-data-quality-services-in-master-data-services"></a>7.1 MDS(Master Data Services)의 Data Quality Services에 대한 버전 간 지원 없음  
**문제:** 다음과 같은 시나리오는 지원되지 않습니다.  
  
-   Data Quality Services 2012가 설치된 SQL Server 2012에서 SQL Server 데이터베이스 엔진 데이터베이스에 호스트된 Master Data Services 2014  
  
-   Data Quality Services 2014가 설치된 SQL Server 2014에서 SQL Server 데이터베이스 엔진 데이터베이스에 호스트된 Master Data Services 2012  
  
**해결 방법:** 데이터베이스 엔진 데이터베이스 및 Data Quality Services와 동일한 버전의 Master Data Services를 사용합니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
## <a name="UA"></a>8.0 업그레이드 관리자 문제  
  
### <a name="81--sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>8.1 SQL Server 2014 업그레이드 관리자가 SQL Server Reporting Services에 대해 관련이 없는 업그레이드 문제를 보고함  
**문제:** SQL Server 2014 미디어에서 제공된 SSUA(SQL Server 업그레이드 관리자)가 SQL Server Reporting Services 서버를 분석할 때 여러 오류를 잘못 보고합니다.  
  
**해결 방법:** 이 문제는 [SSUA용 SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709)에서 제공되는 SQL Server 업그레이드 관리자에서 해결되었습니다.  
  
### <a name="82--sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>8.2 SQL Server 2014 업그레이드 관리자가 SQL Server Integration Services 서버를 분석할 때 오류를 보고함  
**문제:** SQL Server 2014 미디어에서 제공된 SSUA(SQL Server 업그레이드 관리자)가 SQL Server Integration Services 서버를 분석할 때 오류를 보고합니다.  사용자에게 표시되는 오류는 다음과 같습니다.  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**해결 방법:** 이 문제는 [SSUA용 SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709)에서 제공되는 SQL Server 업그레이드 관리자에서 해결되었습니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../sql-server/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[맨 위로 이동](#top)  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

