---
title: SQL Server 2016의 새로운 기능
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql
ms.prod_service: sql
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- 새 SQL Server
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 224
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: c75528700e090c125f90aad47213d1a2e5332c30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33036521"
---
# <a name="whats-new-in-sql-server-2016"></a>SQL Server 2016의 새로운 기능
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  
 SQL Server 2016을 사용하면 메모리 내 성능 및 고급 보안부터 데이터베이스 내 분석까지 모든 기능이 기본 제공된 확장 가능한 하이브리드 데이터베이스 플랫폼을 사용하여 지능형 중요 업무용 응용 프로그램을 빌드할 수 있습니다. SQL Server 2016 릴리스에는 다양한 개선 사항 및 향상된 기능과 함께 새로운 보안 기능, 쿼리 기능, Hadoop 및 클라우드 통합, R 분석 등이 추가되어 있습니다. 

이 페이지에서는 각 SQL Server 구성 요소에 대해 SQL Server 2016의 새로운 기능에 대한 자세한 정보를 확인할 수 있는 요약 정보 및 링크를 제공합니다. 

![SQL Server 2016](../sql-server/media/sql-server-2016.png) 

 **SQL Server를 지금 사용해 보세요.** 
- **무료** [**SQL Server 2016 Developer 버전**](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers)을 다운로드하세요.
- 최신 버전의 [SQL Server Management Studio(SSMS)](../ssms/download-sql-server-management-studio-ssms.md)를 다운로드하세요. 
- Azure 계정이 있으세요? 
  [SQL Server 2016이 이미 설치된 가상 머신](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)을 설정하세요.

## <a name="sql-server-2016-database-engine"></a>SQL Server 2016 데이터베이스 엔진
- 이제 SQL Server 설치 및 설정 중에 **여러 tempDB** 데이터베이스 파일을 구성할 수 있습니다.
- 새 **쿼리 저장소**는 쿼리 텍스트, 실행 계획 및 성능 메트릭을 데이터베이스 내에 저장하여 성능 문제를 쉽게 모니터링하고 문제를 해결할 수 있습니다. 대시보드는 시간, 메모리 또는 CPU 리소스를 가장 많이 사용한 쿼리를 표시합니다.
- **Temporal 테이블**은 발생한 시간과 날짜와 함께 완료하여 모든 데이터 변경 내용을 기록하는 기록 테이블입니다.
- SQL Server의 새 기본 제공 **JSON 지원**은 가져오기, 내보내기, 구문 분석 및 저장을 지원합니다.
- 새 **PolyBase** 쿼리 엔진은 Hadoop 또는 Azure Blob Storage에 외부 데이터와 SQL Server를 통합합니다. 데이터를 가져오거나 내보낼 뿐 아니라 쿼리를 실행할 수 있습니다.
- 새 **Stretch Database** 기능을 사용하면 로컬 SQL Server 데이터베이스에서 클라우드의 Azure SQL Database까지, 데이터를 안전하고 동적으로 보관할 수 있습니다. SQL Server는 연결된 데이터베이스의 로컬 및 원격 데이터를 모두 자동으로 쿼리합니다. 
- **메모리 내 OLTP:** 
    - 이제 FOREIGN KEY, UNIQUE 및 CHECK 제약 조건, 네이티브 컴파일 저장 프로시저 OR, NOT, SELECT DISTINCT, OUTER JOIN 및 SELECT의 하위 쿼리를 지원합니다.
    - 최대 2TB 테이블을 지원합니다(256GB부터). 
    - 정렬 및 Always On 가용성 그룹 지원을 위한 향상된 열 저장 인덱스가 있습니다.
- 새 보안 기능:
    - **Always Encrypted:** 이 기능을 사용하면 암호화 키가 있는 응용 프로그램에서만 SQL Server 2016 데이터베이스의 암호화된 중요 데이터를 액세스할 수 있습니다. 이 키는 SQL Server에 전달되지 않습니다.
    - **동적 데이터 마스킹:** 테이블 정의에 지정된 경우, 마스킹된 데이터가 대부분의 사용자로부터 숨겨지고 UNMASK 권한이 있는 사용자만 완전한 데이터를 볼 수 있습니다.
    - **행 수준 보안:** 데이터 액세스를 데이터베이스 엔진 수준에서 제한할 수 있으므로 사용자가 관련된 항목만 것만 볼 수 있습니다. 

