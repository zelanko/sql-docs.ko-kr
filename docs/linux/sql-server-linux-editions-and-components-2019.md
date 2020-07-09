---
title: SQL Server 2019 버전 및 지원되는 기능 - Linux
ms.date: 01/08/2020
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
author: VanMSFT
ms.author: vanto
ms.reviewer: mikeray
ms.openlocfilehash: d84f7a508d9ae6d46ba529d8139ecc8c0deaf3e8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894036"
---
# <a name="editions-and-supported-features-of-sql-server-2019-on-linux"></a>SQL Server 2019 on Linux 버전 및 지원되는 기능

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SQL Server 2019 on Linux의 다양한 버전에서 지원하는 기능을 자세히 설명합니다. Windows에서 지원되는 SQL Server 버전 및 기능에 대해서는 [SQL Server 2019 - Windows](../sql-server/editions-and-components-of-sql-server-version-15.md)를 참조하세요.  
  
설치 요구 사항은 사용자의 애플리케이션 요구에 따라 달라질 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전별로 각기 다르게 조직 및 개인의 고유한 성능, 런타임 및 가격 요구 사항을 충족시켜 줍니다. 설치하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소도 특정 요구 사항에 따라 달라집니다. 다음 섹션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 있는 여러 버전과 구성 요소 중에서 가장 적합한 항목을 선택하는 방법을 이해하는 데 도움이 될 것입니다.  

최신 릴리스 정보 및 새로운 기능 정보는 다음을 참조하세요.
- [SQL Server 2019 on Linux 릴리스 정보](sql-server-linux-release-notes-2019.md)
- [SQL Server 2019 on Linux의 새로운 기능](sql-server-linux-whats-new-2019.md)

Linux에서 사용할 수 없는 SQL Server 기능 목록은 [지원되지 않는 기능 및 서비스](#Unsupported)를 참조하세요.

### <a name="try-sql-server"></a>SQL Server를 사용해 보세요.    
    
[SQL Server 2019 다운로드](https://www.microsoft.com/sql-server/sql-server-2019)

## <a name="ssnoversion-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 버전  
 다음 표에서는 이러한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에 대해 설명합니다. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|정의|  
|---------------------------------------|----------------|  
|Enterprise|프리미엄 제품인 [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise 버전에서는 초고속 성능이 포함된 포괄적인 고성능 데이터 센터를 제공하여 중요 업무용 워크로드의 서비스 수준을 높일 수 있습니다.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 스탠더드 버전에서는 부서와 소규모 조직이 애플리케이션을 실행하기 위한 기본 데이터 관리를 제공하고 온-프레미스 및 클라우드용 공용 개발 도구를 지원함으로써, 최소한의 IT 리소스만으로도 데이터베이스 관리를 효율적으로 수행할 수 있도록 합니다.|  
|웹|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web 버전을 사용하면 소규모부터 대규모에 이르는 웹 속성에 대한 확장성, 경제성 및 관리 효율성 기능을 제공하여 웹 호스터와 웹 VAP의 총 소유 비용을 낮출 수 있습니다.|  
|Developer|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer 버전을 사용하면 개발자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]기반에서 어떤 유형의 애플리케이션도 빌드할 수 있습니다. 이 버전은 Enterprise 버전의 모든 기능을 포함하지만 프로덕션 서버가 아닌 개발 및 테스트 시스템으로 사용하도록 라이선스가 허여되어 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer는 애플리케이션을 빌드하고 테스트하는 사용자에게 적합한 버전입니다.|  
|Express Edition|Express 버전은 초급 단계의 무료 데이터베이스로 데스크톱 및 소규모 서버 데이터 기반 애플리케이션을 분석 및 빌드하는 데 적합합니다. 이 버전은 개별 소프트웨어 공급업체, 개발자 및 취미로 클라이언트 애플리케이션을 빌드하는 사용자에게 이상적입니다. 고급 데이터베이스 기능이 필요할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express를 다른 고급 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 원활하게 업그레이드할 수 있습니다.|  
  
## <a name="using-ssnoversion-with-clientserver-applications"></a>클라이언트/서버 애플리케이션으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용  

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 직접 연결되는 클라이언트/서버 애플리케이션 실행 컴퓨터에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]클라이언트 구성 요소만 설치하면 됩니다. 데이터베이스 서버의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 관리하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 애플리케이션을 개발하려는 경우에는 클라이언트 구성 요소를 설치하는 것도 좋은 방법입니다.  
  
## <a name="ssnoversion-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소  

SQL Server 2019 on Linux는 SQL Server 데이터베이스 엔진을 지원합니다. 다음 표에서는 데이터베이스 엔진의 기능을 설명합니다.   
  
|서버 구성 요소|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에는 데이터를 저장, 처리 및 보안 설정하기 위한 핵심 서비스인 [!INCLUDE[ssDE](../includes/ssde-md.md)], 복제 기능, 전체 텍스트 검색 기능 및 관계형 데이터와 XML 데이터 관리 도구 및 데이터베이스 내 분석 통합이 포함되어 있습니다.|  

**Developer, Enterprise Core 및 Evaluation Edition**  
Developer, Enterprise Core 및 Evaluation Edition에서 지원하는 기능의 경우 다음 표에서 SQL Server Enterprise Edition에 대해 나열된 기능을 참조하세요.

디벨로퍼 버전은 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)에 대해 클라이언트 1개만 계속 지원합니다. 
  
