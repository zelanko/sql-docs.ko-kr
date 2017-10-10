---
title: "SQL Server Integration Services 작업에서 클라우드로 이동할 | Microsoft Docs"
ms.date: 10/09/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 85ab11747276f0c6c58b13cd409df3e5774915ae
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>SQL Server Integration Services 작업에서 클라우드로 이동할
Azure 클라우드로 SQL Server Integration Services (SSIS) 패키지 및 워크 로드를 이동할 수 있습니다.
-   저장 하 고 SSIS 프로젝트 및 SSIS 카탈로그 데이터베이스 (SSISDB) Azure SQL 데이터베이스에 패키지를 관리 합니다.
-   Azure 데이터 팩터리 버전 2의 일부로 도입 Azure SSIS 통합 런타임 인스턴스에 패키지를 실행 합니다.
-   이러한 일반적인 작업에 대 한 SQL Server Management Studio (SSMS)와 같은 친숙 한 도구를 사용 합니다.

## <a name="benefits"></a>이점
Azure로 온-프레미스 SSIS 작업을 이동 하는 것과 다음과 같은 이점이:
-   **운영 비용 절감** 온-프레미스 인프라를 줄여 합니다.
-   **높은 가용성을 높여 주는** azure 및 Azure SQL 데이터베이스의 고가용성 기능 뿐만 아니라 클러스터 당 여러 노드.
-   **확장성을 높이기** (스케일 업) 노드당 여러 코어 및 클러스터 (수평 확장) 당 여러 노드를 지정 하는 기능입니다.
-   **제한 사항을 피하려면** Azure 가상 컴퓨터에서 SSIS를 실행 합니다.

## <a name="architecture-overview"></a>아키텍처 개요
다음 표에서 SSIS 온-프레미스와 Azure에서 SSIS 간의 차이 강조 표시합니다. 가장 중요 한 차이점은 계산에서 저장소를 분리 합니다.

| 저장소 | 런타임 | 확장성 |
|---|---|---|
| 온-프레미스 (SQL Server) | SQL Server에서 호스트 하는 SSIS 런타임 | SSIS 스케일 아웃 (SQL Server 2017에 이상)<br/><br/>(이전 버전의 SQL Server)에서 사용자 지정 솔루션 |
| Azure (SQL 데이터베이스)에서 | Azure SSIS 통합 런타임, Azure 데이터 팩터리 버전 2의 구성 요소 | SSIS IR에 대 한 크기 조정 옵션 |
| | | |

Azure 데이터 팩터리에 Azure에 있는 SSIS 패키지의 런타임 엔진을 호스팅합니다. 런타임 엔진은 Azure SSIS 통합 런타임 (SSIS IR) 라고 합니다.

SSIS IR의 프로 비전 할 때을 확장 하 고 다음 옵션에 대 한 값을 지정 하 여 쉽게 확장할 수 있습니다.
-   노드 크기 (코어 수 포함) 및 클러스터의 노드 수입니다.
-   SSIS 카탈로그 데이터베이스 (SSISDB) 및 서비스 계층 데이터베이스를 호스팅하는 Azure SQL 데이터베이스의 기존 인스턴스.
-   노드당 최대 병렬 실행 합니다.

한 번 SSIS IR를 프로 비전 하기만 하면 됩니다. 그 후에 배포 하려면 SQL Server Data Tools (SSDT) 및 SQL Server Management Studio (SSMS)를 구성, 실행, 모니터링, 예약 및 관리 패키지와 같은 친숙 한 도구를 사용할 수 있습니다.

> [!NOTE]
> 이 공개 미리 보기 동안 Azure SSIS 통합 런타임에서 에서만 사용 가능 동부 미국과 유럽 북부 지역에 있습니다.

데이터 팩터리는 다른 유형의 통합 런타임도 지원합니다. SSIS IR 및 다른 유형의 통합 런타임에 대 한 자세한 참조 [Azure Data Factory에 통합 런타임에서](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime)합니다.

## <a name="prerequisites"></a>필수 구성 요소
이 항목에서 설명 하는 기능 SQL Server 데이터 도구 (SSDT) 버전 17.2 이상 필요 하지만 SQL Server 2017 또는 SQL Server 2016 필요 하지 않습니다. Azure에 패키지를 배포할 때 패키지 배포 마법사는 패키지를 최신 패키지 형식으로 항상 업그레이드 합니다.

