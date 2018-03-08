---
title: "SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트 | Microsoft Docs"
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96384f918239772c3c6a859f523c04a4d53ec4d0
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트
이제 SSIS(SQL Server Integration Services) 패키지 및 워크로드를 Azure 클라우드로 이동할 수 있습니다.
-   Azure SQL Database의 SSISDB(SSIS 카탈로그 데이터베이스)에서 SSIS 프로젝트와 패키지를 저장 및 관리합니다.
-   Azure Data Factory 버전 2의 일부로 도입된 Azure SSIS Integration Runtime의 인스턴스에서 패키지를 실행합니다.
-   이러한 일반적인 작업에는 SSMS(SQL Server Management Studio)와 같은 친숙한 도구를 사용합니다.

## <a name="benefits"></a>이점
온-프레미스 SSIS 워크로드를 Azure로 이동하면 다음과 같은 잠재적 이점이 있습니다.
-   SSIS를 온-프레미스 또는 Azure 가상 머신에서 실행할 때 **운영 비용을 절감**하고 인프라를 관리하는 부담을 줄입니다.
-   Azure 및 Azure SQL Database의 고가용성 기능뿐만 아니라 클러스터당 여러 노드를 지정할 수 있는 기능도 있으므로 **고가용성을 높입니다**.
-   노드당 다중 코어(강화) 및 클러스터당 다중 노드(규모 확장)를 지정하는 기능으로 **확장성을 높입니다**.

## <a name="architecture-overview"></a>아키텍처 개요
다음 표에서는 온-프레미스 SSIS와 Azure SSIS의 차이점을 보여 줍니다. 가장 중요한 차이점은 저장소와 계산의 분리입니다.

| 저장소 | 런타임 | 확장성 |
|---|---|---|
| 온-프레미스(SQL Server) | SQL Server에서 호스팅하는 SSIS 런타임 | SSIS Scale Out(SQL Server 2017 이상)<br/><br/>사용자 지정 솔루션(이전 버전의 SQL Server) |
| Azure(SQL Database) | Azure SSIS Integration Runtime(Azure Data Factory 버전 2의 구성 요소) | SSIS IR 크기 조정 옵션 |
| | | |

Azure Data Factory는 Azure에서 SSIS 패키지의 런타임 엔진을 호스팅합니다. 런타임 엔진은 Azure SSIS IR(SSIS Integration Runtime)이라고 합니다.

SSIS IR을 프로비전할 때 다음 옵션에 대한 값을 지정하여 강화하거나 규모 확장할 수 있습니다.
-   노드 크기(코어 수 포함) 및 클러스터의 노드 수
-   SSISDB(SSIS 카탈로그 데이터베이스)를 호스팅하는 Azure SQL Database의 기존 인스턴스 및 데이터베이스의 서비스 계층
-   노드당 최대 병렬 실행 수

SSIS IR은 한 번만 프로비전하면 됩니다. 그런 다음 SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)와 같은 친숙한 도구를 사용하여 패키지를 배포, 구성, 실행, 모니터링, 예약 및 관리할 수 있습니다.

