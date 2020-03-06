---
title: SQL Server 2014 버전에서 지 원하는 기능 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caae4212e2182ae6afde29b0fed1aaee4f05645a
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339298"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>SQL Server 2014 버전에서 지원하는 기능


  이 항목은 다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]버전에서 지원되는 기능의 세부 정보를 제공합니다. 

 > **참고:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 180 일의 평가 기간에 대 한 평가 버전에서 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [평가판 소프트웨어 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=190955)를 참조하세요.  
> 
> **참고:** Evaluation 및 Developer 버전에서 지 원하는 기능은 Enterprise 기능 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 집합을 참조 하세요.  
  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기술과 관련된 표로 이동하려면 해당 링크를 클릭합니다.  
  
 [교차 상자 크기 제한](#CrossBoxScale)  
  
 [고가용성](#High_availability)  
  
 [확장성 및 성능](#Scalability)  
  
 [보안](#Enterprise_security)  
  
 [복제](#Replication)  
  
 [관리 도구](#Mgmt_Tools)  
  
 [RDBMS 관리 효율](#RDBMS_mgmt)  
  
 [개발 도구](#Dev_tools)  
  
 [프로그래밍](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services - 고급 어댑터](#SSIS_AA)  
  
 [Integration Services - 고급 변환](#SSIS_AT)  
  
 [Master  Data  Services](#MDS)  
  
 [데이터 웨어하우스](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI 의미 체계 모델(다차원)](#BISemModel_multi)  
  
 [BI 의미 체계 모델 (테이블 형식)](#BISemModel_tabular)  
  
 [SharePoint용 PowerPivot](#PowerPivot)  
  
 [데이터 마이닝](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [비즈니스 인텔리전스 클라이언트](#BIClients)  
  
 [공간 및 위치 서비스](#Spatial)  
  
 [추가 데이터베이스 서비스](#Add_DBServices)  
  
 [기타 구성 요소](#Other_Components)  
  
##  <a name="CrossBoxScale"></a>교차 상자 크기 제한  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|단일 인스턴스에서 사용되는 최대 컴퓨팅 용량([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진)<sup>1</sup>|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|  
|단일 인스턴스에서 사용되는 최대 컴퓨팅 용량(Analysis Services, Reporting Services)<sup>1</sup>|운영 체제가 지원하는 최대 크기|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|  
|최대 메모리 사용량( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진의 인스턴스당)|운영 체제가 지원하는 최대 크기|128GB|128GB|64GB|1 GB|1 GB|1 GB|  
|최대 메모리 사용량( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스당)|운영 체제가 지원하는 최대 크기|운영 체제가 지원하는 최대 크기|64GB|해당 없음|해당 없음|해당 없음|해당 없음|  
|최대 메모리 사용량( [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 인스턴스당)|운영 체제가 지원하는 최대 크기|운영 체제가 지원하는 최대 크기|64GB|64GB|4GB|해당 없음|해당 없음|  
|최대 관계형 데이터베이스 크기|524PB|524PB|524PB|524PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> SERVER + CAL (클라이언트 액세스 라이선스) 기반 라이선스가 포함 된 Enterprise Edition (새 계약에 사용할 수 없음)은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스당 최대 20 개의 코어로 제한 됩니다. 코어 기반 서버 라이선스 모델에서는 제한이 없습니다. 자세한 내용은 [SQL Server의 버전별 계산 용량 제한](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조 하세요.  
  
##  <a name="High_availability"></a>고가용성  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Server Core 지원<sup>1</sup>|예|예|예|예|예|예|예|  
|로그 전달|예|예|예|예||||  
|데이터베이스 미러링|예|지원(Safety Full만)|지원(Safety Full만)|미러링 모니터만|미러링 모니터만|미러링 모니터만|미러링 모니터만|  
|백업 압축|예|예|예|||||  
|데이터베이스 스냅샷|예|||||||  
|AlwaysOn 장애 조치(failover) 클러스터 인스턴스|지원(노드 지원: 운영 체제가 지원하는 최대 크기)|지원(노드 지원: 2)|지원(노드 지원: 2)|||||  
|AlwaysOn 가용성 그룹|예(2개의 동기 보조 복제본을 포함하여 최대 8개까지 보조 복제본 지원)|||||||  
|Connection Director|예|||||||  
|온라인 페이지 및 파일 복원|예|||||||  
|온라인 인덱싱|예|||||||  
|온라인 스키마 변경|예|||||||  
|빠른 복구|예|||||||  
|미러된 백업|예|||||||  
|Hot Add 메모리 및 CPU<sup>2</sup>|예|||||||  
|데이터베이스 복구 관리자|예|예|예|예|예|예|예|  
|암호화된 백업|예|예|예|||||  
|스마트 백업|예|예|예|예||||  
  
 <sup>1</sup> Server Core에 설치 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 하는 방법에 대 한 자세한 내용은 [server core에 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-on-server-core.md)를 참조 하세요.  
  
 <sup>2</sup> 이 기능은 64 비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에만 사용할 수 있습니다.  
  
##  <a name="Scalability"></a>확장성 및 성능  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|다중 인스턴스 지원|50|50|50|50|50|50|50|  
|테이블 및 인덱스 분할|예|||||||  
|데이터 압축|yes|||||||  
|관리|yes|||||||  
|파티션 테이블 병렬 처리|예|||||||  
|여러 Filestream 컨테이너|예|||||||  
|NUMA 인식 큰 페이지 메모리 및 버퍼 배열 할당|예|||||||  
|버퍼 풀 확장 <sup>1</sup>|예|예|예|||||  
|IO 리소스 관리|예|||||||  
|메모리 내 OLTP <sup>1</sup>|예|||||||  
|지연된 내구성|예|예|예|예|예|예|예|  
  
 <sup>1</sup> 이 기능은 64 비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에만 사용할 수 있습니다.  
  
##  <a name="Enterprise_security"></a> 보안  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|기본 감사|예|예|예|예|예|예|예|  
|미세 감사|예|||||||  
|투명한 데이터베이스 암호화|yes|||||||  
|확장 가능 키 관리|예|||||||  
|사용자 정의 역할|예|예|예|예|예|예|예|  
|포함된 데이터베이스|예|예|예|예|예|예|예|  
|백업을 위한 암호화|예|예|예|||||  
  
##  <a name="Replication"></a> 복제  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]변경 내용 추적|예|예|예|예|예|예|예|  
|병합 복제|예|예|예|예(구독자만)|예(구독자만)|예(구독자만)|예(구독자만)|  
|트랜잭션 복제|예|예|예|예(구독자만)|예(구독자만)|예(구독자만)|예(구독자만)|  
|스냅샷 복제|예|예|예|예(구독자만)|예(구독자만)|예(구독자만)|예(구독자만)|  
|다른 유형의 구독자|예|예|예|||||  
|Oracle 게시|예|||||||  
|피어 투 피어 트랜잭션 복제|예|||||||  
  
##  <a name="Mgmt_Tools"></a>관리 도구  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SMO(SQL Management Objects)|예|예|예|예|예|예|예|  
|SQL 구성 관리자|예|예|예|예|예|예|예|  
|SQL CMD(명령 프롬프트 도구)|예|예|예|예|예|예|예|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Management Studio|예|예|예|예|예|예||  
|Distributed Replay - 관리 도구|예|예|예|예|예|예||  
|Distributed Replay - 클라이언트|예|예|예|예||||  
|Distributed Replay - 컨트롤러|예(Enterprise는 최대 16 클라이언트 지원, Developer는 1 클라이언트만 지원)|예|예(1 클라이언트만 지원)|예(1 클라이언트만 지원)||||  
|SQL 프로파일러|예|예|예|아니요<sup>2</sup>|아니요<sup>2</sup>|아니요<sup>2</sup>|아니요<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트|예|예|예|예||||  
|Microsoft System Center Operations Manager 관리 팩|예|예|예|예||||  
|DTA(데이터베이스 튜닝 관리자)|예|예|예<sup>3</sup>|예<sup>3</sup>||||  
|Azure VM [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 데이터베이스 배포 마법사|예|예|예|예|예|예|예|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Azure의 데이터 파일|예|예|예|예|예|예|예|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard 및 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] edition을 사용 하 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web,, with Tools 및 with Advanced Services를 프로 파일링 할 수 있습니다.  
  
 <sup>3</sup> 튜닝은 Standard edition 기능 에서만 사용할 수 있습니다.  
  
##  <a name="RDBMS_mgmt"></a>RDBMS 관리 효율  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|사용자 인스턴스|||||예|예|예|  
|LocalDB|||||예|예||  
|관리자 전용 연결|예|예|예|예|지원(추적 플래그 사용)|지원(추적 플래그 사용)|지원(추적 플래그 사용)|  
|PowerShell 스크립팅 지원|예|예|예|예|예|예|예|  
|SysPrep 지원<sup>1</sup>|예|예|예|예|예|예|예|  
|데이터 계층 응용 프로그램 구성 요소 작업 지원-추출, 배포, 업그레이드, 삭제|예|예|예|예|예|예|예|  
|정책 자동화(일정 및 변경 내용 검사)|예|예|예|예||||  
|성능 데이터 수집기|예|예|예|예||||  
|다중 인스턴스 관리에서 관리되는 인스턴스로 등록 가능|예|예|예|예||||  
|표준 성능 보고서|예|예|예|예||||  
|계획 지침을 위한 계획 지침 및 계획 고정|예|예|예|예||||  
|인덱스 뷰의 직접 쿼리(NOEXPAND 힌트 사용)|예|예|예|예||||  
|인덱싱된 뷰의 자동 유지 관리|예|예|예|예||||  
|분산형 분할 뷰|yes|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|  
|병렬 인덱스 작업|예|||||||  
|쿼리 최적화 프로그램의 인덱싱된 뷰 자동 사용|예|||||||  
|병렬 일관성 검사|예|||||||  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 제어 지점|예|||||||  
|포함된 데이터베이스|예|예|예|예|예|예|예|  
|버퍼 풀 확장<sup>2</sup>|예|예|예|||||  
  
 <sup>1</sup> 자세한 내용은 [SysPrep을 사용 하 여 SQL Server 설치에 대 한 고려 사항](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)을 참조 하세요.  
  
 <sup>2</sup> 이 기능은 64 비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에만 사용할 수 있습니다.  
  
##  <a name="Dev_tools"></a>개발 도구  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)]Visual Studio 통합|예|예|예|예|예|예|예|  
|Intellisense([!INCLUDE[tsql](../includes/tsql-md.md)] 및 MDX)|예|예|예|예|예|예|예|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|예|예|예|예|예|||  
|SQL 쿼리 편집 및 디자인 도구<sup>1</sup>|예|예|예|||||  
|버전 제어 지원<sup>1</sup>|예|예|예|||||  
|MDX 편집, 디버그 및 디자인 도구<sup>1</sup>|예|예|예|||||  
  
 <sup>1</sup> 이 기능은 Standard edition의 64 비트 버전에는 사용할 수 없습니다.  
  
##  <a name="Programmability"></a> Programmability  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|CLR(공용 언어 런타임) 통합|예|예|예|예|예|예|예|  
|네이티브 XML 지원|예|예|예|예|예|예|예|  
|XML 인덱싱|예|예|예|예|예|예|예|  
|MERGE & UPSERT 기능|예|예|예|예|예|예|예|  
|FILESTREAM 지원|예|예|예|예|예|예|예|  
|FileTable|예|예|예|예|예|예|예|  
|날짜 및 시간 데이터 형식|예|예|예|예|예|예|예|  
|국제화 지원|예|예|예|예|예|예|예|  
|전체 텍스트 및 의미 체계 검색|예|예|예|예|예|||  
|쿼리에서 언어 지정|예|예|예|예|예|||  
|Service Broker(메시징)|예|예|예|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]종점|예|예|예|예||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|기능|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사|예|예|예|예|예|예|예|  
|기본 제공 데이터 원본 커넥터|예|예|예|예|예|예|예|  
|SSIS 디자이너 및 런타임|예|예|예|||||  
|기본 변환|예|예|예|||||  
|기본 데이터 프로파일링 도구|예|예|예|||||  
|Attunity Oracle CDC Service|예|||||||  
|Change Data Capture Designer for Oracle by Attunity|예|||||||  
  
###  <a name="SSIS_AA"></a>Integration Services-고급 어댑터  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|성능 우선 Oracle 대상|예|||||||  
|성능 우선 Teradata 대상|예|||||||  
|SAP BW 원본 및 대상|예|||||||  
|데이터 마이닝 모델 학습 대상 어댑터|예|||||||  
|차원 처리 대상 어댑터|예|||||||  
|파티션 처리 대상 어댑터|예|||||||  
|Attunity의 변경 데이터 캡처 구성 요소|예|||||||  
|Attunity의 Connector for ODBC(Open Database Connectivity)|예|||||||  
  
###  <a name="SSIS_AT"></a>Integration Services-고급 변환  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|지속성(성능 우선) 조회|예|||||||  
|데이터 마이닝 쿼리 변환|예|||||||  
|유사 항목 그룹화 및 조회 변환|예|||||||  
|용어 추출 및 조회 변환|예|||||||  
  
##  <a name="MDS"></a>MDS(Master Data Services)  
  
> [!NOTE]  
>  -   
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]는 Business Intelligence 및 Enterprise 64비트 버전에서만 사용할 수 있습니다.  
  
|기능|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]데이터|예|예||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]웹 응용 프로그램|예|예||||||  
  
##  <a name="Data_warehouse"></a>데이터 웨어하우스  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|데이터베이스 없이 큐브 만들기|예|예|예|||||  
|준비 및 데이터 웨어하우스 스키마 자동 생성|예|예|예|||||  
|변경 데이터 캡처|예|||||||  
|스타 조인 쿼리 최적화|예|||||||  
|확장 가능한 읽기 전용 Analysis Services 구성|예|||||||  
|분할된 테이블 및 인덱스의 병렬 쿼리 처리|예|||||||  
|xVelocity 메모리 최적화 columnstore 인덱스|예|||||||  
|글로벌 일괄 집계|예|||||||  
  
##  <a name="SSAS"></a>Analysis Services  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|확장 가능한 공유 데이터베이스(연결/분리, 읽기 전용 데이터베이스)|예|예||||||  
|백업/복원, 데이터베이스 연결/분리|예|예|예|||||  
|데이터베이스 동기화|예|예||||||  
|고가용성|예|예|예|||||  
|프로그래밍 기능(AMO, ADOMD.Net, OLEDB, XML/A, ASSL)|예|예|예|||||  
  
###  <a name="BISemModel_multi"></a>BI 의미 체계 모델 (다차원)  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|반가산적 측정값|예|예|아니요<sup>1</sup>|||||  
|계층 구조|예|예|예|||||  
|KPI|예|예|예|||||  
|큐브 뷰|예|예||||||  
|동작|예|예|예|||||  
|계정 인텔리전스|예|예|예|||||  
|시간 인텔리전스|예|예|예|||||  
|사용자 지정 롤업|예|예|예|||||  
|큐브 쓰기 저장(writeback)|예|예|예|||||  
|차원 쓰기 저장(Writeback)|예|예||||||  
|셀 쓰기 저장(writeback)|예|예|예|||||  
|드릴스루|예|예|예|||||  
|고급 계층 유형(부모-자식, 비정형 계층 구조)|예|예|예|||||  
|고급 차원(참조 차원, 다 대 다 차원|예|예|예|||||  
|연결된 측정값 및 차원|예|예||||||  
|Translations|예|예|예|||||  
|집계|예|예|예|||||  
|여러 파티션|예|예|예, 최대 3|||||  
|자동 관리 캐싱|예|예||||||  
|사용자 지정 어셈블리(저장 프로시저)|예|예|예|||||  
|MDX 쿼리 및 스크립트|예|예|예|||||  
|DAX 쿼리|예|예||||||  
|역할 기반 보안 모델|예|예|예|||||  
|차원 및 셀 수준 보안|예|예|예|||||  
|확장 가능 문자열 스토리지|예|예|예|||||  
|MOLAP, ROLAP, HOLAP 스토리지 모델|예|예|예|||||  
|이진 및 압축 XML 전송|예|예|예|||||  
|밀어넣기 모드 처리|예|예||||||  
|직접 쓰기 저장(writeback)|예|예||||||  
|측정값 식|예|예||||||  
  
 <sup>1</sup> LastChild 반 가산적 측정값은 standard edition에서 지원 되지만 None, FirstChild, FirstNonEmpty 있지 않음, LastNonEmpty 있지 않음, AverageOfChildren 및 ByAccount와 같은 다른 반 가산적 측정값은 지원 되지 않습니다. Sum, Count, Min, Max와 같은 가산적 측정값과 비가산적 측정값(DistinctCount)은 모든 버전에서 지원됩니다.  
  
###  <a name="BISemModel_tabular"></a>BI 의미 체계 모델 (테이블 형식)  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|계층 구조|예|예||||||  
|KPI|예|예||||||  
|큐브 뷰|예|예||||||  
|Translations|예|예||||||  
|DAX 계산, DAX 쿼리, MDX 쿼리|예|예||||||  
|행 수준 보안|예|예||||||  
|파티션|예|예||||||  
|메모리 내 및 DirectQuery 스토리지 모드(테이블 형식만 해당)|예|예||||||  
  
###  <a name="PowerPivot"></a>SharePoint용 PowerPivot  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|공유 서비스 아키텍처를 기반으로 하는 SharePoint 팜 통합|예|예||||||  
|사용량 보고|예|예||||||  
|상태 모니터링 규칙|예|예||||||  
|PowerPivot 갤러리|예|예||||||  
|PowerPivot 데이터 새로 고침|예|예||||||  
|PowerPivot 데이터 피드|예|예||||||  
  
###  <a name="DataMining"></a>데이터 마이닝  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|표준 알고리즘|예|예|예|||||  
|데이터 마이닝 도구(마법사, 편집기, 쿼리 작성기)|예|예|예|||||  
|교차 유효성 검사|예|예||||||  
|마이닝 구조 데이터의 필터링된 하위 집합에 대한 모델|예|예||||||  
|시계열: ARTXP 및 ARIMA 방식 간의 사용자 지정 혼합|예|예||||||  
|시계열: 새 데이터를 사용한 예측|예|예||||||  
|무제한 동시 DM 쿼리|예|예||||||  
|데이터 마이닝 알고리즘에 대 한 고급 구성 & 튜닝 옵션|예|예||||||  
|플러그 인 알고리즘 지원|예|예||||||  
|병렬 모델 처리|예|예||||||  
|시계열: 계열 간 예측|예|예||||||  
|연결 규칙에 대한 무제한 특성|예|예||||||  
|시퀀스 예측|예|예||||||  
|Naive Bayes, 신경망, 로지스틱 회귀를 위한 다중 예측 대상|예|예||||||  
  
##  <a name="Reporting"></a>Reporting Services  
  
###  <a name="Reporting_features"></a>Reporting Services 기능  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|지원되는 카탈로그 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Standard 이상|Standard 이상|Standard 이상|웹|Express|||  
|지원되는 데이터 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|웹|Express|||  
|보고서 서버|예|예|예|예|예|||  
|보고서 디자이너|예|예|예|예|예|||  
|보고서 관리자|예|예|예|예|예|||  
|역할 기반 보안|예|예|예|예|예|||  
|Word 내보내기 및 서식 있는 텍스트 지원|예|예|예|예|예|||  
|향상된 계기 및 차트|예|예|예|예|예|||  
|Excel, PDF 및 이미지로 내보내기|예|예|예|예|예|||  
|사용자 지정 인증|예|예|예|예|예|||  
|데이터 피드로 보고서 사용|예|예|예|예|예|||  
|모델 지원|예|예|예|예||||  
|역할 기반 보안을 위해 사용자 지정 역할 만들기|예|예|예|||||  
|모델 항목 보안|예|예|예|||||  
|무한 클릭 광고|예|예|예|||||  
|공유 구성 요소 라이브러리|예|예|예|||||  
|전자 메일 및 파일 공유 구독/일정 예약|예|예|예|||||  
|보고서 기록, 스냅샷 실행 및 캐싱|예|예|예|||||  
|SharePoint 통합|예|예|예|||||  
|원격 및 비 SQL 데이터 원본 지원<sup>1</sup>|예|예|예|||||  
|데이터 원본, 배달 및 렌더링, RDCE 확장성|예|예|예|||||  
|데이터 기반 보고서 구독|예|예||||||  
|확장 배포(웹 팜)|예|예||||||  
|경고<sup>2</sup>|예|예||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]<sup>2</sup>|예|예||||||  
  
 <sup>1</sup> 에서 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]지원 되는 데이터 원본에 대 한 자세한 내용은 [SSRS&#41;&#40;Reporting Services에서 지 원하는 데이터 원본 ](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조 하세요.  
  
 <sup>2</sup> SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 모드의가 필요 합니다. 자세한 내용은 sharepoint [모드 설치 &#40;sharepoint 2010 및 sharepoint 2013&#41;Reporting Services ](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)를 참조 하세요.  
  
### <a name="report-server-database-server-edition-requirements"></a>보고서 서버 데이터베이스 서버 버전 요구 사항  
 보고서 서버 데이터베이스를 만들 때 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전은 데이터베이스 호스팅에 사용할 수 없습니다. 다음 표에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 특정 버전에 사용할 수 있는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]버전을 보여 줍니다.  
  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 버전|데이터베이스 호스팅에 사용할 데이터베이스 엔진 인스턴스 버전|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard, Business Intelligence Enterprise 버전(로컬 또는 원격)|  
|비즈니스 인텔리전스|Standard, Business Intelligence Enterprise 버전(로컬 또는 원격)|  
|Standard|Standard, Enterprise Edition(로컬 또는 원격)|  
|웹|Web Edition(로컬 전용)|  
|Express with Advanced Services|Express with Advanced Services(로컬 전용)|  
|평가|평가|  
  
##  <a name="BIClients"></a>비즈니스 인텔리전스 클라이언트  
 Microsoft 다운로드 센터에서 제공하는 다음 소프트웨어 클라이언트 애플리케이션을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행되는 비즈니스 인텔리전스 문서를 손쉽게 만들 수 있습니다. 이러한 문서를 서버 환경에서 호스팅하려는 경우 해당 문서 유형을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 사용하세요. 다음 표에서는 이러한 클라이언트 애플리케이션에서 만든 문서를 호스팅하는 데 필요한 서버 기능이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 보여 줍니다.  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|예|예|예|||||  
|Excel 및 Visio 2010용 데이터 마이닝 추가 기능|예|예|예|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]2010|예|예||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|예|예||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]는 Excel 추가 기능이 며에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]종속 되지 않습니다. 그러나 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 은 SharePoint에서 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 공유하고 공동 작업하는 데 필요하며 이 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 및 Business Intelligence 버전의 일부로 사용할 수 있습니다.  
> 2.  위의 표는 이러한 클라이언트 도구를 활성화하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 식별하지만 이러한 기능은 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서 호스팅되는 데이터에 액세스할 수 있습니다.  
  
##  <a name="Spatial"></a>공간 및 위치 서비스  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|공간 인덱스|예|예|예|예|예|예|예|  
|평면 및 측지 데이터 형식|예|예|예|예|예|예|예|  
|고급 공간 라이브러리|예|예|예|예|예|예|예|  
|산업 표준 공간 데이터 형식 가져오기/내보내기|예|예|예|예|예|예|예|  
  
##  <a name="Add_DBServices"></a>추가 데이터베이스 서비스  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|예|예|예|예|예|예|예|  
|데이터베이스 메일|예|예|예|예||||  
  
##  <a name="Other_Components"></a>기타 구성 요소  
  
|기능 이름|Enterprise|비즈니스 인텔리전스|Standard|웹|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|데이터베이스 엔진 서비스|예|예||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014에 대 한 제품 사양](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [SQL Server 2014 설치](../database-engine/install-windows/installation-for-sql-server.md)   
 [SQL Server 2014 빠른 시작 설치](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
