---
title: SSIS(SQL Server Integration Services) 설치 | Microsoft Docs
description: Microsoft SSIS(SQL Server Integration Services)를 설치하는 방법과 SSIS의 다른 다운로드를 가져오는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0478e345f388b3f4246bf33fdaba29a47a6ec0f6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74491960"
---
# <a name="install-integration-services-ssis"></a>Integration Services(SSIS) 설치

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 비롯한 구성 요소 중 일부 또는 전체를 설치하는 한 개의 설치 프로그램을 제공합니다. 설치 프로그램을 사용하여 한 개의 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소와 함께 설치하거나 단독으로 설치합니다.

 이 문서에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하기 전에 알아야 할 중요한 고려 사항에 대해 중점적으로 설명합니다. 이 문서의 정보를 통해 설치 옵션을 평가하여 성공적인 설치를 위한 항목을 선택할 수 있습니다.

![integration Services 설치](install-integration-services/install-integration-services-sql-setup.png)

## <a name="get-ready-to-install-integration-services"></a>Integration Services 설치 준비

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하기 전에 다음 정보를 검토합니다.

- [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

- [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)

## <a name="install-standalone-or-side-by-side"></a>독립 실행형 또는 나란히 설치

다음과 같은 구성으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 수 있습니다.

- 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 없는 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 수 있습니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기존 인스턴스와 함께 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 수 있습니다.

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이전 버전이 이미 설치되어 있는 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 최신 버전으로 업그레이드하면 현재 버전이 이전 버전과 함께 설치됩니다.

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 업그레이드에 대한 자세한 내용은 [Integration Services 업그레이드](../../integration-services/install-windows/upgrade-integration-services.md)를 참조하세요.

## <a name="get-sql-server-with-integration-services"></a>Integration Services를 사용하여 SQL Server 가져오기

Microsoft SQL Server가 아직 없는 경우 [SQL Server 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads)에서 평가판 버전 또는 무료 Developer 버전을 다운로드합니다. SSIS는 SQL Server Express Edition에 포함되지 않습니다.

## <a name="install-integration-services"></a>Integration Services 설치

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 설치 요구 사항을 검토한 결과 컴퓨터가 이러한 요구 사항을 만족하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 준비가 된 것입니다.

설치 마법사를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하는 경우 구성 요소와 옵션을 지정하는 일련의 페이지가 표시됩니다.

- **기능 선택** 페이지의 **공유 기능**에서 **Integration Services**를 선택합니다.

- **인스턴스 기능**에서, 필요에 따라 SSIS 카탈로그 데이터베이스를 호스팅하려면 **데이터베이스 엔진 서비스**를 선택하고, SSIS 패키지를 저장, 관리, 실행 및 모니터링하려면 `SSISDB`를 선택합니다.

- [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로그래밍에 대한 관리 어셈블리를 설치하려면 마찬가지로 **공유 기능** 아래에서 **클라이언트 도구 SDK**를 선택합니다.

> [!NOTE]
> 설치 마법사의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기능 선택**페이지에서 선택하여 설치할 수 있는 일부** 구성 요소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소의 일부분만 설치합니다. 이러한 구성 요소는 특정 태스크에 유용하지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 기능은 제한됩니다. 예를 들어 **데이터베이스 엔진 서비스** 옵션을 선택하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가져오기 및 내보내기 마법사에 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 설치됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 전체 설치하려면 **기능 선택** 페이지에서 **Integration Services** 를 선택해야 합니다.

### <a name="installing-a-dedicated-server-for-etl-processes"></a>ETL 프로세스용 전용 서버 설치

ETL(추출, 변환 및 로드) 프로세스에 전용 서버를 사용하려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]를 설치할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 로컬 인스턴스를 설치합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 일반적으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 패키지를 저장하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 패키지를 예약합니다. ETL 서버에 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 없는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 있는 서버에서 패키지를 예약 또는 실행해야 합니다. 결과적으로 패키지가 ETL 서버에서 실행되지 않고 해당 패키지가 시작된 서버에서 실행됩니다. 따라서 전용 ETL 서버의 리소스는 의도대로 사용되지 않습니다. 또한 다른 서버의 리소스가 실행 중인 ETL 프로세스에 의해 소모될 수 있습니다.

### <a name="configuring-ssis-event-logging"></a>SSIS 이벤트 로깅 구성

기본적으로 새로 설치하는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 실행과 관련된 이벤트를 애플리케이션 이벤트 로그에 기록하지 않도록 구성됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터 수집기 기능을 사용하는 경우 이 설정은 이벤트 로그 항목이 너무 많이 생성되지 않도록 방지합니다. 기록되지 않는 이벤트는 EventID 12288, "패키지가 시작되었습니다" 및 EventID 12289, "패키지가 성공적으로 완료되었습니다"입니다. 이러한 이벤트를 애플리케이션 이벤트 로그에 기록하려면 편집을 위해 레지스트리를 엽니다. 그런 다음 레지스트리에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS 노드를 찾고 LogPackageExecutionToEventLog 설정의 DWORD 값을 0에서 1로 변경합니다.

## <a name="install-additional-components-for-integration-services"></a>Integration Services의 추가 구성 요소 설치

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]을 새로 설치하려면 다음 목록에서 필요한 구성 요소를 선택합니다.

