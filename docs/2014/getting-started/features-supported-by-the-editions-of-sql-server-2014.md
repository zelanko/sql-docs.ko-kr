---
title: SQL Server 2014 버전에서 지 원하는 기능 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- data-quality-services
- database-engine
- integration-services
- master-data-services
- reporting-services-native
- reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0652a2545f0b1e9d591777f0bcabe6395cf4feaa
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802657"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>SQL Server 2014 버전에서 지원하는 기능


  이 항목은 다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]버전에서 지원되는 기능의 세부 정보를 제공합니다. 

 > **참고:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 180 일 평가 기간 동안 평가 버전에서 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [평가판 소프트웨어 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=190955)를 참조하세요.  
> 
> **참고:** Evaluation 및 Developer 버전에서 지원하는 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 기능 집합을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기술과 관련된 표로 이동하려면 해당 링크를 클릭합니다.  
  
 [교차 상자 확장 제한](#CrossBoxScale)  
  
 [고가용성](#High_availability)  
  
 [확장성 및 성능](#Scalability)  
  
 [보안](#Enterprise_security)  
  
 [복제](#Replication)  
  
 [관리 도구](#Mgmt_Tools)  
  
 [RDBMS 관리 효율성](#RDBMS_mgmt)  
  
 [개발 도구](#Dev_tools)  
  
 [프로그래밍 기능](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services-고급 어댑터](#SSIS_AA)  
  
 [Integration Services-고급 변환](#SSIS_AT)  
  
 [MDS(Master Data Services)](#MDS)  
  
 [Data Warehouse](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI 의미 체계 모델 (다차원)](#BISemModel_multi)  
  
 [BI 의미 체계 모델(테이블 형식)](#BISemModel_tabular)  
  
 [SharePoint용 PowerPivot](#PowerPivot)  
  
 [데이터 마이닝](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Business Intelligence 클라이언트](#BIClients)  
  
 [공간 및 위치 서비스](#Spatial)  
  
 [추가 데이터베이스 서비스](#Add_DBServices)  
  
 [다른 구성 요소](#Other_Components)  
  
##  <a name="CrossBoxScale"></a> 교차 상자 확장 제한  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|단일 인스턴스에서 사용 되는 최대 계산 용량 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진)<sup>1</sup>|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|  
|(Analysis Services, Reporting Services) 단일 인스턴스에서 사용 되는 최대 계산 용량 <sup>1</sup>|운영 체제가 지원하는 최대 크기|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|  
|최대 메모리 사용량([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진의 인스턴스당)|운영 체제가 지원하는 최대 크기|128GB|128GB|64GB|1GB|1GB|1GB|  
|최대 메모리 사용량([!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스당)|운영 체제가 지원하는 최대 크기|운영 체제가 지원하는 최대 크기|64GB|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|최대 메모리 사용량([!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 인스턴스당)|운영 체제가 지원하는 최대 크기|운영 체제가 지원하는 최대 크기|64GB|64GB|4GB|해당 사항 없음|해당 사항 없음|  
|최대 관계형 데이터베이스 크기|524PB|524PB|524PB|524PB|10GB|10GB|10GB|  
  
 <sup>1</sup> Server + 클라이언트 액세스 라이선스 (CAL) 기반 라이선스가 (새 계약에 사용할 수 없음)를 사용 하 여 Enterprise Edition은 최대 20 개의 코어로 제한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스. 코어 기반 서버 라이선스 모델에서는 제한이 없습니다. 자세한 내용은 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)를 참조하세요.  
  
##  <a name="High_availability"></a> 고가용성  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Server Core 지원<sup>1</sup>|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|로그 전달|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|데이터베이스 미러링|사용자 계정 컨트롤|지원(Safety Full만)|지원(Safety Full만)|미러링 모니터만|미러링 모니터만|미러링 모니터만|미러링 모니터만|  
|백업 압축|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|데이터베이스 스냅숏|사용자 계정 컨트롤|||||||  
|AlwaysOn 장애 조치(failover) 클러스터 인스턴스|지원(노드 지원: 운영 체제가 지원하는 최대 크기|지원(노드 지원: 2)|지원(노드 지원: 2)|||||  
|AlwaysOn 가용성 그룹|예(2개의 동기 보조 복제본을 포함하여 최대 8개까지 보조 복제본 지원)|||||||  
|Connection Director|사용자 계정 컨트롤|||||||  
|온라인 페이지 및 파일 복원|사용자 계정 컨트롤|||||||  
|온라인 인덱싱|사용자 계정 컨트롤|||||||  
|온라인 스키마 변경|사용자 계정 컨트롤|||||||  
|빠른 복구|사용자 계정 컨트롤|||||||  
|미러된 백업|사용자 계정 컨트롤|||||||  
|Hot Add 메모리 및 CPU<sup>2</sup>|사용자 계정 컨트롤|||||||  
|데이터베이스 복구 관리자|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|암호화된 백업|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|스마트 백업|사용자 계정 컨트롤|예|예|아니요||||  
  
 <sup>1</sup>를 설치 하는 방법은 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Server core에서 참조 [Server Core에 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-on-server-core.md)합니다.  
  
 <sup>2</sup>이 기능은 에서만 사용할 수에 대 한 64 비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다.  
  
##  <a name="Scalability"></a> 확장성 및 성능  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|다중 인스턴스 지원|50|50|50|50|50|50|50|  
|테이블 및 인덱스 분할|사용자 계정 컨트롤|||||||  
|데이터 압축|사용자 계정 컨트롤|||||||  
|리소스 관리자|사용자 계정 컨트롤|||||||  
|파티션 테이블 병렬 처리|사용자 계정 컨트롤|||||||  
|여러 Filestream 컨테이너|사용자 계정 컨트롤|||||||  
|NUMA 인식 큰 페이지 메모리 및 버퍼 배열 할당|사용자 계정 컨트롤|||||||  
|버퍼 풀 확장 <sup>1</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|IO 리소스 관리|사용자 계정 컨트롤|||||||  
|메모리 내 OLTP <sup>1</sup>|사용자 계정 컨트롤|||||||  
|지연된 내구성|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
  
 <sup>1</sup> 이 기능은 에서만 사용할 수에 대 한 64 비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다.  
  
##  <a name="Enterprise_security"></a> 보안  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|기본 감사|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|미세 감사|사용자 계정 컨트롤|||||||  
|투명한 데이터베이스 암호화|사용자 계정 컨트롤|||||||  
|확장 가능 키 관리|사용자 계정 컨트롤|||||||  
|사용자 정의 역할|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|포함된 데이터베이스|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|백업을 위한 암호화|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
  
##  <a name="Replication"></a> Replication  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 변경 내용 추적|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|병합 복제|사용자 계정 컨트롤|예|사용자 계정 컨트롤|예(구독자만)|예(구독자만)|예(구독자만)|예(구독자만)|  
|트랜잭션 복제|사용자 계정 컨트롤|예|사용자 계정 컨트롤|예(구독자만)|예(구독자만)|예(구독자만)|예(구독자만)|  
|스냅숏 복제|사용자 계정 컨트롤|예|사용자 계정 컨트롤|예(구독자만)|예(구독자만)|예(구독자만)|예(구독자만)|  
|다른 유형의 구독자|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|Oracle 게시|사용자 계정 컨트롤|||||||  
|피어 투 피어 트랜잭션 복제|사용자 계정 컨트롤|||||||  
  
##  <a name="Mgmt_Tools"></a> Management Tools  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SMO(SQL Management Objects)|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|SQL 구성 관리자|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|SQL CMD(명령 프롬프트 도구)|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|사용자 계정 컨트롤|예|예|예|예|사용자 계정 컨트롤||  
|Distributed Replay - 관리 도구|사용자 계정 컨트롤|예|예|예|예|사용자 계정 컨트롤||  
|Distributed Replay - 클라이언트|사용자 계정 컨트롤|아니요|예|사용자 계정 컨트롤||||  
|Distributed Replay - 컨트롤러|예(Enterprise는 최대 16 클라이언트 지원, Developer는 1 클라이언트만 지원)|아니요|예(1 클라이언트만 지원)|예(1 클라이언트만 지원)||||  
|SQL 프로파일러|사용자 계정 컨트롤|예|사용자 계정 컨트롤|이상<sup>2</sup>|이상<sup>2</sup>|이상<sup>2</sup>|이상<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|Microsoft System Center Operations Manager 관리 팩|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|DTA(데이터베이스 튜닝 관리자)|사용자 계정 컨트롤|사용자 계정 컨트롤|예<sup>3</sup>|예<sup>3</sup>||||  
|Windows Azure VM 마법사에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 배포|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Windows Azure의 데이터 파일|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 웹 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]합니다 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Tools 및 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] Advanced Services를 사용 하 여 프로 파일링 할 수를 사용 하 여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 표준 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise edition.  
  
 <sup>3</sup> 튜닝은 Standard edition 기능 에서만 활성화 됩니다.  
  
##  <a name="RDBMS_mgmt"></a> RDBMS Manageability  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|사용자 인스턴스|||||사용자 계정 컨트롤|예|사용자 계정 컨트롤|  
|LocalDB|||||사용자 계정 컨트롤|사용자 계정 컨트롤||  
|관리자 전용 연결|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|지원(추적 플래그 사용)|지원(추적 플래그 사용)|지원(추적 플래그 사용)|  
|PowerShell 스크립팅 지원|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|SysPrep 지원<sup>1</sup>|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|지원 데이터 계층 응용 프로그램 구성 요소 작업-추출, 배포, 업그레이드, 삭제|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|정책 자동화(일정 및 변경 내용 검사)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|성능 데이터 수집기|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|다중 인스턴스 관리에서 관리되는 인스턴스로 등록 가능|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|표준 성능 보고서|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|계획 지침을 위한 계획 지침 및 계획 고정|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|인덱스 뷰의 직접 쿼리(NOEXPAND 힌트 사용)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|인덱싱된 뷰의 자동 유지 관리|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|분산형 분할 뷰|사용자 계정 컨트롤|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|부분 분산형 분할 뷰는 업데이트할 수 없음|  
|병렬 인덱스 작업|사용자 계정 컨트롤|||||||  
|쿼리 최적화 프로그램의 인덱싱된 뷰 자동 사용|사용자 계정 컨트롤|||||||  
|병렬 일관성 검사|사용자 계정 컨트롤|||||||  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 제어 지점|사용자 계정 컨트롤|||||||  
|포함된 데이터베이스|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|버퍼 풀 확장<sup>2</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
  
 <sup>1</sup> 자세한 내용은 [SysPrep을 사용하여 SQL Server 설치 시 고려 사항](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)을 참조하세요.  
  
 <sup>2</sup> 이 기능은 에서만 사용할 수에 대 한 64 비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다.  
  
##  <a name="Dev_tools"></a> Development Tools  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 통합|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|Intellisense([!INCLUDE[tsql](../includes/tsql-md.md)] 및 MDX)|사용자 계정 컨트롤|예|예|예|예|예|예|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|예|예|예|예|사용자 계정 컨트롤|||  
|SQL 쿼리, 편집 및 디자인 도구<sup>1</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|버전 제어 지원<sup>1</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|MDX 편집, 디버그 및 디자인 도구<sup>1</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
  
 <sup>1</sup> 이 기능은 64 비트 버전의 Standard edition에 제공 됩니다. 합니다.  
  
##  <a name="Programmability"></a> Programmability  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|CLR(공용 언어 런타임) 통합|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|네이티브 XML 지원|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|XML 인덱싱|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|MERGE 및 UPSERT 기능|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|FILESTREAM 지원|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|FileTable|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|날짜 및 시간 데이터 형식|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|국제화 지원|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|전체 텍스트 및 의미 체계 검색|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|쿼리에서 언어 지정|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|Service Broker(메시징)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|  
|[!INCLUDE[tsql](../includes/tsql-md.md)] 엔드포인트|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|기능|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|기본 제공 데이터 원본 커넥터|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|SSIS 디자이너 및 런타임|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|기본 변환|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|기본 데이터 프로파일링 도구|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|Attunity Oracle CDC Service|사용자 계정 컨트롤|||||||  
|Change Data Capture Designer for Oracle by Attunity|사용자 계정 컨트롤|||||||  
  
###  <a name="SSIS_AA"></a> Integration Services - 고급 어댑터  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|성능 우선 Oracle 대상|사용자 계정 컨트롤|||||||  
|성능 우선 Teradata 대상|사용자 계정 컨트롤|||||||  
|SAP BW 원본 및 대상|사용자 계정 컨트롤|||||||  
|데이터 마이닝 모델 학습 대상 어댑터|사용자 계정 컨트롤|||||||  
|차원 처리 대상 어댑터|사용자 계정 컨트롤|||||||  
|파티션 처리 대상 어댑터|사용자 계정 컨트롤|||||||  
|Attunity의 변경 데이터 캡처 구성 요소|사용자 계정 컨트롤|||||||  
|Attunity의 Connector for ODBC(Open Database Connectivity)|사용자 계정 컨트롤|||||||  
  
###  <a name="SSIS_AT"></a> Integration Services - 고급 변환  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|지속성(성능 우선) 조회|사용자 계정 컨트롤|||||||  
|데이터 마이닝 쿼리 변환|사용자 계정 컨트롤|||||||  
|유사 항목 그룹화 및 조회 변환|사용자 계정 컨트롤|||||||  
|용어 추출 및 조회 변환|사용자 계정 컨트롤|||||||  
  
##  <a name="MDS"></a> Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]는 Business Intelligence 및 Enterprise 64비트 버전에서만 사용할 수 있습니다.  
  
|기능|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
##  <a name="Data_warehouse"></a> Data Warehouse  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|데이터베이스 없이 큐브 만들기|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|준비 및 데이터 웨어하우스 스키마 자동 생성|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|변경 데이터 캡처|사용자 계정 컨트롤|||||||  
|스타 조인 쿼리 최적화|사용자 계정 컨트롤|||||||  
|확장 가능한 읽기 전용 Analysis Services 구성|사용자 계정 컨트롤|||||||  
|분할된 테이블 및 인덱스의 병렬 쿼리 처리|사용자 계정 컨트롤|||||||  
|xVelocity 메모리 최적화 columnstore 인덱스|사용자 계정 컨트롤|||||||  
|글로벌 일괄 집계|사용자 계정 컨트롤|||||||  
  
##  <a name="SSAS"></a> Analysis Services  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|확장 가능한 공유 데이터베이스(연결/분리, 읽기 전용 데이터베이스)|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|데이터베이스 백업/복원 및 연결/분리|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|데이터베이스 동기화|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|고가용성|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|프로그래밍 기능(AMO, ADOMD.Net, OLEDB, XML/A, ASSL)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
  
###  <a name="BISemModel_multi"></a> BI 의미 체계 모델 (다차원)  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|반가산적 측정값|사용자 계정 컨트롤|사용자 계정 컨트롤|No<sup>1</sup>|||||  
|계층 구조|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|KPI|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|큐브 뷰|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|동작|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|계정 인텔리전스|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|시간 인텔리전스|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|사용자 지정 롤업|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|큐브 쓰기 저장(writeback)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|차원 쓰기 저장(Writeback)|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|셀 쓰기 저장(writeback)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|드릴스루|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|고급 계층 유형(부모-자식, 비정형 계층 구조)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|고급 차원(참조 차원, 다 대 다 차원|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|연결된 측정값 및 차원|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|Translations|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|Aggregations|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|여러 파티션|사용자 계정 컨트롤|사용자 계정 컨트롤|예, 최대 3|||||  
|자동 관리 캐싱|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|사용자 지정 어셈블리(저장 프로시저)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|MDX 쿼리 및 스크립트|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|DAX 쿼리|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|역할 기반 보안 모델|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|차원 및 셀 수준 보안|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|확장 가능 문자열 스토리지|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|MOLAP, ROLAP, HOLAP 스토리지 모델|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|이진 및 압축 XML 전송|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|밀어넣기 모드 처리|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|직접 쓰기 저장(writeback)|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|측정값 식|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
 <sup>1</sup>standard edition에서 LastChild 반 가산적 측정값은 지원 되지만 None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren 및 ByAccount와 같은 다른 반 가산적 측정값 없습니다. Sum, Count, Min, Max와 같은 가산적 측정값과 비가산적 측정값(DistinctCount)은 모든 버전에서 지원됩니다.  
  
###  <a name="BISemModel_tabular"></a> BI Semantic Model (Tabular)  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|계층 구조|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|KPI|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|큐브 뷰|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|Translations|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|DAX 계산, DAX 쿼리, MDX 쿼리|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|행 수준 보안|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|파티션|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|메모리 내 및 DirectQuery 스토리지 모드(테이블 형식만 해당)|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
###  <a name="PowerPivot"></a> SharePoint 용 PowerPivot  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|공유 서비스 아키텍처를 기반으로 하는 SharePoint 팜 통합|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|사용 보고|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|상태 모니터링 규칙|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|PowerPivot 갤러리|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|PowerPivot 데이터 새로 고침|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|PowerPivot 데이터 피드|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
###  <a name="DataMining"></a> Data Mining  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|표준 알고리즘|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|데이터 마이닝 도구(마법사, 편집기, 쿼리 작성기)|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|교차 유효성 검사|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|마이닝 구조 데이터의 필터링된 하위 집합에 대한 모델|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|시계열: ARTXP 및 ARIMA 방식 간의 사용자 지정 혼합|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|시계열: 새 데이터를 사용한 예측|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|무제한 동시 DM 쿼리|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|데이터 마이닝 알고리즘용 고급 구성 및 튜닝 옵션|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|플러그 인 알고리즘 지원|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|병렬 모델 처리|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|시계열: 계열 간 예측|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|연결 규칙에 대한 무제한 특성|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|시퀀스 예측|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|Naive Bayes, 신경망, 로지스틱 회귀를 위한 다중 예측 대상|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
##  <a name="Reporting"></a> Reporting  Services  
  
###  <a name="Reporting_features"></a> Reporting Services 기능  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|지원되는 카탈로그 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Standard 이상|Standard 이상|Standard 이상|Web|Express|||  
|지원되는 데이터 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Web|Express|||  
|보고서 서버|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|보고서 디자이너|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|보고서 관리자|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|역할 기반 보안|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|Word 내보내기 및 서식 있는 텍스트 지원|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|향상된 계기 및 차트|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|Excel, PDF 및 이미지로 내보내기|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|사용자 지정 인증|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|데이터 피드로 보고서 사용|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|||  
|모델 지원|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
|역할 기반 보안을 위해 사용자 지정 역할 만들기|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|모델 항목 보안|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|무한 클릭 광고|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|공유 구성 요소 라이브러리|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|전자 메일 및 파일 공유 구독/일정 예약|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|보고서 기록, 스냅숏 실행 및 캐싱|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|SharePoint 통합|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|원격 및 비 SQL 데이터 원본 지원<sup>1</sup>|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|데이터 원본, 배달 및 렌더링, RDCE 확장성|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|데이터 기반 보고서 구독|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|확장 배포(웹 팜)|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|경고<sup>2</sup>|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
 <sup>1</sup>지원 되는 데이터 원본에 대 한 자세한 내용은 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]를 참조 하십시오 [Data Sources Supported by Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 <sup>2</sup>필요 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드에서. 자세한 내용은 [Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)합니다.  
  
### <a name="report-server-database-server-edition-requirements"></a>보고서 서버 데이터베이스 서버 버전 요구 사항  
 보고서 서버 데이터베이스를 만들 때 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전은 데이터베이스 호스팅에 사용할 수 없습니다. 다음 표에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 특정 버전에 사용할 수 있는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]버전을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 버전|데이터베이스 호스팅에 사용할 데이터베이스 엔진 인스턴스 버전|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard, Business Intelligence Enterprise 버전(로컬 또는 원격)|  
|Business Intelligence|Standard, Business Intelligence Enterprise 버전(로컬 또는 원격)|  
|표준|Standard, Enterprise Edition(로컬 또는 원격)|  
|Web|Web Edition(로컬 전용)|  
|Express with Advanced Services|Express with Advanced Services(로컬 전용)|  
|Evaluation|Evaluation|  
  
##  <a name="BIClients"></a> Business Intelligence 클라이언트  
 Microsoft 다운로드 센터에서 제공하는 다음 소프트웨어 클라이언트 애플리케이션을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행되는 비즈니스 인텔리전스 문서를 손쉽게 만들 수 있습니다. 이러한 문서를 서버 환경에서 호스팅하려는 경우 해당 문서 유형을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 사용하세요. 다음 표에서는 이러한 클라이언트 애플리케이션에서 만든 문서를 호스팅하는 데 필요한 서버 기능이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 보여 줍니다.  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|Excel 및 Visio 2010용 데이터 마이닝 추가 기능|사용자 계정 컨트롤|예|사용자 계정 컨트롤|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] Excel 추가 기능 및 종속 되지 않는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 그러나 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]은 SharePoint에서 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]통합 문서를 공유하고 공동 작업하는 데 필요하며 이 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 및 Business Intelligence 버전의 일부로 사용할 수 있습니다.  
> 2.  위의 표는 이러한 클라이언트 도구를 활성화하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 식별하지만 이러한 기능은 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서 호스팅되는 데이터에 액세스할 수 있습니다.  
  
##  <a name="Spatial"></a> Spatial and Location Services  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|공간 인덱스|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|평면 및 측지 데이터 형식|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|고급 공간 라이브러리|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|산업 표준 공간 데이터 형식 가져오기/내보내기|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
  
##  <a name="Add_DBServices"></a> Additional Database Services  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|사용자 계정 컨트롤|예|예|예|예|예|사용자 계정 컨트롤|  
|데이터베이스 메일|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤||||  
  
##  <a name="Other_Components"></a> 기타 구성 요소  
  
|기능 이름|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data  Quality  Services|사용자 계정 컨트롤|사용자 계정 컨트롤||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 제품 사양](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [SQL Server 2014 설치](../database-engine/install-windows/installation-for-sql-server.md)   
 [SQL Server 2014 빠른 시작 설치](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
