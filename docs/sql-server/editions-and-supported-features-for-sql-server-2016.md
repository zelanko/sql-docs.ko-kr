---
title: "SQL Server 2016의 버전과 지원하는 기능 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "sql 버전"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b9b9db3ca911b8fd8eed6304b9d3a8f51e9e9ba2
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-supported-features-for-sql-server-2016"></a>SQL Server 2016의 버전과 지원하는 기능
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목은 다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]버전에서 지원되는 기능의 세부 정보를 제공합니다.  
  
 SQL Server Evaluation 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
  
 최신 릴리스 정보 및 새로운 기능 정보는 다음을 참조하세요.
- [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
- [SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **SQL Server 2016 사용해보기**    
    
 > [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Download SQL Server 2016  from the Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**(평가 센터에서 SQL Server 2016 다운로드)    
    
> ![Azure 가상 컴퓨터 소형](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)(SQL Server 2016이 이미 설치된 가상 컴퓨터 실행)**    
    
**Developer 및 Evaluation Edition**  
 Developer 및 Evaluation Edition에서 지원하는 기능의 경우 아래 표에서 SQL Server Enterprise Edition에 대해 나열된 기능을 참조하세요.
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1용 Developer Edition에 추가된 기능 목록은 [SQL Server 2016 SP1 버전](https://aka.ms/uw6cw4)을 참조하세요.   
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|단일 인스턴스에서 사용되는 최대 계산 용량 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨| 
|단일 인스턴스에서 사용되는 최대 계산 용량 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스별 최대 버퍼 풀 메모리|운영 체제가 지원하는 최대 크기|128GB|64GB|1410MB|1410MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스별 최대 Columnstore 세그먼트 캐시 메모리|무제한 메모리| 32GB<sup>2</sup>| 16GB<sup>2</sup>| 352MB<sup>2</sup>| 352MB<sup>2</sup>|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 데이터베이스별 최대 메모리 최적화 데이터 크기|무제한 메모리| 32GB<sup>2</sup>| 16GB<sup>2</sup>| 352MB<sup>2</sup>| 352MB<sup>2</sup>|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스당 최대 메모리 사용량|운영 체제가 지원하는 최대 크기|테이블 형식: 16GB<br /><br /> MOLAP: 64GB|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 인스턴스당 최대 메모리 사용량|운영 체제가 지원하는 최대 크기|64GB|64GB|4GB|해당 사항 없음|
|최대 관계형 데이터베이스 크기|524PB|524PB|524PB|10GB|10GB|  
  
<sup>1</sup> Server + CAL(클라이언트 액세스 라이선스) 기반 라이선스가 포함된 엔터프라이즈 버전(새 계약에 사용할 수 없음)은 SQL Server 인스턴스마다 최대 20개의 코어로 제한됩니다. 코어 기반 서버 라이선스 모델에서는 제한이 없습니다. 자세한 내용은 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조하세요.  
  
<sup>2</sup> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1에 적용됩니다. 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core 지원 <sup>1</sup>|예|예|예|예|예|  
|로그 전달|예|예|예|아니오|아니요|  
|데이터베이스 미러링|예|예<br /><br /> 전체 보안만|미러링 모니터만|미러링 모니터만|미러링 모니터만| 
|백업 압축|예|예|아니오|아니오|아니요| 
|데이터베이스 스냅숏|예|예 <sup>3</sup>|예 <sup>3</sup>|예 <sup>3</sup>|예 <sup>3</sup>|
|Always On 장애 조치(failover) 클러스터 인스턴스|예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|예<br /><br /> 노드 2개 지원|아니요|아니오|아니요|  
|Always On 가용성 그룹|예<br /><br /> 2개의 동기 보조 복제본을 포함하여 최대 8개까지 보조 복제본 지원|아니요|아니오|아니오|아니요|
|기본 가용성 그룹 <sup>2</sup>|아니요|예<br /><br /> 노드 2개 지원|아니요|아니오|아니요|
|온라인 페이지 및 파일 복원|예|아니오|아니오|아니오|아니요|
|온라인 인덱싱|예|아니오|아니오|아니오|아니요|
|온라인 스키마 변경|예|아니오|아니오|아니오|아니요|
|빠른 복구|예|아니오|아니오|아니오|아니요|
|미러된 백업|예|아니오|아니오|아니오|아니요|
|Hot Add 메모리 및 CPU|예|아니오|아니오|아니오|아니요|
|데이터베이스 복구 관리자|예|예|예|예|예|
|암호화된 백업|예|예|아니오|아니오|아니요|
|Microsoft Azure에 하이브리드 백업(URL에 백업)|예|예|아니오|아니오|아니요|  
  
 <sup>1</sup> Server Core에 SQL Server 2016을 설치하는 방법은 [Server Core에 SQL Server 2016 설치](../database-engine/install-windows/install-sql-server-on-server-core.md)를 참조하세요. 

<sup>2</sup> 기본 가용성 그룹에 대한 자세한 내용은 [기본 가용성 그룹](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)을 참조하세요.  

<sup>3</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다.
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|예|예 <sup>2</sup>|예 <sup>2</sup>|예<sup>2</sup>|예<sup>2</sup>|  
|메모리 내 OLTP <sup>1</sup>|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>, <sup>3</sup>|예 <sup>2</sup>|
|Stretch Database|예|예|예|예|예|
|영구 주 메모리|예|예|예|예|예|
|다중 인스턴스 지원|50|50|50|50|50|
|테이블 및 인덱스 분할|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|  
|데이터 압축|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|
|리소스 관리자|예|아니오|아니오|아니오|아니요|  
|분할된 테이블 병렬 처리(partitioned table parallelism)|예|아니오|아니오|아니오|아니요|
|여러 Filestream 컨테이너|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|
|NUMA 인식 및 큰 페이지 메모리 및 버퍼 배열 할당|예|아니오|아니오|아니오|아니요|
|버퍼 풀 확장|예|예|아니오|아니오|아니요|
|IO 리소스 관리|예|아니오|아니오|아니오|아니요|  
|지연된 내구성|예|예|예|예|예|

<sup>1</sup> 메모리 내 OLTP 데이터 크기 및 Columnstore 세그먼트 캐시는 크기 조정 제한 섹션에서 버전별로 지정된 메모리 양으로 제한됩니다. 최대 병렬 처리 수준도 제한됩니다. 인덱스 작성에 대한 DOP(병렬 처리 수준)는 Standard Edition의 경우 2DOP, Web 및 Express Edition의 경우 1DOP로 제한됩니다. 디스크 기반 테이블과 메모리 최적화 테이블을 통해 생성된 columnstore 인덱스가 해당합니다.

<sup>2</sup> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1에 적용됩니다. 

<sup>3</sup> 이 기능은 LocalDB 설치 옵션에 포함되지 않습니다.
##  <a name="RDBMSS"></a> RDBMS Security  
  
|기능|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|행 수준 보안|예|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|  
|항상 암호화|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>| 
|동적 데이터 마스킹|예|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|   
|기본 감사|예|예|예|예|예| 
|미세 감사|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>| 
|투명한 데이터베이스 암호화|예|아니오|아니오|아니오|아니요|   
|확장 가능 키 관리|예|아니오|아니오|아니오|아니요| 
|사용자 정의 역할|예|예|예|예|예| 
|포함된 데이터베이스|예|예|예|예|예| 
|백업을 위한 암호화|예|예|아니오|아니오|아니요|  

<sup>1</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다.  
##  <a name="Replication"></a> Replication  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|다른 유형의 구독자|예|예|아니오|아니오|아니요|  
|병합 복제|예|예|예(구독자만)|예(구독자만)|예(구독자만)|   
|Oracle 게시|예|아니오|아니오|아니오|아니요| 
|피어 투 피어 트랜잭션 복제|예|아니오|아니오|아니오|아니요|   
|스냅숏 복제|예|예|예(구독자만)|예(구독자만)|예(구독자만)|   
|SQL Server 변경 내용 추적|예|예|예|예|예| 
|트랜잭션 복제|예|예|예(구독자만)|예(구독자만)|예(구독자만)|   
|Azure에 대한 트랜잭션 복제|예|예|아니오|아니오|아니요|   
|트랜잭션 복제 업데이트 가능한 구독|예|아니오|아니오|아니오|아니요|  
  
##  <a name="SSMS"></a> Management Tools  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SMO(SQL Management Objects)|예|예|예|예|예|  
|SQL 구성 관리자|예|예|예|예|예|   
|SQL CMD(명령 프롬프트 도구)|예|예|예|예|예|      
|Distributed Replay - 관리 도구|예|예|예|예|아니요|  
|Distribute Replay - Client|예|예|예|아니오|아니요|  
|Distributed Replay - 컨트롤러|예(최대 16개 클라이언트)|예(1개 클라이언트)|예(1개 클라이언트)|아니요|아니요|   
|SQL 프로파일러|예|예|아니요 <sup>1</sup>|아니요 <sup>1</sup>|아니요 <sup>1</sup>|  
|SQL Server 에이전트|예|예|예|아니오|아니요| 
|Microsoft System Center Operations Manager 관리 팩|예|예|예|아니오|아니요|  
|DTA(데이터베이스 튜닝 관리자)|예|예 <sup>2</sup>|예 <sup>2</sup>|아니요|아니요|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express with Tools 및 SQL Server Express with Advanced Services는 SQL Server Standard 및 SQL Server Enterprise Edition을 사용하여 프로파일링할 수 있습니다.  
  
 <sup>2</sup> 튜닝은 Standard Edition 기능에서만 사용됩니다.  
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|사용자 인스턴스|아니요|아니오|아니요|예|예| 
|LocalDB|아니요|아니오|아니요|예|아니요| 
|관리자 전용 연결|예|예|예|예, 추적 플래그 있음|예, 추적 플래그 있음|   
|PowerShell 스크립팅 지원|예|예|예|예|예| 
|SysPrep 지원 <sup>1</sup>|예|예|예|예|예| 
|데이터 계층 응용 프로그램 구성 요소 작업 지원 - 추출, 배포, 업그레이드, 삭제|예|예|예|예|예| 
|정책 자동화(일정 및 변경 내용 검사)|예|예|예|아니오|아니요|   
|성능 데이터 수집기|예|예|예|아니오|아니요| 
|다중 인스턴스 관리에서 관리되는 인스턴스로 등록 가능|예|예|예|아니오|아니요|   
|표준 성능 보고서|예|예|예|아니오|아니요| 
|계획 지침을 위한 계획 지침 및 계획 고정|예|예|예|아니오|아니요|   
|인덱스 뷰의 직접 쿼리(NOEXPAND 힌트 사용)|예|예|예|예|예| 
|인덱싱된 뷰의 자동 유지 관리|예|예|예|아니오|아니요| 
|분산형 분할 뷰|예|아니오|아니오|아니오|아니요| 
|병렬 인덱스 작업|예|아니오|아니오|아니오|아니요|  
|쿼리 최적화 프로그램의 인덱싱된 뷰 자동 사용|예|아니오|아니오|아니오|아니요| 
|병렬 일관성 검사|예|아니오|아니오|아니오|아니요| 
|SQL Server 유틸리티 제어 지점|예|아니오|아니오|아니오|아니요|    
|버퍼 풀 확장|예|예|아니오|아니오|아니요| 
  
 <sup>1</sup> 자세한 내용은 [SysPrep을 사용하여 SQL Server 설치 시 고려 사항](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)을 참조하세요.  
 
<sup>2</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다. 
  
##  <a name="DevTools"></a> Development Tools  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Microsoft Visual Studio 통합|예|예|예|예|예| 
|Intellisense(Transact-SQL 및 MDX)|예|예|예|예|예| 
|SQL  Server  Data  Tools(SSDT)|예|예|예|예|아니요|    
|MDX 편집, 디버그 및 디자인 도구|예|예|아니오|아니오|아니요|   
  
##  <a name="Programmability"></a> Programmability  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|기본 R 통합|예|예|예|예|아니요|   
|고급 R 통합|예|아니오|아니오|아니오|아니요| 
|R Server (Standalone)|예|아니오|아니오|아니오|아니요|   
|Polybase 계산 노드|예|예 <sup>1</sup>|예 <sup>1</sup>, <sup>2</sup>|예 <sup>1</sup>, <sup>2</sup>|예 <sup>1</sup>, <sup>2</sup>| 
|Polybase 헤드 노드|예|아니오|아니오|아니오|아니요| 
|JSON|예|예|예|예|예|   
|쿼리 저장소|예|예|예|예|예|   
|임시 테이블|예|예|예|예|예|   
|CLR(공용 언어 런타임) 통합|예|예|예|예|예|   
|네이티브 XML 지원|예|예|예|예|예| 
|XML 인덱싱|예|예|예|예|예| 
|MERGE 및 UPSERT 기능|예|예|예|예|예|   
|FILESTREAM 지원|예|예|예|예|예| 
|FileTable|예|예|예|예|예| 
|날짜 및 시간 데이터 형식|예|예|예|예|예|  
|국제화 지원|예|예|예|예|예| 
|전체 텍스트 및 의미 체계 검색|예|예|예|예|아니요| 
|쿼리에서 언어 지정|예|예|예|예|아니요|   
|Service Broker(메시징)|예|예|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|   
|Transact-SQL 끝점|예|예|예|아니오|아니요| 

<sup>1</sup> 여러 계산 노드를 사용하는 확장에는 헤드 노드가 필요합니다.

<sup>2</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다.
  
## <a name="IS"></a> Integration Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원되는 SSIS(Integration Services) 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Integration Services 기능](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)을 참조하세요.

##  <a name="MDS"></a> Master Data Services  
 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 버전에서 지원되는 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]및 Data Quality Services 기능에 대한 자세한 내용은 [Master Data Services and Data Quality Services Features Supported by the Editions of SQL Server 2016](../master-data-services/master-data-services-and-data-quality-services-features-support.md)(SQL Server 2016 버전에서 지원하는 Master Data Services 및 Data Quality Services 기능)을 참조하세요. 

  
##  <a name="DW"></a> Data Warehouse  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|데이터베이스 없이 큐브 만들기|예|예|아니오|아니오|아니요 |   
|준비 및 데이터 웨어하우스 스키마 자동 생성|예|예|아니오|아니오|아니요| 
|변경 데이터 캡처|예|예 <sup>1</sup>|아니요|아니오|아니요| 
|스타 조인 쿼리 최적화|예|아니오|아니오|아니오|아니요| 
|확장 가능한 읽기 전용 Analysis Services 구성|예|아니오|아니오|아니오|아니요| 
|분할된 테이블 및 인덱스의 병렬 쿼리 처리|예|아니오|아니오|아니오|아니요|   
|글로벌 일괄 집계|예|아니오|아니오|아니오|아니요| 

<sup>1</sup> [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1에 적용됩니다.  
##  <a name="SSAS"></a> Analysis Services  
  
[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 Analysis Services 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요. 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 Analysis Services 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 Analysis Services 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 SharePoint용 PowerPivot 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="DM"></a> Data Mining  
  
[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 데이터 마이닝 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="SSRS"></a> Reporting Services  
  
[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 Reporting Services 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.

##  <a name="BIC"></a> Business Intelligence Clients  

[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]버전에서 지원되는 Business Intelligence 클라이언트 기능에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) 및 [SQL Server 2016 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|공간 인덱스|예|예|예|예|예|   
|평면 및 측지 데이터 형식|예|예|예|예|예| 
|고급 공간 라이브러리|예|예|예|예|예|   
|산업 표준 공간 데이터 형식 가져오기/내보내기|예|예|예|예|예|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|예|예|예|예|예|   
|데이터베이스 메일|예|예|예|아니오|아니요| 
  
##  <a name="Other"></a> Other Components  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|아니요|아니요| 
|StreamInsight HA|StreamInsight Premium Edition|아니요|아니오|아니오|아니요|   
  
> [![Download SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[Download the latest version of SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2016 제품 사양](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [SQL Server 2016 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  