- **Integration Services(SSIS)** . SQL Server 설치 마법사를 사용하여 SSIS를 설치합니다. SSIS를 선택하면 다음 항목이 설치됩니다.

  - SQL Server 데이터베이스 엔진에서 SSIS 카탈로그 지원.

  - 필요에 따라, 마스터와 작업자로 구성되는 [Scale Out 기능](../scale-out/walkthrough-set-up-integration-services-scale-out.md).

  - 32비트 및 64비트 SSIS 구성 요소.

  - SSIS를 설치해도 SSIS 패키지를 설계 및 개발하는 데 필요한 도구는 설치되지 **않습니다**.

- **SQL Server 데이터베이스 엔진**. SQL Server 설치 마법사를 사용하여 데이터베이스 엔진을 설치합니다. 데이터베이스 엔진을 선택하면 SSIS 패키지를 저장, 관리, 실행 및 모니터링하는 SSIS 카탈로그 데이터베이스 `SSISDB`를 만들고 호스팅할 수 있습니다.

- **SQL Server Data Tools(SSDT)** . SSDT를 다운로드하여 설치하려면 [SSDT(SQL Server Data Tools) 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요. SSDT를 설치하면 SSIS 패키지를 설계 및 배포할 수 있습니다. SSDT는 다음 항목을 설치합니다.

  - SSIS 디자이너를 포함한 SSIS 패키지 디자인 및 개발 도구.

  - 32비트 SSIS 구성 요소만.

  - 제한된 버전의 Visual Studio(Visual Studio 버전이 아직 설치되지 않은 경우).

  - SSIS 스크립트 태스크 및 스크립트 구성 요소에서 사용하는 스크립트 편집기인 VSTA(Visual Studio Tools for Applications).

  - 배포 마법사 및 패키지 업그레이드 마법사를 포함한 SSIS 마법사.

  - SQL Server 가져오기 및 내보내기 마법사.

- **SQL Server Data Tools(SSDT)** . Visual Studio 2019에 대한 SSDT 독립 실행형 설치 프로그램이 중단되었습니다. 이제 Visual Studio 2019의 경우 [VS 마켓플레이스](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects&ssr=false#overview)에서 SSIS 디자이너 확장을 가져올 수 있습니다.

- **Azure용 integration Services 기능 팩**. 기능 팩을 다운로드하여 설치하려면 [Azure용 Microsoft SQL Server 2017 Integration Services 기능 팩](https://docs.microsoft.com/sql/integration-services/azure-feature-pack-for-integration-services-ssis?view=sql-server-2017)을 참조하세요. 기능 팩을 설치하면 패키지에서 다음 서비스를 포함한 Azure 클라우드의 스토리지 및 분석 서비스에 연결할 수 있습니다.

  - Azure Blob Storage.

  - Azure HDInsight.

  - Azure Data Lake Store.

  - Azure SQL Data Warehouse.

  - Azure Data Lake Storage(Gen2).

- **선택적 추가 구성 요소**. 필요에 따라 SQL Server 기능 패키지에서 추가 타사 구성 요소를 다운로드할 수 있습니다.

  - Microsoft® Connector for SAP BW for Microsoft SQL Server®. 이러한 구성 요소를 얻는 방법은 [Microsoft® SQL Server® 2017 기능 팩](https://www.microsoft.com/download/details.aspx?id=55992)을 참조하세요.

  - Microsoft Connector Version 5.0 for Oracle by Attunity 및 Microsoft Connector Version 5.0 for Teradata by Attunity. 이러한 구성 요소를 얻는 방법은 [Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [여러 Integration Services 버전을 병렬로 설치](installing-integration-services-versions-side-by-side.md)

- [SQL Server 2016 Integration Services의 새로운 기능](../what-s-new-in-integration-services-in-sql-server-2016.md)

- [SQL Server 2017 Integration Services의 새로운 기능](../what-s-new-in-integration-services-in-sql-server-2017.md)
