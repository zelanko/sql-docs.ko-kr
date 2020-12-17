---
title: SQL 도구 개요
description: SQL Server, Azure SQL(Azure SQL 데이터베이스, Azure SQL 관리형 인스턴스, SQL 가상 머신), Azure Synapse Analytics용 SQL 쿼리 및 관리 도구입니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 02/04/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017'
ms.openlocfilehash: df6a1e45a31bffd87ea7db06e0569162f7896fc0
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559305"
---
# <a name="sql-tools-overview"></a>SQL 도구 개요

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

데이터베이스를 관리하려면 도구가 필요합니다. 데이터베이스가 클라우드, Windows, macOS 또는 [Linux](../linux/sql-server-linux-overview.md)에서 실행되는지 관계없이 도구는 데이터베이스와 동일한 플랫폼에서 실행할 필요가 없습니다.

다음 표에서 다양한 SQL 도구에 대한 링크를 볼 수 있습니다.

> [!Note]
> SQL Server를 다운로드하려면 [SQL Server 설치](../database-engine/install-windows/install-sql-server.md)를 참조하세요.

## <a name="recommended-tools"></a>권장 도구

다음 도구는 GUI(그래픽 사용자 인터페이스)를 제공합니다.

| 도구 | Description | 운영 체제 |
|:--|:--|:--|
| [ **![ADS 이미지](../tools/media/overview-sql-tools/azure-data-studio.svg)</br></br>Azure Data Studio**](../azure-data-studio/download.md) | 주문형 SQL 쿼리를 실행하고 텍스트, JSON 또는 Excel로 결과를 보고 저장할 수 있는 경량 편집기입니다. 데이터를 편집하고, 즐겨 사용하는 데이터베이스 연결을 구성하며, 익숙한 개체 검색 환경에서 데이터베이스 개체를 찾습니다. | **Windows</br>macOS</br>Linux** |
| [ **![SSMS 이미지](../tools/media/overview-sql-tools/ssms.svg)</br></br>SQL Server Management Studio(SSMS)**](../ssms/download-sql-server-management-studio-ssms.md) | 완벽한 GUI 지원으로 SQL Server 인스턴스 또는 데이터베이스를 관리합니다. SQL Server, Azure SQL Database, Azure Synapse Analytics의 모든 구성 요소에 액세스하고 구성, 관리, 개발합니다. 다양한 기술 수준의 개발자와 데이터베이스 관리자가 SQL에 액세스할 수 있도록 여러 서식 있는 스크립트 편집기와 광범위한 그래픽 도구 그룹을 결합하는 포괄적인 단일 유틸리티를 제공합니다. | **Windows** |
| [ **![SSDT 이미지](../tools/media/overview-sql-tools/ssdt.svg)</br>SQL Server Data Tools(SSDT)**](../ssdt/download-sql-server-data-tools-ssdt.md) | SQL Server 관계형 데이터베이스, Azure SQL 데이터베이스, AS(Analysis Services) 데이터 모델, IS(Integration Services) 패키지 및 RS(Reporting Services) 보고서를 빌드하기 위한 최신형 개발 도구입니다. SSDT를 사용하면 **[Visual Studio](https://visualstudio.microsoft.com/downloads/)** 에서 애플리케이션을 개발할 때처럼 쉽게 SQL Server 콘텐츠 형식을 디자인 및 배포할 수 있습니다. | **Windows** |
| [ **![VS Code 이미지](../tools/media/overview-sql-tools/visual-studio-code.svg)</br></br>Visual Studio Code**](https://code.visualstudio.com/) | Visual Studio Code용 **[mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)** 은 Visual Studio Code에서 SQL Server 연결과 T-SQL에 대한 풍부한 편집 환경을 지원하는 공식 SQL Server 확장 프로그램입니다. 경량 편집기에서 T-SQL 스크립트를 작성합니다. | **Windows</br>macOS</br>Linux** |

## <a name="command-line-tools"></a>명령줄 도구

아래 도구는 주요 명령줄 도구입니다.

| 도구 | Description | 운영 체제 |
|:--|:--|:--|
|[**bcp**](bcp-utility.md)|대량 복사 프로그램 유틸리티(**b** ulk **c** opy **p** rogram utility, **bcp**)는 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 대량 복사합니다.| **Windows</br>macOS</br>Linux** |
|[**mssql-cli(미리 보기)**](mssql-cli.md)|**mssql-cli** 는 SQL Server를 쿼리하는 대화형 명령줄 도구입니다. IntelliSense, 구문 강조 표시 등을 제공하는 명령줄 도구를 사용하여 SQL Server를 쿼리합니다. | **Windows</br>macOS</br>Linux** |
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md) | **mssql-conf** 는 Linux에서 실행되는 SQL Server를 구성합니다. | **Linux** |
|[**mssql-scripter(미리 보기)**](https://github.com/Microsoft/mssql-scripter) | **mssql-scripter** 는 SQL Server 데이터베이스를 스크립팅하기 위한 다중 플랫폼 명령줄 환경입니다. | **Windows</br>macOS</br>Linux** |
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd** 유틸리티를 사용하여 명령 프롬프트에서 Transact-SQL 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다. | **Windows</br>macOS</br>Linux** |
| [**sqlpackage**](sqlpackage/sqlpackage.md) |**sqlpackage** 는 다음 데이터베이스 개발 작업을 자동화하는 명령줄 유틸리티입니다. |**Windows</br>macOS</br>Linux** |
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** 은 SQL을 사용하기 위한 cmdlet을 제공합니다. | **Windows</br>macOS</br>Linux** |

## <a name="migration-and-other-tools"></a>마이그레이션 및 기타 도구

이러한 도구는 SQL 데이터베이스를 마이그레이션하고, 구성하고, 기타 기능을 제공하는 데 사용됩니다.

| 도구 | Description |
|:--|:--|
| **[구성 관리자](../tools/configuration-manager/sql-server-configuration-manager-help.md)** | SQL Server 구성 관리자를 사용하여 SQL Server 서비스를 구성하고 네트워크 연결을 구성할 수 있습니다. Windows에서 실행되는 구성 관리자|
| **[데이터베이스 실험 도우미](../dea/database-experimentation-assistant-overview.md)** | 데이터베이스 실험 도우미를 사용하여 지정된 작업에 대한 대상 SQL 버전을 평가할 수 있습니다. |
| **[Data Migration Assistant](../dma/dma-overview.md)** | Data Migration Assistant 도구를 사용하면 새 버전의 SQL Server 또는 Azure SQL Database의 데이터베이스 기능에 영향을 줄 수 있는 호환성 문제를 검색하여 최신 데이터 플랫폼으로 업그레이드할 수 있습니다. |
| **[Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md)** | Distributed Replay 기능을 사용하여 향후 SQL Server 업그레이드의 영향을 쉽게 평가할 수 있습니다. 또한 Distributed Replay를 사용하여 하드웨어 및 운영 체제 업그레이드의 영향을 평가하고 SQL Server를 튜닝할 수 있습니다. |
| **[ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)** | ssbdiagnose 유틸리티는 Service Broker 대화 또는 Service Broker 서비스 구성의 문제를 보고합니다. |
| **[SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md)** | SQL Server Migration Assistant를 사용하여 Microsoft Access, DB2, MySQL, Oracle 및 Sybase에서 SQL Server로 데이터베이스를 마이그레이션하는 작업을 자동화할 수 있습니다.|

이 페이지에 설명되지 않은 추가 도구를 찾고 있는 경우 [SQL 명령 프롬프트 유틸리티](command-prompt-utility-reference-database-engine.md) 및 [SQL Server 확장 기능 및 도구 다운로드](download-sql-feature-packs.md)를 참조하세요.
