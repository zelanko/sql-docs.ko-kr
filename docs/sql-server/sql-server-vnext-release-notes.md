---
title: "SQL Server vNext 릴리스 정보 | Microsoft Docs"
ms.custom: ""
ms.date: "03/12/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: "craigg-msft"
ms.author: "craigg"
manager: "jhubbard"
caps.handback.revision: 39
---
# SQL Server vNext 릴리스 정보
이 항목에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 관련 제한 사항 및 문제에 대해 설명합니다.

- 이 릴리스의 새로운 기능을 검토하려면 [SQL Server vNext의 새로운 기능](../sql-server/what-s-new-in-sql-server-vnext.md)을 참조하세요.
- [SQL Server on Linux Release notes](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)(Linux 기반 SQL Server 릴리스 정보)는 새로운 설명서 플랫폼에 게시됩니다.
- [SQL Server Reporting Services 릴리스 정보](../reporting-services/reporting-services-릴리스-정보.md)는 Reporting Services 섹션 내에서 게시됩니다.

 **사용해보기:**    
   -   [![평가 센터에서 다운로드](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[평가 센터](http://go.microsoft.com/fwlink/?LinkID=829477)**에서 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 다운로드


## <a name="sql-server-vnext-ctp-13-february--2017"></a>SQL Server vNext CTP 1.3(2017년 2월)
### <a name="supported-installation-scenarios-ctp-13"></a>지원되는 설치 시나리오(CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]는 테스트 버전으로만 제공됩니다.  프로덕션 배포는 지원되지 않습니다. [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]은 가상 컴퓨터에 설치하고 테스트하는 것이 좋습니다.

### <a name="documentation-ctp-13"></a>설명서(CTP 1.3)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SSIS(SQL Server Integration Services)(CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>이 CTP 릴리스에서는 CDC 구성 요소가 지원되지 않음
-   **문제 및 고객에게 미치는 영향**: 이 CTP 릴리스에서는 CDC 제어 작업, CDC 소스 및 CDC 분할자가 지원되지 않습니다.
-   **해결 방법**: 해결 방법이 없습니다.


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-12-january--2017"></a>SQL Server vNext CTP 1.2(2017년 1월)
### <a name="supported-installation-scenarios-ctp-12"></a>지원되는 설치 시나리오(CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]는 테스트 버전으로만 제공됩니다.  프로덕션 배포는 지원되지 않습니다. [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]은 가상 컴퓨터에 설치하고 테스트하는 것이 좋습니다.

### <a name="sql-server-database-engine-ctp-12"></a>SQL Server 데이터베이스 엔진(CTP 1.2)
- **문제 및 고객에게 미치는 영향:** 일부 경우에 MSSQLSERVER 서비스가 "시작 중" 상태에서 중단됩니다.
- **해결 방법:** 이 문제를 해결하려면
  -  `mssqlserver` 서비스 및 `keyiso` 서비스 간에 종속성을 만듭니다. 이 작업을 수행하는 한 가지 방법은 관리자 권한 명령 프롬프트에서 다음 명령을 실행하는 것입니다. `sc config mssqlserver depend= keyiso`
  - 컴퓨터를 다시 부팅합니다.

### <a name="documentation-ctp-12"></a>설명서(CTP 1.2)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SSIS(SQL Server Integration Services)(CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>SSIS 규모 확장이 설치되어 있으면 SSIS 카탈로그가 삭제되지 않을 수 있음
**문제 및 고객에게 미치는 영향:** SSIS 규모 확장 기능이 컴퓨터에 설치되어 있는 경우 "사용자가 현재 로그인되어 있기 때문에 *'login'* 로그인을 삭제할 수 없습니다."라는 오류가 발생하고 SSISDB 카탈로그 데이터베이스가 삭제되지 않을 수 있습니다.
   
**해결 방법**:
-   규모 확장 마스터 컴퓨터에서 "services.msc" 명령을 실행하여 서비스 창을 엽니다. SQL Server Integration Services 클러스터 마스터 서비스를 중지합니다.
-   마스터에 연결된 규모 확장 작업자 컴퓨터에서 "services.msc" 명령을 실행하여 서비스 창을 엽니다. SQL Server Integration Services 클러스터 작업자 서비스를 중지합니다.

이제 SSISDB 카탈로그 데이터베이스를 삭제할 수 있습니다.

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services(CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>엔터티 트랜잭션 로그 유형이 특성으로 설정되어 있으면 트랜잭션이 작동하지 않을 수 있음
**문제 및 고객에게 미치는 영향:** 엔터티 트랜잭션 로그 유형이 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에서 **특성**(기본값: **멤버**)으로 설정되어 있으면 다음 시나리오가 실패합니다.

* 엔터티 변경에 대한 트랜잭션이 웹 사이트에 표시되지 않습니다.
* 웹 사이트에서 **트랜잭션** 페이지를 열고 트랜잭션을 되돌릴 수 없습니다.
* 웹 사이트에서 트랜잭션 주석을 사용하여 엔터티를 업데이트할 수 없습니다.

**해결 방법**: 해결 방법이 없습니다.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>**커밋된 버전만 복사**가 false로 설정되어 있으면 버전 복사가 작동하지 않을 수 있음
-  **문제 및 고객에게 미치는 영향:** **커밋된 버전만 복사** 설정이 **아니요**(기본값: **예**)로 설정되어 있으면 버전 복사 작업이 실패할 수 있습니다. 오류 메시지가 없습니다.
-  **해결 방법**: 해결 방법이 없습니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-11-december--2016"></a>SQL Server vNext CTP 1.1(2016년 12월)
### <a name="supported-installation-scenarios-ctp-11"></a>지원되는 설치 시나리오(CTP 1.1)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]는 테스트 버전으로만 제공됩니다.  프로덕션 배포는 지원되지 않습니다. [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]은 가상 컴퓨터에 설치하고 테스트하는 것이 좋습니다.

특히 다음과 같은 시나리오가 사용될 수 있지만 철저히 테스트되지 않았으며 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에서 지원되지 **않습니다**.
- CTP 1.1 제거
- 다른 버전의 SQL Server와 함께 병렬 설치
- 이전 버전의 SQL Server에서 업그레이드
- [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 설치의 일부로 SQL Server 기능 팩 구성 요소를 사용할 수 없음

### <a name="documentation-ctp-11"></a>설명서(CTP 1.1)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-master-data-services-ctp-11"></a>SQL Server Master Data Services(CTP 1.1)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>엔터티 트랜잭션 로그 유형이 특성으로 설정되어 있으면 트랜잭션이 작동하지 않을 수 있음
**문제 및 고객에게 미치는 영향:** 엔터티 트랜잭션 로그 유형이 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에서 **특성**(기본값: **멤버**)으로 설정되어 있으면 다음 시나리오가 실패합니다.

* 엔터티 변경에 대한 트랜잭션이 웹 사이트에 표시되지 않습니다.
* 웹 사이트에서 **트랜잭션** 페이지를 열고 트랜잭션을 되돌릴 수 없습니다.
* 웹 사이트에서 트랜잭션 주석을 사용하여 엔터티를 업데이트할 수 없습니다.

**해결 방법**: 해결 방법이 없습니다.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>**커밋된 버전만 복사**가 false로 설정되어 있으면 버전 복사가 작동하지 않을 수 있음
-  **문제 및 고객에게 미치는 영향:** **커밋된 버전만 복사** 설정이 **아니요**(기본값: **예**)로 설정되어 있으면 버전 복사 작업이 실패할 수 있습니다. 오류 메시지가 없습니다.
-  **해결 방법**: 해결 방법이 없습니다.

### <a name="sql-server-integration-services-ssis-ctp-11"></a>SSIS(SQL Server Integration Services)(CTP 1.1)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>SSIS 규모 확장이 설치되어 있으면 SSIS 카탈로그가 삭제되지 않을 수 있음
**문제 및 고객에게 미치는 영향:** SSIS 규모 확장 기능이 컴퓨터에 설치되어 있는 경우 "사용자가 현재 로그인되어 있기 때문에 *'login'* 로그인을 삭제할 수 없습니다."라는 오류가 발생하고 SSISDB 카탈로그 데이터베이스가 삭제되지 않을 수 있습니다.
   
**해결 방법**:
-   규모 확장 마스터 컴퓨터에서 "services.msc" 명령을 실행하여 서비스 창을 엽니다. SQL Server Integration Services 클러스터 마스터 서비스를 중지합니다.
-   마스터에 연결된 규모 확장 작업자 컴퓨터에서 "services.msc" 명령을 실행하여 서비스 창을 엽니다. SQL Server Integration Services 클러스터 작업자 서비스를 중지합니다.

이제 SSISDB 카탈로그 데이터베이스를 삭제할 수 있습니다.

#### <a name="odbc-components-are-not-supported-in-this-ctp-release"></a>이 CTP 릴리스에서는 ODBC 구성 요소가 지원되지 않음
**문제 및 고객 영향**: 이 CTP 릴리스에서는 ODBC 연결 관리자, 원본 및 대상이 지원되지 않습니다.

**해결 방법**: 해결 방법이 없습니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-10-november-2016"></a>SQL Server vNext CTP 1.0(2016년 11월)
### <a name="supported-installation-scenarios-ctp10"></a>지원되는 설치 시나리오(CTP&1;.0)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]는 테스트 버전으로만 제공됩니다.  프로덕션 배포는 지원되지 않습니다. [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]은 가상 컴퓨터에 설치하고 테스트하는 것이 좋습니다.

특히 다음과 같은 시나리오가 사용될 수 있지만 철저히 테스트되지 않았으며 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에서 지원되지 **않습니다**.
- CTP 1.0의 제거
- 다른 버전의 SQL Server와 함께 병렬 설치
- 이전 버전의 SQL Server에서 업그레이드
- [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 설치의 일부로 SQL Server 기능 팩 구성 요소를 사용할 수 없음

### <a name="documentation-ctp-10"></a>설명서(CTP 1.0)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]과 관련된 문서의 내용은 **적용 대상:**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-database-engine-ctp-10"></a>SQL Server 데이터베이스 엔진(CTP 1.0)
-  **문제 및 고객에게 미치는 영향:** CTP1의 `STRING_AGG` 함수는 결과로 LOB 형식(예: `NVARCHAR(MAX)`)을 반환합니다. 향후 CTP 릴리스에서는 이 동작이 변경될 수 있으며 입력 값이 LOB 형식이 아닐 경우 `STRING_AGG`에서 `NVARCHAR(4000)`을 반환할 수 있습니다. 연결된 결과가 `NVARCHAR(4000)`에 맞지 않을 경우 오버플로 오류가 발생할 수 있습니다.

-  **문제 및 고객에게 미치는 영향:** `WITHIN`과 같이 예약되지 않은 키워드를 `STRING_AGG` 식의 별칭으로 사용하지 마세요. 예를 들어 `SELECT Company.Name, STRING_AGG(Product.Name, ',') AS WITHIN FROM TableA;` 같은 경우입니다. 향후 CTP 릴리스에서는 `STRING_AGG` 호출 후 `WITHIN` 토큰이 `STRING_AGG` 함수의 일부로 사용될 수 있습니다.

-  **해결 방법:** `WITHIN` 별칭을 사용하지 않거나 `STRING_AGG` 함수에서 추가될 수 있는 향후 변경 내용과 충돌하지 않도록 하려면 `AS WITHIN`을 별칭 사양으로 추가하세요.


### <a name="sql-server-integration-services-ctp-10"></a>SQL Server Integration Services(CTP 1.0)
#### <a name="stop-operation-in-ssis-catalog-may-fail"></a>SSIS 카탈로그에서 작업 중지가 실패할 수 있음
**문제 및 고객에게 미치는 영향:** [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] 또는 catalog.stop_operation 저장 프로시저를 사용하여 [!INCLUDE[ssIS_md](../includes/ssis-md.md)]에서 작업을 중지하면 "사용자 정의 루틴 또는 집계 'stop_operation_internal'을(를) 실행하는 동안 .NET Framework 오류가 발생했습니다."라는 오류가 발생하며 실패할 수 있습니다.

-  **해결 방법:** Windows 작업 관리자를 엽니다. **프로세스** 탭에서 **ISServerExec**라는 프로세스를 찾고 **작업 끝내기**를 클릭하여 프로세스를 종료합니다.

#### <a name="create-dump-of-ssis-pacakge-execution-may-fail"></a>SSIS 패키지 실행의 덤프 만들기가 실패할 수 있음
**문제 및 고객에게 미치는 영향:** catalog.create_execution_dump 저장 프로시저를 사용하여 패키지 실행에 대한 덤프를 만들면 "사용자 정의 루틴 또는 집계 'create_execution_dump_internal'을(를) 실행하는 동안 .NET Framework 오류가 발생했습니다."라는 오류가 발생하며 실패할 수 있습니다.

-  **해결 방법:** Windows 작업 관리자를 엽니다. **프로세스** 탭에서 **ISServerExec**라는 프로세스를 찾아 마우스 오른쪽 단추로 클릭한 다음 **덤프 파일 만들기**를 클릭합니다.

#### <a name="get-perf-counter-of-ssis-package-execution-may-fail"></a>SSIS 패키지 실행의 성능 카운터 가져오기가 실패할 수 있음
**문제 및 고객에게 미치는 영향:** 테이블 반환 함수 catalog.dm_execution_performance_counters를 사용하여 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 성능 카운터를 쿼리하면 "사용자 정의 루틴 또는 집계 'get_execution_perf_counters'을(를) 실행하는 동안 .NET Framework 오류가 발생했습니다."라는 오류가 발생하며 실패할 수 있습니다.

-  **해결 방법**: Windows 성능 모니터를 사용하여 성능 카운터 값을 직접 모니터링합니다. 특정 패키지 실행과 관련된 성능 카운터에 대한 해결 방법은 없습니다.

#### <a name="deleting-catalog-may-fail-when-ssis-scale-out-master-is-installed"></a>SSIS 규모 확장 마스터가 설치되어 있으면 카탈로그 삭제가 실패할 수 있음
**문제 및 고객에게 미치는 영향:** [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 규모 확장 기능이 컴퓨터에 설치되어 있는 경우 **SSISDB** 카탈로그를 삭제하면 "사용자가 현재 '...'(으)로 로그인되어 있기 때문에 이 로그인을 삭제할 수 없습니다."라는 오류가 발생하며 실패할 수 있습니다. 

**해결 방법**: 
* 규모 확장 마스터 컴퓨터에서 "services.msc" 명령을 실행하여 **서비스** 창을 열고 **SQL Server Integration Services 클러스터 마스터** 서비스를 중지합니다. 

* 마스터에 연결된 규모 확장 작업자 컴퓨터에서 "services.msc" 명령을 실행하여 **서비스** 창을 엽니다. **SQL Server Integration Services 클러스터 작업자** 서비스를 중지합니다. 

이제 **SSISDB** 카탈로그를 삭제할 수 있어야 합니다.

#### <a name="odbc-connector-in-ssis-is-not-supported"></a>SSIS에서 ODBC 커넥터가 지원되지 않음
-  **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssIS_md](../includes/ssis-md.md)]에서 ODCB 커넥터가 지원되지 않습니다.
-  **해결 방법:** 해결 방법이 없습니다.

### <a name="sql-server-reporting-services-ctp-10"></a>SQL Server Reporting Services(CTP 1.0)

SQL Server Reporting Services는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대해 새로운 기능을 릴리스하지 않습니다.

### <a name="sql-server-master-data-services-ctp-10"></a>SQL Server Master Data Services(CTP 1.0)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>엔터티 트랜잭션 로그 유형이 특성으로 설정되어 있으면 트랜잭션이 작동하지 않을 수 있음
**문제 및 고객에게 미치는 영향:** 엔터티 트랜잭션 로그 유형이 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에서 **특성**(기본값: **멤버**)으로 설정되어 있으면 다음 시나리오가 실패합니다.

* 엔터티 변경에 대한 트랜잭션이 웹 사이트에 표시되지 않습니다.
* 웹 사이트에서 **트랜잭션** 페이지를 열고 트랜잭션을 되돌릴 수 없습니다.
* 웹 사이트에서 트랜잭션 주석을 사용하여 엔터티를 업데이트할 수 없습니다.

**해결 방법**: 해결 방법이 없습니다.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>**커밋된 버전만 복사**가 false로 설정되어 있으면 버전 복사가 작동하지 않을 수 있음
**문제 및 고객에게 미치는 영향:** **커밋된 버전만 복사** 설정이 **아니요**(기본값: **예**)로 설정되어 있으면 버전 복사 작업이 실패할 수 있습니다. 오류 메시지가 없습니다.

**해결 방법**: 해결 방법이 없습니다.
 
### <a name="sql-server-management-studio-ssms-ctp-10"></a>SSMS(SQL Server Management Studio)(CTP 1.0)
SQL Server Management Studio는 별도의 다운로드입니다.  최신 정보는 [SQL Server Management Studio - 릴리스 정보](https://msdn.microsoft.com/library/mt238486.aspx)를 참조하세요.

##  <a name="infotipimageshiproominfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) SQL Server 엔지니어링 팀에 문의 
- [Stack Overflow(태그 sql-server) - 기술 관련 문의 사항](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 포럼 - 기술 관련 문의 사항](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 버그 보고 및 기능 요청](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - R에 대한 일반 토론](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
