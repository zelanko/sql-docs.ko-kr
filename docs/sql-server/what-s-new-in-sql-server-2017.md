---
title: SQL Server 2017의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 42358e9e43e12a13c5b9e03b58df349b8f7a4231
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65729439"
---
# <a name="whats-new-in-sql-server-2017"></a>SQL Server 2017의 새로운 기능
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]
SQL Server 2017에서는 SQL Server의 기능을 Linux, Linux 기반 Docker 컨테이너 및 Windows에서도 제공하여 SQL Server를 개발 언어, 데이터 형식, 온-프레미스 또는 클라우드, 운영 체제 등을 선택할 수 있는 플랫폼으로 만들기 위한 중요한 진전을 이루었습니다. 이 항목에서는 특정 기능 영역의 새로운 기능을 요약하고 추가 세부 정보에 대한 링크를 포함합니다. Linux의 SQL Server에 대한 자세한 내용은 [SQL Server on Linux Documentation](https://docs.microsoft.com/sql/linux/)(Linux 기반 SQL Server 설명서)을 참조하세요.

[![평가 센터에서 다운로드](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **사용해 보기:** [SQL Server 2017 릴리스 다운로드 - 2017년 10월](https://go.microsoft.com/fwlink/?LinkID=829477).

> [!NOTE]
> 아래 변경 내용 외에도 누적 업데이트는 GA 릴리스 이후 정기적으로 릴리스됩니다. 이러한 누적 업데이트는 다양한 향상된 기능 및 수정 사항을 제공합니다. 최신 CU 릴리스에 대한 자세한 내용은 [SQL Server 2017 누적 업데이트](https://aka.ms/sql2017cu)를 참조하세요.

## <a name="sql-server-2017-database-engine"></a>SQL Server 2017 데이터베이스 엔진

SQL Server 2017은 새로운 많은 데이터베이스 엔진 기능과 기능 개선 및 성능 개선 사항을 포함하고 있습니다. 
- CTP 2.0에 설명된 `clr strict security` 기능에 대한 해결 방법으로 이제 **CLR 어셈블리**를 허용 목록에 추가할 수 있습니다. 신뢰할 수 있는 어셈블리의 허용 목록을 지원하기 위해 [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) 및 [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)가 추가되었습니다(RC1).  
- **다시 시작 가능한 온라인 인덱스 다시 작성**은 오류(예: 복제본으로 장애 조치(failover) 또는 디스크 공간 부족) 발생 후 중지된 위치에서 온라인 인덱스 다시 작성을 재개하거나 일시 중지하고 나중에 온라인 인덱스 다시 작성 작업을 다시 시작합니다. [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) 및 [온라인 인덱스 작업에 대한 지침](../relational-databases/indexes/guidelines-for-online-index-operations.md)을 참조하세요. (CTP 2.0)
- ALTER DATABASE SCOPED CONFIGURATION의 **IDENTITY_CACHE** 옵션을 사용하면 서버가 예기치 않게 다시 시작하거나 보조 서버로 장애 조치(failover)된 후 ID 열의 값이 차이 나지 않도록 할 수 있습니다. [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요. (CTP 2.0)
- 애플리케이션 워크로드의 런타임 조건에 대한 최적화 전략을 적용한 새로운 세대의 향상된 쿼리 처리 기능입니다. **적응 쿼리 처리** 기능 제품군의 첫 번째 버전의 경우 다중 문 테이블 값 함수에 대한 **배치 모드 적응 조인**, **배치 모드 메모리 부여 피드백** 및 **인터리브 실행**과 같은 세 가지 새로운 향상된 기능이 있습니다.  [SQL 데이터베이스의 지능형 쿼리 처리](../relational-databases/performance/intelligent-query-processing.md)를 참조하세요.
- **자동 데이터베이스 튜닝**은 잠재적 쿼리 성능 문제에 대한 정보를 제공하고 솔루션을 추천하며 식별된 문제를 자동으로 해결할 수 있습니다. [Automatic tuning](../relational-databases/automatic-tuning/automatic-tuning.md)(자동 튜닝)을 참조하세요. (CTP 2.0)
- 다 대 다 관계를 모델링하기 위한 새 **그래프 데이터베이스 기능** 에 노드 및 에지 테이블을 만들기 위한 새 [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 구문과 쿼리를 위한 [MATCH](../t-sql/queries/match-sql-graph.md) 키워드가 포함됩니다. [Graph Processing with SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md)(SQL Server 2017에서 그래프 처리)을 참조하세요. (CTP 2.0)
- CLR 어셈블리의 보안을 향상하기 위해 `clr strict security`라는 sp_configure 옵션이 기본적으로 사용하도록 설정됩니다. [CLR strict security](../database-engine/configure-windows/clr-strict-security.md)(CLR 엄격한 보안)를 참조하세요. (CTP 2.0)
- 설치 프로그램에서는 이제 초기 tempdb 파일 크기를 최대 파일당 **256GB**(262,144MB)까지 지정할 수 있으며, IFI를 사용하도록 설정하지 않고 파일 크기를 1GB보다 크게 설정하면 경고가 표시됩니다. (CTP 2.0)
- [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)의 **modified_extent_page_count** 열에서 각 데이터베이스 파일의 차등 변경 내용을 추적하므로 데이터베이스에서 변경된 페이지의 비율에 따라 차등 백업이나 전체 백업을 수행하는 스마트 백업 솔루션을 지원합니다. (CTP 2.0)
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) T-SQL 구문에서는 이제 **ON** 키워드를 사용하여 테이블을 사용자의 기본값이 아닌 FileGroup으로 로드할 수 있습니다. (CTP 2.0)
- 이제 동일한 인스턴스에 속한 데이터베이스를 비롯해 **Always On 가용성 그룹**에 속한 모든 데이터베이스에서 데이터베이스 간 트랜잭션이 지원됩니다. [Transactions - Always On Availability Groups and Database Mirroring](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)(트랜잭션 - Always On 가용성 그룹 및 데이터베이스 미러링)을 참조하세요. (CTP 2.0)
- 새 **가용성 그룹** 기능에 클러스터 없는 지원, 최소 복제본 커밋 가용성 그룹 설정 및 Windows-Linux OS 간 마이그레이션 및 테스트가 포함됩니다. (CTP 1.3)
- 새 동적 관리 뷰:
    - [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)는 트랜잭션 로그 상태 모니터링에 유용한 요약 수준 특성 및 정보를 트랜잭션 로드 파일에 노출합니다. (CTP 2.1)
    - [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)는 데이터베이스별 버전 저장소 사용을 추적하며, 데이터베이스별 버전 저장소 사용을 기준으로 tempdb 크기를 사전에 계획하는 데 유용합니다. (CTP 2.0)
    - [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)는 VLF 정보를 노출하여 잠재적인 트랜잭션 로그 문제를 모니터링하고, 알리고, 방지합니다. (CTP 2.0)
    - [sys.dm_db_stats_histogram](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)은 통계를 검토하기 위해 새로운 동적 관리 뷰입니다. (CTP 1.3)
    - **sys.dm_os_host_info**는 Windows와 Linux 모두에 대한 운영 체제 정보를 제공합니다. (CTP 1.0)
- **DTA(데이터베이스 튜닝 관리자)** 의 성능이 개선되고 옵션이 추가됩니다. (CTP 1.2)
- **메모리 내 기능이 향상**되어 메모리 최적화 테이블에서 계산 열이 지원되고 고유하게 컴파일된 모듈에서 JSON 함수가 완벽히 지원되며 고유하게 컴파일된 모듈에서 CROSS APPLY 연산자가 지원됩니다. (CTP 1.1)
- **문자열 함수** CONCAT_WS, TRANSLATE 및 TRIM이 새로 제공되며 STRING_AGG 함수에 대해 WITHIN GROUP이 새로 지원됩니다. (CTP 1.1)
- CSV 및 Azure Blob 파일에 대한 새 **대량 액세스 옵션**(BULK INSERT 및 OPENROWSET(BULK...) )이 제공됩니다. (CTP 1.1)
- **메모리 최적화 개체의 기능이 향상**되어, sp_spaceused가 제공되고, 메모리 최적화 테이블에 대한 8개 인덱스 제한이 제거되었으며, 메모리 최적화 테이블과 고유하게 컴파일된 T-SQL 모듈에 대한 sp_rename과 고유하게 컴파일된 T-SQL 모듈에 대한 CASE 및 TOP (N) WITH TIES가 함께 제공됩니다. 메모리 액세스에 최적화된 파일 그룹 파일을 이제 Azure Storage에서 저장, 백업 및 복원할 수 있습니다. (CTP 1.0)
- **DATABASE SCOPED CREDENTIAL**는 보안 가능하고 보조적인 CONTROL, ALTER, REFERENCES, TAKE OWNERSHIP 및 VIEW DEFINITION 사용 권한의 새 클래스입니다. 이제 ADMINISTER DATABASE BULK OPERATIONS가 sys.fn_builtin_permissions에 표시됩니다. (CTP 1.0)
- 데이터베이스 **COMPATIBILITY_LEVEL 140**이 추가되었습니다. (CTP 1.0).  

자세한 내용은 [What's new in SQL Server 2017 Database Engine](~/database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)(SQL Server 2017 데이터베이스 엔진의 새로운 기능)을 참조하세요.

## <a name="sql-server-2017-integration-services-ssis"></a>SQL Server 2017 Integration Services(SSIS)
- SSIS의 새 **Scale Out** 기능에서 다음과 같은 새로운 기능과 변경된 기능을 제공합니다. 자세한 내용은 [What's New in Integration Services in SQL Server 2017](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)(SQL Server 2017에서 Integration Services의 새로운 기능)을 참조하세요. (RC1)
    -   Scale Out Master에서 이제 고가용성을 지원합니다.
    -   Scale Out Worker에서 실행 로그의 장애 조치(failover) 처리가 향상되었습니다.
    -   일관성과 가독성을 향상하기 위해 저장 프로시저 **[catalog].[create_execution]** 의 *runincluster* 매개 변수 이름이 *runinscaleout*으로 변경되었습니다.
    -   SSIS 카탈로그에 SSIS 패키지를 실행하기 위한 기본 모드를 지정하는 새 전역 속성이 있습니다.
- 새 **SSIS용 Scale Out** 기능에서 이제 실행을 트리거할 때 **Use32BitRuntime** 매개 변수를 사용할 수 있습니다. (CTP 2.1)
- SQL Server 2017 Integration Services(SSIS)에서 이제 **Linux의 SQL Server**를 지원하며 새 패키지를 사용하여 명령줄에서 Linux의 SSIS 패키지를 실행할 수 있습니다. 자세한 내용은 [blog post announcing SSIS support for Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)(Linux에 대한 SSIS 지원을 발표하는 블로그 게시물)를 참조하세요. (CTP 2.1)
- 새 **SSIS용 Scale Out** 기능을 사용하면 여러 컴퓨터에서 훨씬 더 쉽게 SSIS를 실행할 수 있습니다. [Integration Services 스케일 아웃](~/integration-services/scale-out/integration-services-ssis-scale-out.md)을 참조하세요. (CTP 1.0)
- 이제 OData 원본 및 OData 연결 관리자가 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결할 수 있습니다. (CTP 1.0)

자세한 내용은 [What's New in Integration Services in SQL Server 2017](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)(SQL Server 2017에서 Integration Services의 새로운 기능)을 참조하세요.

## <a name="sql-server-2017-master-data-services-mds"></a>SQL Server 2017 MDS(Master Data Services)
- SQL Server 2012, SQL Server 2014 및 SQL Server 2016에서 SQL Server 2017 Master Data Services로 업그레이드할 때의 환경 및 성능이 개선되었습니다. 
- 이제 웹 애플리케이션의 **탐색기** 페이지에서 엔터티, 컬렉션 및 계층 구조의 정렬된 목록을 볼 수 있습니다.
- 스테이징 저장 프로시저를 사용하여 수백만 개의 레코드를 스테이징하기 위한 성능이 향상되었습니다.
- 모델 사용 권한을 할당하기 위해 **그룹 관리** 페이지에서 **엔터티** 폴더를 확장할 때의 성능이 향상되었습니다. **그룹 관리** 페이지는 웹 애플리케이션의 **보안** 섹션에 있습니다. 성능 향상에 대한 자세한 내용은 [https://support.microsoft.com/help/4023865?preview](https://support.microsoft.com/help/4023865?preview)를 참조하세요. 사용 권한 할당에 대한 자세한 내용은 [모델 개체 사용 권한 할당(Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)를 참조하세요.

## <a name="sql-server-2017-analysis-services-ssas"></a>SQL Server 2017 Analysis Services(SSAS) 
SQL Server Analysis Services 2017에서는 테이블 형식 모델에 대한 여러 향상된 기능을 새로 제공합니다. 이러한 개체는 다음과 같습니다.
- Analysis Services의 기본 설치 옵션인 테이블 형식 모드 (CTP 2.0)
- 테이블 형식 모델의 메타데이터를 보호하는 개체 수준 보안 (CTP 2.0)
- 날짜 필드를 기준으로 관계를 쉽게 만드는 날짜 관계 (CTP 2.0)
- M 쿼리에 대한 새 **데이터 가져오기**(파워 쿼리) 데이터 원본 및 기존 DirectQuery 데이터 원본 지원 (CTP 2.0) 
- SSDT용 DAX 편집기 (CTP 2.0)
- 인코딩 힌트. 대규모 메모리 내 테이블 형식 모델의 데이터 새로 고침을 최적화하기 위한 고급 기능 (CTP 1.3)
- 테이블 형식 모델에 대한 **1400 호환성 수준** 지원 새로 만들거나 기존 테이블 형식 모델 프로젝트를 1400 호환성 수준으로 업그레이드하려면 [SSDT(SQL Server Data Tools) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939)를 다운로드 및 설치합니다. (CTP 1.1)
- 1400 호환성 수준의 테이블 모델에 대한 최신 **데이터 가져오기** 환경 [Analysis Services Team Blog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/)(Analysis Services 팀 블로그)를 참조하세요. (CTP 1.1)
- 비정형 계층의 빈 멤버를 숨기기 위한 **멤버 숨기기** 속성 (CTP 1.1)
- 집계 정보에 대한 **자세한 정보를 표시**하기 위한 **세부 정보 행** 최종 사용자 작업. 세부 정보 행 식을 작성하기 위한 [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) 및 **DETAILROWS** 함수 (CTP 1.1)
- 여러 값을 지정하는 DAX **IN** 연산자 (CTP 1.1)

자세한 내용은 [What's new in SQL Server Analysis Services 2017](~/analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)(SQL Server Analysis Services 2017의 새로운 기능)을 참조하세요.

## <a name="sql-server-2017-reporting-services-ssrs"></a>SQL Server 2017 Reporting Services(SSRS)
SQL Server 설치 프로그램을 통해 SQL Server Reporting Services를 더 이상 설치할 수 없습니다. [Microsoft SQL Server 2017 Reporting Services를 다운로드](https://www.microsoft.com/download/details.aspx?id=55252)하려면 Microsoft 다운로드 센터로 이동하세요. 
- 이제 보고서에서 주석을 사용하여 큐브 뷰를 추가하고 다른 사용자와 공동 작업할 수 있습니다. 주석에 첨부 파일도 포함할 수 있습니다.
- 최신 버전의 보고서 작성기와 SQL Server Data Tools에서 필요한 필드를 쿼리 디자이너로 끌어다 놓아 지원되는 SQL Server Analysis Services 테이블 형식 데이터 모델에 대한 네이티브 DAX 쿼리를 만들 수 있습니다. [Reporting Services blog](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)(Reporting Services 블로그)를 참조하세요.
- 최신 애플리케이션 및 사용자 지정 개발을 사용하기 위해 SSRS는 이제 완벽 하게 development 규격 RESTful API를 지원합니다. 전체 API 사양 및 설명서는 이제 [swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0)에서 확인할 수 있습니다.

자세한 내용은 [What's new in SQL Server Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)(SSRS(SQL Server Reporting Services)의 새로운 기능)를 참조하세요.

## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 2017의 Machine Learning 

R 언어와 함께 Python 지원을 반영하여 SQL Server R Services 이름이 **SQL Server Machine Learning Services**로 변경되었습니다. Machine Learning Services(데이터베이스 내)를 사용하여 SQL Server에서 R 또는 Python 스크립트를 실행하거나 **Microsoft Machine Learning Server(독립 실행형)** 를 설치하여 SQL Server가 필요 없는 R 및 Python 모델을 배포하고 사용할 수 있습니다. 

SQL Server 개발자는 이제 Microsoft의 최신 혁신 기능과 함께 오픈 소스 에코 시스템에서 사용할 수 있는 광범위 Python ML 및 AI 라이브러리에 액세스할 수 있습니다.

- **revoscalepy** - RevoScaleR에 해당하는 이 Pythonic 항목에는 선형 및 로지스틱 회귀, 의사 결정 트리, 승격된 트리 및 임의 포리스트의 병렬 알고리즘 외에도 데이터 변환 및 데이터 이동, 원격 컴퓨팅 컨텍스트 및 데이터 소스에 사용할 풍부한 API 집합이 포함되어 있습니다.
- **microsoftml** - Python 바인딩을 사용하는 이 첨단 기계 학습 알고리즘 및 변환 패키지에는 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 최적화된 선형 및 로지스틱 회귀 알고리즘이 포함되어 있습니다. 이미지 추출 또는 감정 분석에 사용할 수 있는 ResNet 모델을 기반으로 미리 학습된 모델도 가져옵니다.
- **T-SQL로 Python 운영화** - 저장 프로시저 `sp_execute_external_script`를 사용하여 Python 코드를 쉽게 배포합니다. SQL에서 Python 프로세스로 데이터를 스트리밍하고 MPI 링 병렬화를 사용하여 뛰어난 성능을 얻습니다.
- **SQL Server 컴퓨팅 컨텍스트의 Python** - 데이터 과학자와 개발자는 개발 환경에서 원격으로 Python 코드를 실행하여 데이터를 이동하지 않고 데이터를 탐색하고 모델을 개발할 수 있습니다.
- **네이티브 점수 매기기** - Transact-SQL의 PREDICT 함수는 R의 설치 여부와 관계없이 SQL Server 2017의 모든 인스턴스에서 점수를 매기는 데 사용할 수 있습니다. 지원되는 RevoScaleR 및 revoscalepy 알고리즘 하나를 사용하여 모델을 학습한 후 새로운 압축 이진 형식으로 저장하기만 하면 됩니다.
- **패키지 관리** - T-SQL은 이제 DBA가 R 패키지를 좀 더 효과적으로 관리할 수 있도록 CREATE EXTERNAL LIBRARY 문을 지원합니다. 역할을 사용하여 프라이빗 또는 공유 패키지 액세스를 제어하고, 데이터베이스에 R 패키지를 저장하여 다른 사용자와 공유합니다.
- **성능 향상** - 저장 프로시저 `sp_execute_external_script`는 columnstore 데이터에 대한 일괄 처리 모드 실행을 지원하도록 최적화되었습니다.


자세한 내용은 [What's new in SQL Server Machine Learning Services](~/advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)(SQL Server Machine Learning Services의 새로운 기능)를 참조하세요.

## <a name="next-steps"></a>다음 단계
- [SQL Server 2017 릴리스 정보](sql-server-2017-release-notes.md)를 참조하세요.
- [SQL Server 2017 on Linux의 새로운 기능](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)을 알아보세요.
- [SQL Server 2016의 새로운 기능](what-s-new-in-sql-server-2016.md)을 확인하세요.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
