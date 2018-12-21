---
title: SQL Server 2017의 버전 및 지원하는 기능 ~ Linux | Microsoft Docs
ms.custom: sql-linux
ms.date: 09/14/2017
ms.prod: sql
ms.reviewer: ''
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
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 089ced09d718b0716f0c19d4553e52ff02c3d505
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665582"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Linux의 SQL Server 2017에서 버전 및 지원하는 기능

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux의 SQL Server 2017의 다양한 버전에서 지원되는 기능의 상세 정보를 제공합니다. Windows의 SQL Server의 버전 및 지원하는 기능에 대해서는, [SQL Server 2017-Windows](../sql-server/editions-and-components-of-sql-server-2017.md)를 참조하세요.  
  
설치 요구 사항은 사용자의 응용 프로그램 요구에 따라 달라질 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 여러 버전은 각기 다르게 조직 및 개인의 고유한 성능, 런타임 및 가격 요구 사항을 충족시켜 줍니다. 설치하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소도 특정 요구 사항에 따라 달라집니다. 다음 섹션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 있는 여러 버전과 구성 요소 중에서 가장 적합한 항목을 선택하는 방법을 이해하는 데 도움이 될 것입니다.  

최신 릴리스 정보 및 새로운 기능 정보는 다음을 참조하세요.
- [Linux 릴리스 노트의 SQL Server](sql-server-linux-release-notes.md)
- [Linux의 SQL Server의 새로운 기능](sql-server-linux-whats-new.md)