Azure에서 필수 구성 요소에 대 한 자세한 내용은 참조 하십시오. [Azure에 SQL Server Integration Services (SSIS) 패키지 리프트 하 고 shift](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)합니다.

## <a name="ssis-features-on-azure"></a>Azure에서 SSIS 기능

SSISDB를 호스트 하기 위해 SQL 데이터베이스의 인스턴스를 프로 비전 하는 경우 SSIS 및 액세스 재배포 가능 패키지에 대 한 Azure 기능 팩이 설치 됩니다. 이러한 구성 요소는 Excel 및 Access 파일 및 다양 한 Azure 데이터 원본 연결을 제공합니다. 이 이번에 SSIS에 대 한 타사 구성 요소를 설치할 수 없습니다.

SSISDB를 호스팅하는 SQL 데이터베이스의 이름은 됩니다 배포 SSDT 및 SSMS-에서 패키지를 관리 하는 경우 사용 하는 네 부분으로 된 이름에서 첫 번째 부분의 `<sql_database_name>.database.windows.net`합니다.

Azure SQL 데이터베이스에는 SSISDB에 배포한 프로젝트에 대 한 프로젝트 배포 모델로 패키지 배포 모델이 아닌를 사용 해야 합니다.

디자인 하 고 패키지 온-프레미스에서 SSDT 또는 Visual Studio에서 SSDT 설치로 구축 계속 있습니다.

Windows 인증을 사용 하 여 클라우드에서 온-프레미스 데이터 원본에 연결 하는 방법에 대 한 정보를 참조 하십시오. [Windows 인증을 사용 하 여 온-프레미스 데이터 원본에 연결](ssis-azure-connect-with-windows-auth.md)합니다.

## <a name="common-tasks"></a>일반 작업

### <a name="provision"></a>프로비전
배포 하 고 Azure에서 SSIS 패키지를 실행할 수 있습니다, 전에 SSISDB 카탈로그 데이터베이스와 Azure SSIS 통합 런타임에서 프로 비전 해야 합니다. 이 문서의 단계 프로 비전이 수행: [Azure에 SQL Server Integration Services (SSIS) 패키지 리프트 하 고 shift](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)합니다.

### <a name="deploy-and-run-packages"></a>배포 및 패키지 실행
프로젝트를 배포 하 고 SQL 데이터베이스에서 패키지를 실행 하려면 여러 친숙 한 도구 및 스크립팅 옵션 중 하나를 사용할 수 있습니다.
-   SSMS(SQL Server Management Studio)
-   (SSMS, Visual Studio Code 또는 다른 도구)에서 transact SQL
-   명령줄 도구
-   PowerShell
-   C# 및 SSIS 관리 개체 모델

### <a name="monitor-packages"></a>모니터 패키지
SSMS에서 실행 중인 패키지를 모니터링 하려면 SSMS에서 다음 도구 중 하나로 사용할 수 있습니다.
-   마우스 오른쪽 단추로 클릭 **SSISDB**를 선택한 후 **활성 작업** 열려는 **활성 작업** 대화 상자.
-   개체 탐색기, 마우스 오른쪽 단추 클릭 및 선택에서 패키지를 선택 합니다. **보고서**, 다음 **표준 보고서**, 다음 **모든 실행**합니다.

### <a name="schedule-packages"></a>일정 패키지
SQL 데이터베이스에 저장 된 패키지의 실행을 예약 하려면 다음 도구를 사용할 수 있습니다.
-   SQL Server 에이전트 온-프레미스
-   데이터 팩터리 SQL Server 저장 프로시저 작업

자세한 내용은 참조 하십시오. [일정 SSIS 패키지를 Azure에서 실행](ssis-azure-schedule-packages.md)합니다.

## <a name="next-steps"></a>다음 단계
Azure에서 SSIS 작업을 시작 하려면 다음 문서를 참조 합니다.
-   [SQL Server Integration Services (SSIS) 패키지를 Azure로 이동할](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [배포, 실행 및 Azure에서 SSIS 패키지를 모니터링 합니다.](ssis-azure-deploy-run-monitor-tutorial.md)