##  <a name="scale-limits"></a><a name="Cross-BoxScaleLimits"></a> 확장 한도  
  
|기능|Enterprise|Standard|웹|Express| 
|-------------|----------------|--------------|---------|------------------------|
|단일 인스턴스에서 사용되는 최대 컴퓨팅 용량 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨| 
|단일 인스턴스에서 사용되는 최대 컴퓨팅 용량 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스당 최대 버퍼 풀 메모리|운영 체제가 지원하는 최대 크기|128GB|64GB|1410MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스당 최대 Columnstore 세그먼트 캐시 메모리|무제한 메모리| 32GB| 16GB| 352MB|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 데이터베이스당 메모리 최적화 데이터의 최대 크기|무제한 메모리| 32GB| 16GB| 352MB|
|최대 관계형 데이터베이스 크기|524PB|524PB|524PB|10 GB|  
  
<sup>1</sup> Server + CAL(클라이언트 액세스 라이선스) 기반 라이선스가 포함된 Enterprise 버전(새 계약에 사용할 수 없음)은 SQL Server 인스턴스마다 최대 20개의 코어로 제한됩니다. 코어 기반 서버 라이선스 모델에서는 제한이 없습니다. 자세한 내용은 [SQL Server의 버전별 컴퓨팅 용량 제한](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조하세요.  
 
##  <a name="rdbms-high-availability"></a><a name="RDBMSHA"></a> RDBMS 고가용성  
  
|기능|Enterprise|Standard|웹|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|로그 전달|예|예|예|예|  
|백업 압축|예|예|예|예| 
|데이터베이스 스냅샷|예|예|예|예|
|Always On 장애 조치(failover) 클러스터 인스턴스<sup>1</sup>|예|예|예|예| 
|Always On 가용성 그룹<sup>2</sup>|예|예|예|예|
|기본 가용성 그룹<sup>3</sup>|예|예|예|예|
|최소 복제본 커밋 가용성 그룹|예|예|예|예|
|클러스터가 없는 가용성 그룹|예|예|예|예|
|온라인 페이지 및 파일 복원|예|예|예|예|
|온라인 인덱싱|예|예|예|예|
|다시 시작 가능한 온라인 인덱스 다시 작성|예|예|예|예|
|온라인 스키마 변경|예|예|예|예|
|빠른 복구|예|예|예|예|
|미러된 백업|예|예|예|예|
|Hot Add 메모리 및 CPU|예|예|예|예|
|암호화된 백업|예|예|예|예|
|Azure에 하이브리드 백업(URL에 백업)|예|예|예|예|
  
<sup>1</sup> Enterprise 버전에서 노드 수는 운영 체제 최댓값입니다. 스탠더드 버전에서는 두 개의 노드가 지원됩니다. 

<sup>2</sup> Enterprise 버전에서는 2개의 동기 보조 복제본을 포함하여 최대 8개까지 보조 복제본이 지원됩니다. 

<sup>3</sup> Standard Edition은 기본 가용성 그룹을 지원합니다. 기본 가용성 그룹은 데이터베이스가 하나인 두 개의 복제본을 지원합니다. 기본 가용성 그룹에 대한 자세한 내용은 [기본 가용성 그룹](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)을 참조하세요.    

##  <a name="rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> RDBMS 확장성 및 성능  
  
|기능|Enterprise|Standard|웹|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|예|예|예|예|  
|클러스터형 columnstore 인덱스의 큰 개체 이진 파일|예|예|예|예|  
|온라인 비클러스터형 columnstore 인덱스 다시 작성|예|예|예|예|
|메모리 내 OLTP <sup>1</sup>|예|예|예|예|
|영구 주 메모리|예|예|예|예|
|테이블 및 인덱스 분할|예|예|예|예|  
|데이터 압축|예|예|예|예|
|관리|예|예|예|예|  
|분할된 테이블 병렬 처리|예|예|예|예|
|NUMA 인식 및 큰 페이지 메모리 및 버퍼 배열 할당|예|예|예|예|
|IO 리소스 관리|예|예|예|예|  
|지연된 내구성|예|예|예|예|
|자동 튜닝|예|예|예|예|
|일괄 처리 모드 적응 조인|예|예|예|예|
|일괄 처리 모드 메모리 부여 피드백|예|예|예|예|
|다중 문 테이블 반환 함수에 대한 인터리브 실행|예|예|예|예|
|대량 삽입 기능 개선|예|예|예|예|


<sup>1</sup> 메모리 내 OLTP 데이터 크기 및 Columnstore 세그먼트 캐시는 크기 조정 제한 섹션에서 버전별로 지정된 메모리 양으로 제한됩니다. 최대 병렬 처리 수준도 제한됩니다. 인덱스 작성의 DOP(프로세스 병렬도)는 Standard Edition의 경우 2DOP, Web, Express Edition의 경우 1DOP로 제한됩니다. 디스크 기반 테이블과 메모리 최적화 테이블에서 생성된 columnstore 인덱스가 해당합니다.

##  <a name="rdbms-security"></a><a name="RDBMSS"></a> RDBMS 보안  
  
|기능|Enterprise|Standard|웹|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|행 수준 보안|예|예|예|예|  
|Always Encrypted|예|예|예|예| 
|동적 데이터 마스킹|예|예|예|예|   
|기본 감사|예|예|예|예| 
|미세 감사|예|예|예|예| 
|투명한 데이터베이스 암호화|예|예|예|예|   
|사용자 정의 역할|예|예|예|예| 
|포함된 데이터베이스|예|예|예|예| 
|백업을 위한 암호화|예|예|예|예|  

##  <a name="rdbms-manageability"></a><a name="RDBMSM"></a> RDBMS 관리성  
  
|기능|Enterprise|Standard|웹|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|관리자 전용 연결|예|예|예|예, 추적 플래그 있음|   
|PowerShell 스크립팅 지원|예|예|예|예| 
|데이터 계층 애플리케이션 구성 요소 작업 지원 - 추출, 배포, 업그레이드, 삭제|예|예|예|예| 
|정책 자동화(일정 및 변경 내용 검사)|예|예|예|예|  
|성능 데이터 수집기|예|예|예|예|
|표준 성능 보고서|예|예|예|예|
|계획 지침을 위한 계획 지침 및 계획 고정|예|예|예|예| 
|인덱스 뷰의 직접 쿼리(NOEXPAND 힌트 사용)|예|예|예|예| 
|인덱싱된 뷰의 자동 유지 관리|예|예|예|예|
|분산형 분할 뷰|예|예|예|예| 
|병렬 인덱스 작업|예|예|예|예|  
|쿼리 최적화 프로그램의 인덱싱된 뷰 자동 사용|예|예|예|예| 
|병렬 일관성 검사|예|예|예|예| 
|SQL Server 유틸리티 제어 지점|예|예|예|예|    

##  <a name="programmability"></a><a name="Programmability"></a> Programmability  
  
|기능|Enterprise|Standard|웹|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|예|예|예|예|   
|쿼리 저장소|예|예|예|예|   
|임시 테이블|예|예|예|예|   
|네이티브 XML 지원|예|예|예|예| 
|XML 인덱싱|예|예|예|예| 
|MERGE 및 UPSERT 기능|예|예|예|예|   
|날짜 및 시간 데이터 형식|예|예|예|예|  
|국제화 지원|예|예|예|예| 
|전체 텍스트 및 의미 체계 검색|예|예|예|예|
|쿼리에서 언어 지정|예|예|예|예|
|Service Broker(메시징)|예|예|아니요(클라이언트 전용)|아니요(클라이언트 전용)|
|Transact-SQL 엔드포인트|예|예|예|예|
|그래프|예|예|예|예|  


<sup>1</sup> 여러 컴퓨팅 노드를 사용하는 확장에는 헤드 노드가 필요합니다.

## <a name="integration-services"></a><a name="IS"></a> Integration Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원되는 SSIS(Integration Services) 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Integration Services 기능](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)을 참조하세요.

##  <a name="spatial-and-location-services"></a><a name="SLS"></a> 공간 및 위치 서비스  
  
|기능 이름|Enterprise|Standard|웹|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|공간 인덱스|예|예|예|예|   
|평면 및 측지 데이터 형식|예|예|예|예| 
|고급 공간 라이브러리|예|예|예|예|   
|산업 표준 공간 데이터 형식 가져오기/내보내기|예|예|예|예|   

## <a name="unsupported-features--services"></a><a name="Unsupported"></a> 지원되지 않는 기능 및 서비스

다음 기능 및 서비스는 Linux의 SQL Server 2019에서 사용할 수 없습니다. 이 기능에 대한 지원은 시간이 지나면서 점점 더 활성화됩니다.

| 영역 | 지원되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 병합 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | 타사 연결을 사용하는 분산 쿼리 |
| &nbsp; | [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이외의 데이터 원본에 연결된 서버  |
| &nbsp; | 시스템 확장 저장 프로시저(XP_CMDSHELL 등) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | EXTERNAL_ACCESS 또는 UNSAFE 권한 세트가 있는 CLR 어셈블리 |
| &nbsp; | Buffer Pool Extension |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, Queue Reader, SSIS, SSAS, SSRS |
| &nbsp; | 경고 |
| &nbsp; | 관리되는 백업 |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| &nbsp; | 연결된 서버의 AD 인증 | 
| &nbsp; | AG(가용성 그룹)의 AD 인증 | 
| **Services** | SQL Server Browser |
| &nbsp; | SQL Server R Services<sup>1</sup> |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | 데이터베이스 엔진 서비스 |
| &nbsp; | Master  Data  Services |

<sup>1</sup> SQL Server R은 SQL Server 내에서 지원되지만 별도 패키지로서의 SQL Server R Services는 지원되지 않습니다.
  
## <a name="next-steps"></a>다음 단계
 [SQL Server 2017 버전 및 지원되는 기능 - Linux](sql-server-linux-editions-and-components-2017.md)  
 [SQL Server 2019 버전 및 지원되는 기능 - Windows](../sql-server/editions-and-components-of-sql-server-version-15.md)  
 [SQL Server 2017 버전 및 지원되는 기능 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [SQL Server 2016 버전 및 지원되는 기능 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [SQL Server 2014 버전 및 지원되는 기능 - Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [SQL Server 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [SQL Server에 대한 제품 사양](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)