> [!NOTE]
> 이 공개 미리 보기 동안 Azure SSIS Integration Runtime은 아직 모든 지역에서 사용할 수 없습니다. 지원되는 지역에 대한 정보는 [지역별 사용 가능한 제품 - Microsoft Azure](https://azure.microsoft.com/regions/services/)를 참조하세요.

또한 Data Factory는 다른 유형의 통합 런타임도 지원합니다. SSIS IR 및 다른 유형의 통합 런타임에 대한 자세한 내용은 [Azure Data Factory의 통합 런타임](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항
이 아티클에서 설명하는 기능에는 SQL Server 2017 또는 SQL Server 2016이 필요하지 않습니다.

이러한 기능을 사용하려면 다음 버전의 SSDT(SQL Server Data Tools)가 필요합니다.
-   Visual Studio 2017용, 버전 15.3(미리 보기) 이상
-   Visual Studio 2015용, 버전 17.2 이상

> [!NOTE]
> Azure에 패키지를 배포하는 경우 패키지 배포 마법사는 항상 패키지를 최신 패키지 형식으로 업그레이드합니다.

Azure에서 필수 구성 요소에 대한 자세한 정보는 [Azure에 SSIS 패키지 배포](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)를 참조하세요.

## <a name="ssis-features-on-azure"></a>Azure의 SSIS 기능

SQL Database 인스턴스를 프로비전하여 SSISDB를 호스팅하면 SSIS용 Azure Feature Pack 및 Access 재배포 가능 패키지도 설치됩니다. 이러한 구성 요소는 기본 제공 구성 요소에서 지원하는 데이터 원본 외에도 **Excel 및 Access** 파일 및 다양한 **Azure** 데이터 원본에 대한 연결을 제공합니다. 이때 SSIS용 **타사 구성 요소**(Attunity 및 SAP BI 구성 요소에 의한 Oracle 및 Teradata 구성 요소와 같은 Microsoft의 타사 구성 요소 포함)는 설치할 수 없습니다.

SSISDB를 호스팅하는 **SQL Database의 이름**은 SSDT 및 SSMS에서 패키지를 배포하고 관리할 때 사용할 네 부분으로 된 이름(`<sql_database_name>.database.windows.net`)의 첫 부분입니다.

Azure SQL Database에서 SSISDB에 배포하는 프로젝트의 경우 패키지 배포 모델이 아닌 **프로젝트 배포 모델**을 사용해야 합니다.

SSDT가 설치된 Visual Studio 또는 SSDT에서 온-프레미스 **패키지를 설계하고 빌드**합니다.

Windows 인증을 사용하여 클라우드에서 **온-프레미스 데이터 원본**에 연결하는 방법에 대한 자세한 내용은 [Windows 인증을 사용하여 온-프레미스 데이터 원본에 연결](ssis-azure-connect-with-windows-auth.md)을 참조하세요.

## <a name="common-tasks"></a>일반 작업

### <a name="provision"></a>프로비전
Azure에서 SSIS 패키지를 배포하고 실행하려면 먼저 SSISDB 카탈로그 데이터베이스와 Azure SSIS Integration Runtime을 프로비전해야 합니다. [Azure에 SSIS 패키지 배포](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal) 아티클의 프로비전 단계를 수행합니다.

### <a name="deploy-and-run-packages"></a>패키지 배포 및 실행
SQL Database에서 프로젝트를 배포하고 패키지를 실행하려면 다음과 같은 몇 가지 친숙한 도구 및 스크립팅 옵션 중 하나를 사용할 수 있습니다.
-   SSMS(SQL Server Management Studio)
-   Transact-SQL(SSMS, Visual Studio Code 또는 다른 도구에서 제공)
-   명령줄 도구
-   PowerShell
-   C# 및 SSIS 관리 개체 모델

### <a name="monitor-packages"></a>패키지 모니터링
SSMS에서 실행 중인 패키지를 모니터링하려면 SSMS에서 다음 보고 도구 중 하나를 사용할 수 있습니다.
-   **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **활성 작업**을 선택하여 **활성 작업** 대화 상자를 엽니다.
-   [개체 탐색기]에서 패키지를 선택하여 마우스 오른쪽 단추로 클릭하고, **보고서**, **표준 보고서**, **모든 실행**을 차례로 선택합니다.

### <a name="schedule-packages"></a>패키지 예약
SQL Database에 저장된 패키지의 실행을 예약하려면 다음 도구를 사용할 수 있습니다.
-   온-프레미스 SQL Server 에이전트
-   Data Factory SQL Server 저장 프로시저 작업

자세한 내용은 [Azure에서 SSIS 패키지 실행 예약](ssis-azure-schedule-packages.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
Azure에서 SSIS 워크로드를 시작하려면 다음 문서를 참조하세요.
-   [Azure에 SSIS 패키지 배포](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)
-   [Azure에서 SSIS 패키지 배포, 실행 및 모니터링](ssis-azure-deploy-run-monitor-tutorial.md)
