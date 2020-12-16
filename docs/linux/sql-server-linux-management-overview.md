---
title: SQL Server on Linux 관리
description: 이 문서에서는 Linux에서 실행되는 SQL Server에 대한 일반적인 관리 작업 및 도구의 링크를 제공합니다.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 '
ms.openlocfilehash: dd0151edd199c5627b9676db5ed2ff304c1f5c3f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471554"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>SQL Server on Linux를 관리할 올바른 도구 선택

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

다양한 방법으로 SQL Server on Linux를 관리할 수 있습니다. 다음 섹션에서는 추가 리소스에 대한 포인터를 사용하여 다양한 관리 도구 및 기술에 대해 간략히 설명합니다.

## <a name="mssql-conf"></a>mssql-conf 

**mssql-conf** 도구는 SQL Server on Linux를 구성합니다. 자세한 내용은 [mssql-conf를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조하세요.

## <a name="transact-sql"></a>Transact-SQL

클라이언트 도구에서 수행할 수 있는 거의 모든 작업은 Transact-SQL 문을 사용하여 수행할 수도 있습니다. SQL Server는 SQL Server의 상태와 구성을 쿼리하는 [DMV(동적 관리 뷰)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 제공합니다. 데이터베이스 관리 작업을 위한 [Transact-SQL 명령](../t-sql/language-reference.md)도 있습니다. SQL Server에 대한 연결 및 Transact-SQL 쿼리 실행을 지원하는 [sqlcmd](sql-server-linux-setup-tools.md) 또는 [Visual Studio Code](../tools/visual-studio-code/sql-server-develop-use-vscode.md) 같은 모든 클라이언트 도구에서 이 명령을 실행할 수 있습니다.

## <a name="azure-data-studio"></a>Azure Data Studio

새 Azure Data Studio는 SQL Server를 관리하기 위한 플랫폼 간 도구입니다. 자세한 내용은 [Azure Data Studio](../azure-data-studio/what-is.md)를 참조하세요.

## <a name="sql-server-management-studio-on-windows"></a>Windows의 SQL Server Management Studio

SSMS(SQL Server Management Studio)는 SQL Server를 관리하기 위한 그래픽 사용자 인터페이스를 제공하는 Windows 애플리케이션입니다. 현재 Windows에서만 실행되지만 Linux SQL Server 인스턴스에 원격으로 연결하는 데 사용할 수 있습니다. SSMS를 사용하여 SQL Server를 관리하는 방법에 대한 자세한 내용은 [SSMS를 사용하여 SQL Server on Linux 관리](sql-server-linux-manage-ssms.md)를 참조하세요.

## <a name="mssql-cli-preview"></a>mssql-cli(미리 보기)

Microsoft는 새로운 SQL Server용 플랫폼 간 스크립팅 도구인 [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)를 릴리스했습니다. 이 도구는 현재 미리 보기로 제공됩니다.

## <a name="powershell"></a>PowerShell

PowerShell은 SQL Server on Linux를 관리하기 위한 다양한 명령줄 환경을 제공합니다. 자세한 내용은 [PowerShell을 사용하여 SQL Server on Linux 관리](sql-server-linux-manage-powershell.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

SQL Server on Linux에 대한 자세한 내용은 [SQL Server on Linux](sql-server-linux-overview.md)를 참조하세요.