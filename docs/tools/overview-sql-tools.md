---
title: SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse에 대 한 SQL 도구 및 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe249e4df9c33fcbb292fc93f218e16ae111b0bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105664"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse에 대 한 SQL 도구 및 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

데이터베이스를 관리 (쿼리, 모니터링 등) 하려면 도구가 필요 합니다. 데이터베이스가 클라우드, Windows 또는 [Linux](../linux/sql-server-linux-overview.md)에서 실행 될 수 있는 동안에는 도구를 데이터베이스와 동일한 플랫폼에서 실행할 필요가 없습니다. 

사용할 수 있는 많은 데이터베이스 도구가 있으므로이 문서에서는 SQL 데이터베이스 작업에 사용할 수 있는 몇 가지 도구에 대 한 설명과 포인터를 제공 합니다. 필요한 도구를 결정 하는 데 도움이 필요한 경우 [어떤 도구를 사용 해야 하나요?](#which-tool-should-i-choose)를 참조 하세요.

## <a name="gui-tools-to-manage-databases"></a>데이터베이스를 관리 하는 GUI 도구  

다음은 주 GUI (그래픽 사용자 인터페이스) 도구입니다.

| 도구 | 설명 | 실행 |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]는 실행 되는 모든 데이터베이스를 관리 하는 데 사용 되는 무료 경량 도구입니다. 이 미리 보기 릴리스는 확장 된 Transact-sql 편집기를 비롯 한 데이터베이스 관리 기능과 데이터베이스의 작동 상태에 대 한 사용자 지정 가능한 정보를 제공 합니다. | **Windows, macos 및 Linux에서 실행 됩니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)]**|
| [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | SSMS (SQL Server Management Studio)를 사용 하 여 SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse를 쿼리, 디자인 및 관리할 수 있습니다. | **SSMS는 Windows에서 실행됩니다.**|
| [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | SQL Server, Azure SQL Database 및 Azure SQL Data Warehouse를 위한 강력한 개발 환경으로 Visual Studio를 전환 합니다.| **SSDT는 Windows에서 실행됩니다**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Visual Studio Code를 설치한 후 Microsoft SQL Server, Azure SQL Database 및 SQL Data Warehouse를 개발 하기 위한 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) 을 설치 합니다.| **Visual Studio Code는 Windows, macOS 및 Linux에서 실행**됩니다.|


## <a name="command-line-tools-to-manage-databases"></a>데이터베이스를 관리 하는 명령줄 도구

기본 명령줄 도구는 다음과 같습니다.

| 도구 | 설명 | 실행 |
|:--|:--|:--|
|[**mssql-cli(미리 보기)** ](mssql-cli.md)|**mssql-cli** 는 SQL Server 쿼리를 위한 대화형 명령줄 도구입니다. | Windows, macOS 및 Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage** 는 여러 데이터베이스 개발 작업을 자동화 하는 명령줄 유틸리티입니다. macOS 및 Linux 버전의 sqlpackage는 현재 미리 보기로 제공 됩니다. | Windows, macOS 및 Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** 는 SQL을 사용 하기 위한 cmdlet을 제공 합니다.| Windows, macOS 및 Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd** 유틸리티를 사용 하 여 명령 프롬프트에서 transact-sql 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다. | Windows, macOS 및 Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|**대**량 **복**사 **프**로그램 유틸리티(**bcp**)는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 대량 복사합니다.|Windows, macOS 및 Linux|
|[**mssql-스크립터 (미리 보기)** ](https://github.com/Microsoft/mssql-scripter)|**mssql-스크립터** 는 SQL Server 데이터베이스를 스크립팅 하는 다중 플랫폼 명령줄 환경입니다.|Windows, macOS 및 Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**mssql-회의** 는 Linux에서 실행 되는 SQL Server를 구성 합니다.|Linux|



## <a name="which-tool-should-i-choose"></a>어떤 도구를 선택 해야 하나요?

- Windows, Linux 또는 Mac의 경량 편집기에서 SQL Server 인스턴스 또는 데이터베이스를 관리 하 시겠습니까? [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) 선택
- Windows에서 전체 GUI 지원으로 SQL Server 인스턴스 또는 데이터베이스를 관리 하 시겠습니까? [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) 선택
- Windows에서 컴파일 시간 유효성 검사, 리팩터링 및 디자이너 지원을 포함 하 여 데이터베이스 코드를 만들거나 유지 관리 하 시겠습니까? [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) 선택
- IntelliSense, 구문 및 기타 기능을 제공 하는 명령줄 도구를 사용 하 여 SQL Server를 쿼리 할까요? [Mssql-cli](mssql-cli.md) 선택
- Windows, Linux 또는 Mac에서 경량 편집기로 T-sql 스크립트를 작성 하 시겠습니까? [Visual Studio Code](https://code.visualstudio.com/) 및 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) 을 선택 합니다.



## <a name="additional-tools"></a>추가 도구

| 도구 | 설명 |
|:--|:--|
| [구성 관리자](../tools/configuration-manager/sql-server-configuration-manager-help.md) | SQL Server 구성 관리자를 사용 하 여 SQL Server 서비스를 구성 하 고 네트워크 연결을 구성할 수 있습니다. Windows에서 실행 되는 Configuration Manager|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | SQL Server Migration Assistant를 사용하여 Microsoft Access, DB2, MySQL, Oracle 및 Sybase에서 SQL Server로 데이터베이스를 마이그레이션하는 작업을 자동화할 수 있습니다.|
| [데이터베이스 실험 도우미](../dea/database-experimentation-assistant-overview.md) | 데이터베이스 실험 도우미를 사용 하 여 지정 된 작업에 대 한 대상 SQL 버전을 평가할 수 있습니다. |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Distributed Replay 기능을 사용 하 여 향후 SQL Server 업그레이드의 영향을 쉽게 평가할 수 있습니다. 또한 Distributed Replay를 사용 하 여 하드웨어 및 운영 체제 업그레이드의 영향을 평가 하 고 SQL Server 튜닝할 수 있습니다. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 유틸리티는 Service Broker 대화 또는 Service Broker 서비스의 구성에서 문제를 보고 합니다. |

이 페이지에 설명 되지 않은 추가 도구를 찾고 있는 경우 [SQL 명령 프롬프트 유틸리티](command-prompt-utility-reference-database-engine.md)를 참조 하세요.