Linux에서 사용할 수 없는 SQL Server 기능의 목록을 보려면 참조 [지원 되지 않는 기능 및 서비스](sql-server-linux-release-notes.md#Unsupported)합니다.

### <a name="try-sql-server"></a>SQL Server를 사용해 보세요.    
    
[SQL Server 2017 다운로드](https://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 버전  
 다음 표에서는 이러한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에 대해 설명합니다. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|정의|  
|---------------------------------------|----------------|  
|Enterprise|프리미엄 제품인 [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise edition은 중요 업무용 워크로드에 대한 높은 서비스 수준을 사용하도록 설정하는 매우 빠른 성능 포괄적인 고성능 데이터 센터 기능을 제공합니다.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition 부서와 소규모 조직이 응용 프로그램을 실행하기 위한 기본 데이터 관리를 제공하며 온-프레미스 및 클라우드용 공용 개발 도구 지원-최소한의 IT 리소스를 사용하여 효과적인 데이터베이스 관리를 사용하도록 설정합니다.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web 버전을 사용하면 소규모부터 대규모에 이르는 웹 속성에 대한 확장성, 경제성 및 관리 효율성 기능을 제공하여 웹 호스터와 웹 VAP의 총 소유 비용을 낮출 수 있습니다.|  
|Developer|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer 버전을 사용하면 개발자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기반에서 어떤 유형의 응용 프로그램도 빌드할 수 있습니다. 이 버전은 Enterprise 버전의 모든 기능을 포함하지만 프로덕션 서버가 아닌 개발 및 테스트 시스템으로 사용하도록 라이선스가 허가되어 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer는 응용 프로그램을 빌드하고 테스트하는 사용자에게 적합한 버전입니다.|  
|Express Edition|Express 버전은 초급 단계의 무료 데이터베이스로 데스크톱 및 소규모 서버 데이터 기반 응용 프로그램을 분석 및 빌드하는 데 적합합니다. 이 버전은 개별 소프트웨어 공급업체, 개발자 및 취미로 클라이언트 응용 프로그램을 빌드하는 사용자에게 이상적입니다. 고급 데이터베이스 기능이 필요할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express를 다른 고급 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 원활하게 업그레이드할 수 있습니다.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>클라이언트/서버 응용 프로그램으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용  

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 직접 연결되는 클라이언트/서버 응용 프로그램 실행 컴퓨터에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]클라이언트 구성 요소만 설치하면 됩니다. 데이터베이스 서버의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 관리하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 응용 프로그램을 개발하려는 경우에는 클라이언트 구성 요소를 설치하는 것도 좋은 방법입니다.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소  

SQL Server 2017 Linux에서 SQL Server 데이터베이스 엔진을 지원합니다. 다음 표에서 데이터베이스 엔진의 기능을 설명합니다.   
  
|서버 구성 요소|설명|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 포함 된 [!INCLUDE[ssDE](../includes/ssde-md.md)], 데이터베이스 분석 통합에서 저장, 처리 및 데이터, 복제, 전체 텍스트 검색, 관계형 관리용 도구 및 XML 데이터 보안에 대 한 핵심 서비스입니다.|  

**Developer, Enterprise Core 및 Evaluation edition**  
Developer, Enterprise Core 및 Evaluation edition을 지 원하는 기능, SQL Server Enterprise edition은 다음 표에 나열 된 기능을 참조 하세요.

Developer Edition은 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)에 대해 클라이언트 1개만 계속 지원합니다. 
  
##  <a name="Cross-BoxScaleLimits"></a> 확장 한도  
  
|기능|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|단일 인스턴스에서 사용되는 최대 계산 용량 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨| 
|단일 인스턴스에서 사용되는 최대 계산 용량 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스당 최대 버퍼 풀 메모리|운영 체제가 지원하는 최대 크기|128GB|64GB|1410MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스당 최대 Columnstore 세그먼트 캐시 메모리|무제한 메모리| 32GB| 16GB| 352MB|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 데이터베이스당 메모리 최적화 데이터의 최대 크기|무제한 메모리| 32GB| 16GB| 352MB|
|최대 관계형 데이터베이스 크기|524PB|524PB|524PB|10GB|  
  
<sup>1</sup> Enterprise edition Server + 클라이언트 액세스 라이선스 (CAL) 기반 라이선스(새 계약에 사용할 수 없음)는 SQL Server 인스턴스당 20 개의 코어로 제한됩니다. 코어 기반 서버 라이선스 모델에서는 제한이 없습니다. 자세한 내용은 [SQL Server의 버전별 계산 용량 제한](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)합니다.  
 
##  <a name="RDBMSHA"></a> RDBMS 고가용성  
  
|기능|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|로그 전달|예|예|예|아니요|  
|백업 압축|예|예|아니오|아니요| 
|데이터베이스 스냅숏|예|아니오|아니요|아니요|
|Always On 장애 조치 클러스터 인스턴스의<sup>1</sup>|예|예|아니오|아니요| 
|Always On 가용성 그룹<sup>2</sup>|예|아니오|아니요|아니요|
|기본 가용성 그룹 <sup>3</sup>|아니요|예|아니오|아니요|
|최소 복제본 커밋 가용성 그룹|예|예|아니오|아니요|
|클러스터가 없는 가용성 그룹|예|예|아니오|아니요|
|온라인 페이지 및 파일 복원|예|아니오|아니요|아니요|
|온라인 인덱싱|예|아니오|아니요|아니요|
|다시 시작 가능한 온라인 인덱스 다시 작성|예|아니오|아니요|아니요|
|온라인 스키마 변경|예|아니오|아니요|아니요|
|빠른 복구|예|아니오|아니요|아니요|
|미러된 백업|예|아니오|아니요|아니요|
|Hot Add 메모리 및 CPU|예|아니오|아니요|아니요|
|암호화된 백업|예|예|아니오|아니요|
|Microsoft Azure에 하이브리드 백업(URL에 백업)|예|예|아니오|아니요|
  
<sup>1</sup> Enterprise edition에서, 지원하는 노드 수는 최대 운영 체제 수입니다. Standard 버전에서는 두 개의 노드가 지원됩니다. 

<sup>2</sup> Enterprise edition에서, 2개의 동기 보조 복제본을 포함하여 최대 8개의 보조 복제본에 대한 지원을 제공합니다. 

<sup>3</sup> standard edition은 기본 가용성 그룹을 지원 합니다. 기본 가용성 그룹은 데이터베이스가 하나인 두 개의 복제본을 지원합니다. 기본 가용성 그룹에 대한 자세한 내용은 [기본 가용성 그룹](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)을 참조하세요.    

##  <a name="RDBMSSP"></a> RDBMS 확장성 및 성능  
  
|기능|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|예|예|예|예|  
|클러스터형 columnstore 인덱스의 큰 개체 이진 파일|예|예|예|예|  
|온라인 비클러스터형 columnstore 인덱스 다시 작성|예|아니오|아니요|아니요|
|In-Memory OLTP <sup>1</sup>|예|예|예|예|
|영구 주 메모리|예|예|예|예|
|테이블 및 인덱스 분할|예|예|예|예|  
|데이터 압축|예|예|예|예|
|리소스 관리자|예|아니오|아니요|아니요|  
|분할된 테이블 병렬 처리|예|아니오|아니요|아니요|
|NUMA 인식 및 큰 페이지 메모리 및 버퍼 배열 할당|예|아니오|아니요|아니요|
|IO 리소스 관리|예|아니오|아니요|아니요|  
|지연된 내구성|예|예|예|예|
|자동 튜닝|예|아니오|아니요|아니요|
|일괄 처리 모드 적응 조인|예|아니오|아니요|아니요|
|일괄 처리 모드 메모리 부여 피드백|예|아니오|아니요|아니요|
|다중 문 테이블 반환 함수에 대한 인터리브 실행|예|예|예|예|
|대량 삽입 기능 개선|예|예|예|예|


<sup>1</sup> In-Memory OLTP 데이터 크기 및 Columnstore 세그먼트 캐시는 크기 조정 제한 섹션에서 버전별로 지정된 메모리 양으로 제한됩니다. 최대 병렬 처리 수준도 제한됩니다. 인덱스 작성에 대한 프로세스 병렬 처리 (DOP) 수준은 Standard edition에 대한 2 DOP 및 Web 및 Express edition에 대한 DOP를 1로 제한됩니다. 디스크 기반 테이블과 메모리 최적화 테이블에서 생성된 columnstore 인덱스가 해당합니다.

##  <a name="RDBMSS"></a> RDBMS 보안  
  
|기능|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|행 수준 보안|예|예|예|예|  
|항상 암호화|예|예|예|예| 
|동적 데이터 마스킹|예|예|예|예|   
|기본 감사|예|예|예|예| 
|미세 감사|예|예|예|예| 
|투명한 데이터베이스 암호화|예|아니오|아니요|아니요|   
|사용자 정의 역할|예|예|예|예| 
|포함된 데이터베이스|예|예|예|예| 
|백업을 위한 암호화|예|예|아니오|아니요|  

##  <a name="RDBMSM"></a> RDBMS 관리성  
  
|기능|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|관리자 전용 연결|예|예|예|예, 추적 플래그 있음|예, 추적 플래그 있음|   
|PowerShell 스크립팅 지원|예|예|예|예| 
|데이터 계층 응용 프로그램 구성 요소 작업 지원 - 추출, 배포, 업그레이드, 삭제|예|예|예|예| 
|정책 자동화(일정 및 변경 내용 검사)|예|예|예|아니오|아니요|   
|성능 데이터 수집기|예|예|예|아니오|아니요| 
|표준 성능 보고서|예|예|예|아니오|아니요| 
|계획 지침을 위한 계획 지침 및 계획 고정|예|예|예|아니오|아니요|   
|인덱스 뷰의 직접 쿼리(NOEXPAND 힌트 사용)|예|예|예|예| 
|인덱싱된 뷰의 자동 유지 관리|예|예|예|아니오|아니요| 
|분산형 분할 뷰|예|아니오|아니요|아니요| 
|병렬 인덱스 작업|예|아니오|아니요|아니요|  
|쿼리 최적화 프로그램의 인덱싱된 뷰 자동 사용|예|아니오|아니요|아니요| 
|병렬 일관성 검사|예|아니오|아니요|아니요| 
|SQL Server 유틸리티 제어 지점|예|아니오|아니요|아니요|    

##  <a name="Programmability"></a> Programmability  
  
|기능|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|예|예|예|예|   
|쿼리 저장소|예|예|예|예|   
|임시 테이블|예|예|예|예|   
|네이티브 XML 지원|예|예|예|예| 
|XML 인덱싱|예|예|예|예| 
|MERGE 및 UPSERT 기능|예|예|예|예|   
|날짜 및 시간 데이터 형식|예|예|예|예|  
|국제화 지원|예|예|예|예| 
|전체 텍스트 및 의미 체계 검색|예|예|예|예|아니요| 
|쿼리에서 언어 지정|예|예|예|예|아니요|   
|Service Broker(메시징)|예|예|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|   
|Transact-SQL 엔드포인트|예|예|예|아니오|아니요| 
|그래프|예|예|예|예|  


<sup>1</sup> 여러 계산 노드를 사용하는 확장에는 헤드 노드가 필요합니다.

## <a name="IS"></a> Integration Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]의 버전 별로 지원하는 Integration Services (SSIS) 기능에 대한 내용은, [SQL Server 버전 별로 지원하는 Integration Services 기능](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)을 참조하세요.

##  <a name="SLS"></a> 공간 및 위치 서비스  
  
|기능 이름|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|공간 인덱스|예|예|예|예|   
|평면 및 측지 데이터 형식|예|예|예|예| 
|고급 공간 라이브러리|예|예|예|예|   
|산업 표준 공간 데이터 형식 가져오기/내보내기|예|예|예|예|   

  
## <a name="next-steps"></a>다음 단계 
 [SQL Server 2017-Windows의 버전 및 지원하는 기능](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [SQL Server 2016-Windows의 버전 및 지원하는 기능](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [SQL Server 2014-Windows의 버전 및 지원하는 기능](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [SQL Server 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [SQL Server에 대한 제품 사양](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