[데이터베이스 엔진](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)을 참조하세요.
## <a name="sql-server-2016-analysis-services-ssas"></a>SSAS(SQL Server 2016 Analysis Services)
SQL Server 2016 Analysis Services는 **1200 호환성 수준**을 기준으로 테이블 형식 모델 데이터베이스에 대한 향상된 성능, 제작, 데이터베이스 관리, 필터링, 프로세싱 및 그 외 많은 기능을 제공합니다.
- **[SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)** 는 통계 분석에 사용되는 R 프로그래밍 언어를 SQL Server에 통합합니다. 
- 새 **데이터베이스 일관성 검사기(DBCC)** 는 잠재적 데이터 손상 문제를 감지하기 위해 내부적으로 실행됩니다.
- **직접 쿼리**는 라이브 외부 데이터를 먼저 가져오는 대신 쿼리하며 이제 Azure SQL, Oracle 및 Teradata를 비롯한 더 많은 데이터 원본을 지원합니다. 
- 다양한 새 **DAX(Data Access Expressions) 기능**이 있습니다.
- 새 **[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)** 네임스페이스는 테이블 형식 모드 인스턴스 및 모델을 관리합니다. 
- [Analysis Services Management Objects(AMO)](http://msdn.microsoft.com/library/mt436122.aspx)가 두 번째 어셈블리인 **Microsoft.AnalysisServices.Core.dll**을 포함하도록 리팩터링되었습니다.

[Analysis Services 엔진(SSAS)](../analysis-services/what-s-new-in-analysis-services.md)을 참조하세요. 

## <a name="sql-server-2016-integration-services-ssis"></a>SQL Server 2016 Integration Services(SSIS)
- **Always On 가용성 그룹** 지원
- **증분 패키지 배포**
- **Always Encrypted** 지원
- 새 **ssis_logreader** 데이터베이스 수준 역할
- 새 **사용자 지정 로깅 수준**
- 데이터 흐름의 **오류에 대한 열 이름** 
- 새 **커넥터**
- **Hadoop 파일 시스템(HDFS)** 지원

[통합 서비스(SSIS)](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)를 참조하세요.

## <a name="sql-server-2016-master-data-services-mds"></a>SQL Server 2016 Master Data Services(MDS)
- 재귀 및 다대다 계층 구조에 대한 지원을 비롯한 **파생된 계층 구조 개선 사항**
- **도메인 기반 특성** 필터링
- 모델 간 엔터티 데이터를 공유하기 위한 **엔터티 동기화**
- **변경 집합**을 통한 승인 워크플로
- 쿼리 성능을 개선하는 **사용자 지정 인덱스**
- 향상된 보안을 위한 새 **권한 수준**
- 다시 디자인된 **비즈니스 규칙 관리** 환경

[MDS(Master Data Services)](../master-data-services/what-s-new-in-master-data-services-mds.md)를 참조하세요.

## <a name="sql-server-2016-reporting-services-ssrs"></a>SQL Server 2016 Reporting Services(SSRS)
Microsoft가 이 릴리스에서 Reporting Services를 완전히 개선했습니다. 
- KPI 기능이 있는 새 **웹 보고서 포털**
- 새 **모바일 보고서 게시자**
- HTML5를 지원하는 **다시 디자인된 보고서 렌더링 엔진** 
- 새 트리맵 및 선버스트 **차트 유형** 

[Reporting Services(SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계   
- [SQL Server 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)   
- [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md) 
- [SQL Server 2016 데이터시트](http://download.microsoft.com/download/C/5/3/C53C3AEF-653C-4598-8721-D522E8AC6A3A/SQL_Server_2016_Everything_Built-In_Datasheet_EN_US.pdf)
- [SQL Server 버전에서 지원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx)
- [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [설치 마법사에서 SQL Server 2016 설치](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [설치 및 서비스 설치](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
- [새 SQL PowerShell 모듈](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update/)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]