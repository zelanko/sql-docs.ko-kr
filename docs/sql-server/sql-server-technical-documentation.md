---
title: SQL Server 설명서 | Microsoft Docs
ms.date: 02/28/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: ''
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 8868bbce17a31e72d55cbdca3e7badb00e66666e
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="sql-server-documentation"></a>SQL Server 설명서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server는 Microsoft 데이터 플랫폼의 핵심 요소입니다. SQL Server는 ODBMS(운영 데이터베이스 관리 시스템)의 선두 주자입니다. 이 설명서를 통해 SQL Server를 설치하고, 구성하며, 사용할 수 있습니다. 콘텐츠는 종단 간 예제, 코드 샘플 및 비디오를 포함합니다. SQL Server 언어 항목은 [언어 참조](../t-sql/language-reference.md)를 참조하세요.

|새로운 기능  | 릴리스 정보  |
|---------|---------|
|[SQL Server 2017의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)     | [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)        |
|[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)     | [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)        |
|[SQL Server 2014의 새로운 기능](https://msdn.microsoft.com/library/bb500435(v=sql.120).aspx)     | [SQL Server 2014 Release Notes](../sql-server/sql-server-2014-release-notes.md)        |


**SQL Server를 사용해 보세요.**
> [![평가 센터에서 다운로드](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [SQL Server 다운로드](http://go.microsoft.com/fwlink/?LinkID=829477)
>
> [![평가 센터에서 다운로드](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)
>
> [![평가 센터에서 다운로드](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)
>
> [![가상 머신 만들기](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [SQL Server가 있는 가상 머신 가져오기](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)

## <a name="sql-server-technologies"></a>SQL Server 기술


|||
|-|-|    
|![SQL 데이터베이스 엔진](../sql-server/media/sql-database-engine.png "SQL 데이터베이스 엔진")|**[데이터베이스 엔진](../database-engine/sql-server-database-engine-overview.md)**<br /><br /> 데이터베이스 엔진은 데이터 저장, 처리 및 보안 유지를 위한 핵심 서비스입니다. 데이터베이스 엔진에서는 기업 내에서 가장 다루기 어려운 데이터 소비형 응용 프로그램의 요구 사항을 충족시키기 위해 액세스 제어 및 빠른 트랜잭션 처리를 제공합니다. 또한 데이터베이스 엔진은 고가용성을 유지하기 위한 다각적인 지원을 제공합니다.|
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 데이터 웨어하우징을 위해 추출, 변환 및 로드하는 ETL 패키지를 비롯하여 고성능 데이터 통합 솔루션을 작성하기 위한 플랫폼입니다.|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] 는 개인, 팀 및 기업의 비즈니스 인텔리전스를 위한 분석 데이터 플랫폼 및 도구 집합입니다. 서버 및 클라이언트 디자이너는 기존의 OLAP 솔루션, 새 테이블 형식 모델링 솔루션, 그리고 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], Excel 및 SharePoint Server 환경을 사용하는 셀프 서비스 분석과 공동 작업을 지원합니다. 또한[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에는 많은 양의 데이터 내에 숨겨진 패턴과 관계를 확인할 수 있도록 데이터 마이닝 기능이 포함되어 있습니다.|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services는 엔터프라이즈에 웹 사용이 가능한 보고 기능을 제공합니다.  다양한 데이터 원본에서 내용을 가져오고 다양한 형식으로 보고서를 게시하며 중앙에서 보안 및 구독을 관리하는 보고서를 만들 수 있습니다.|
|![R Server](../sql-server/media/r-server.png "R Server")|**[Machine Learning Services](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft Machine Learning Services는 인기 있는 R 및 Python 언어를 사용하여 엔터프라이즈 워크플로에 대한 기계 학습의 통합을 지원합니다.<br /><br /> Machine Learning Services(데이터베이스 내)는 R 및 Python을 SQL Server와 통합함으로써 저장 프로시저를 호출하여 모델을 쉽게 빌드 및 재교육하고 점수를 매길 수 있도록 합니다.  Microsoft Machine Learning Server는 SQL Server를 요구하지 않고 R 및 Python에 대한 엔터프라이즈 규모의 지원을 제공합니다.|
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server DQS(Data Quality Services)는 기술 자료 기반 데이터 정리 솔루션을 제공합니다. DQS를 사용하면 기술 자료를 작성한 다음 해당 기술 자료를 사용하여 컴퓨터 기반 및 대화형 방법을 통해 데이터에 대한 데이터 수정 및 중복 제거를 수행할 수 있습니다. 클라우드 기반 참조 데이터 서비스를 사용할 수 있으며, SQL Server Integration Services 및 Master Data Services와 DQS를 통합하는 데이터 관리 솔루션을 작성할 수 있습니다.|
|![Replication Services](../sql-server/media/replication-services.png "Replication Services")|**[복제](../relational-databases/replication/sql-server-replication.md)**<br /><br /> 복제는 한 데이터베이스에서 다른 데이터베이스로 데이터 및 데이터베이스 개체를 복사 및 배포한 다음 데이터베이스 간에 동기화를 수행하여 일관성을 유지하는 일련의 기술입니다. 복제를 사용하면 LAN 및 WAN, 전화 접속 연결, 무선 연결 및 인터넷을 통해 데이터를 여러 다른 위치로 배포하고 원격 또는 모바일 사용자에게 배포할 수 있습니다.|
|![Master  Data  Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 는 마스터 데이터 관리를 위한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 솔루션입니다. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 작성된 솔루션을 사용하면 정확한 정보를 기반으로 보고와 분석을 수행할 수 있습니다. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 사용하여 마스터 데이터에 대한 중앙 리포지토리를 만들고 시간 경과에 따라 변경되는 데이터의 감사 가능 및 보안 가능 레코드를 유지 관리합니다.|

## <a name="migrate-and-move-data"></a>데이터 마이그레이션 및 이동

- [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)
- [Microsoft Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)
- [SQL Server 데이터베이스를 Azure SQL Database로 마이그레이션](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

## <a name="earlier-sql-server-versions"></a>이전 버전의 SQL Server

- [SQL Server 업데이트 센터 - 지원되는 모든 버전에 대한 링크 및 정보](https://msdn.microsoft.com/library/ff803383.aspx)
- [SQL Server 2014 설명서](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [SQL Server 2012 설명서](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)
- [SQL Server 2008 R2 설명서](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)
- [SQL Server 2008 설명서](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx)
- [보관된 SQL Server 2005 설명서](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)

## <a name="samples"></a>샘플

- [Wide World Importers 예제 데이터베이스](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)
- [SQL Server 2016에 대한 AdventureWorks 예제 데이터베이스 및 스크립트](https://www.microsoft.com/download/details.aspx?id=49502) 
- [GitHub의 SQL Server 예제](https://github.com/Microsoft/sql-server-samples)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]