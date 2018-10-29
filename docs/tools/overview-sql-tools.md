---
title: SQL 도구 및 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse에 대 한 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 359144187de1b1a780ba3d866f4a4881c2444442
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643941"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL 도구 및 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse에 대 한 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

(쿼리, 모니터 등)를 관리 하려면 데이터베이스 도구가 필요 합니다. 데이터베이스는 Windows, 또는 클라우드에서 실행 될 수 있습니다 하는 동안 [Linux](../linux/sql-server-linux-overview.md), 도구는 데이터베이스와 동일한 플랫폼에서 실행할 필요가 없습니다. 

많은 도구가 있습니다 데이터베이스를 사용할 수 있도록이 문서에서는 SQL database를 사용 하 여 작업에 대 한 설명 및 사용 가능한 도구 중 일부에 대 한 포인터를 제공 합니다. 어떤 도구를 결정 합니다. 도움이 필요한 경우에 표시 [어떤 도구 사용 해야 합니까?](#which-tool-should-i-choose)합니다.


## <a name="gui-tools-to-manage-databases"></a>데이터베이스를 관리 하는 GUI 도구  

다음은 기본 그래픽 사용자 인터페이스 (GUI) 도구입니다.

| 도구 | 설명 | 실행 |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] 실행 중인 경우 항상 데이터베이스 관리를 위한 무료, 경량 도구입니다. 이 미리 보기 릴리스에서 확장 된 TRANSACT-SQL 편집기 및 데이터베이스의 작동 상태에 대 한 사용자 지정이 가능한 정보를 포함 하 여 데이터베이스 관리 기능을 제공 합니다. | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows, macOS 및 Linux에서 실행**합니다.|
| [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | SQL Server Management Studio (SSMS)를 사용 하 여 쿼리를 디자인 하 고 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse 관리. | **SSMS는 Windows에서 실행됩니다.**|
| [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse 용 강력한 개발 환경에 Visual Studio를 설정 합니다.| **Windows에서 실행 되는 SSDT**합니다.|
| [Visual Studio Code](https://code.visualstudio.com/)| Visual Studio Code를 설치한 후 설치 합니다 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) Microsoft SQL Server, Azure SQL Database 및 SQL Data Warehouse 개발을 위한 합니다.| **Windows, macOS 및 Linux에서 실행 되는 visual Studio Code**합니다.|


## <a name="command-line-tools-to-manage-databases"></a>데이터베이스를 관리 하기 위한 명령줄 도구

다음은 주요 명령줄 도구입니다.

| 도구 | 설명 | 실행 |
|:--|:--|:--|
|[**mssql-cli(미리 보기)**](mssql-cli.md)|**mssql cli** 는 SQL Server 쿼리는 대화형 명령줄 도구가 있습니다. | Windows, macOS 및 Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage** 는 여러 데이터베이스 개발 태스크를 자동화 하는 명령줄 유틸리티입니다. macOS 및 Linux 버전의 sqlpackage는 현재 미리 보기. | Windows, macOS 및 Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** SQL을 사용 하 여 작업에 대 한 cmdlet을 제공 합니다.| Windows, macOS 및 Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd** 유틸리티를 사용 하면 TRANSACT-SQL 문, 시스템 프로시저 및 명령 프롬프트에서 스크립트 파일을 입력 합니다. | Windows, macOS 및 Linux|
|[**bcp**](../2014/tools/bcp-utility.md)|**대**량 **복**사 **프**로그램 유틸리티(**bcp**)는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 대량 복사합니다.|Windows, macOS 및 Linux|
|[**mssql-scripter (미리 보기)**](https://github.com/Microsoft/mssql-scripter)|**mssql scripter** 은 SQL Server 데이터베이스를 스크립팅 하는 것에 대 한 다중 플랫폼 명령줄 환경|Windows, macOS 및 Linux|
|[**mssql conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**mssql conf** Linux에서 실행 중인 SQL Server를 구성 합니다.|Linux|



## <a name="which-tool-should-i-choose"></a>어떤 도구를 선택 해야 하나요?

- SQL Server 인스턴스 또는 데이터베이스에서 Windows, Linux 또는 Mac에는 가벼운 편집기에서 관리 하 시겠습니까? [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) 선택
- SQL Server 인스턴스 또는 전체 GUI 지원을 통해 Windows에서 데이터베이스를 관리 하 시겠습니까? [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) 선택
- 수행 하거나 데이터베이스 코드를 컴파일 시간 유효성 검사를 포함 하 여 유지 관리 하려면, 리팩터링 및 디자이너를 Windows에서 지원? [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) 선택
- IntelliSense, 구문 높은 조명 기능 하는 명령줄 도구를 사용 하 여 SQL Server를 쿼리 하려는 경우 등? 선택 [mssql-cli](mssql-cli.md)
- Windows, Linux 또는 Mac에서 가벼운 편집기에서 T-SQL 스크립트를 작성 하 시겠습니까? 선택할 [Visual Studio Code](https://code.visualstudio.com/) 고 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>추가 도구

| 도구 | 설명 |
|:--|:--|
| [구성 관리자](../tools/configuration-manager/sql-server-configuration-manager-help.md) | SQL Server 구성 관리자 SQL Server 서비스를 구성 하 고 네트워크 연결을 구성 하려면 사용 하 고 있습니다. Windows에서 실행 되는 configuration Manager|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | SQL Server Migration Assistant를 사용하여 Microsoft Access, DB2, MySQL, Oracle 및 Sybase에서 SQL Server로 데이터베이스를 마이그레이션하는 작업을 자동화할 수 있습니다.|
| [데이터베이스 실험 도우미](../dea/database-experimentation-assistant-overview.md) | 지정된 된 워크 로드에 대 한 대상된 버전의 SQL 평가 하려면 데이터베이스 실험 도우미를 사용 합니다. |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Distributed Replay 기능을 사용 하 여 향후 SQL Server 업그레이드의 영향을 평가할 수 있도록 합니다. 하드웨어 및 운영 체제 업그레이드 및 SQL Server 튜닝의 영향을 평가 하는 데 Distributed Replay를 사용할 수도 있습니다. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 유틸리티는 Service Broker 서비스 구성 이나 Service Broker 대화의 문제를 보고 합니다. |

이 페이지에 나와 있지 않은 추가 도구를 찾고 볼 [SQL 명령 프롬프트 유틸리티](command-prompt-utility-reference-database-engine.md)합니다.

