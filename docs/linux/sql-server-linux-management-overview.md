---
title: "Linux에서 SQL Server 관리 | Microsoft Docs"
description: "이 문서에서는 Linux에서 실행 중인 SQL Server에 대 한 일반 관리 작업 및 도구에 대 한 링크 합니다."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: de19f1952465c62bf026dbd3d92666b7a1b968ae
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Linux에서 SQL Server를 관리 하는 적절 한 도구 선택

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 2017 linux를 관리 하는 방법은 여러 가지가 있습니다. 다음 섹션의 다른 관리 도구와 기술을 더 많은 리소스에 대 한 포인터와 간략 한 개요를 제공합니다.

## <a name="mssql-conf"></a>mssql-conf 
**mssql conf** 도구는 Linux에서 SQL Server를 구성 합니다. 자세한 내용은 참조 [mssql conf와 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.

## <a name="transact-sql"></a>Transact-SQL

클라이언트 도구에서 수행할 수 있는 모든 항목이 거의 Transact SQL 문으로 수행할 수도 있습니다. SQL Server에서 제공 [동적 관리 뷰 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 상태와 구성을 SQL server를 쿼리 합니다. 또한 [TRANSACT-SQL 명령을](https://msdn.microsoft.com/library/bb510741.aspx) 데이터베이스 관리 작업에 대 한 합니다. SQL Server에 연결 및 예를 들어 TRANSACT-SQL 쿼리를 실행할 수 있도록 하는 클라이언트 도구에서 이러한 명령을 실행할 수 있습니다 [sqlcmd](sql-server-linux-setup-tools.md) 또는 [Visual Studio Code](sql-server-linux-develop-use-vscode.md)합니다.

## <a name="sql-server-operations-studio-preview"></a>SQL Server 작업 Studio (미리 보기)

새 Microsoft SQL 작업 Studio (미리 보기)는 SQL Server를 관리 하기 위한 플랫폼 간 도구입니다. 자세한 내용은 참조 [Microsoft SQL 작업 Studio (미리 보기)](../sql-operations-studio/what-is.md)합니다.

## <a name="sql-server-management-studio-on-windows"></a>Windows에서 SQL Server Management Studio

SQL Server Management Studio (SSMS)는 SQL Server를 관리 하기 위한 그래픽 사용자 인터페이스를 제공 하는 Windows 응용 프로그램. 현재 창 에서만 실행, 원격으로 Linux SQL Server 인스턴스에 연결 하는 데 사용할 수 있습니다. SSMS를 사용 하 여 SQL Server 관리에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server 관리를 사용 하 여 SSMS](sql-server-linux-manage-ssms.md)합니다.

## <a name="mssql-cli-preview"></a>mssql-cli (미리 보기)

Microsoft SQL Server에 대 한 새로운 플랫폼 간 스크립팅 도구를 출시 했습니다 [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)합니다. 이 도구는 현재 미리 보기입니다.

## <a name="powershell"></a>PowerShell

PowerShell에는 Linux에서 SQL Server를 관리 하는 풍부한 명령줄 환경을 제공 합니다. 자세한 내용은 참조 [PowerShell Linux에서 SQL Server 관리를 사용 하 여](sql-server-linux-manage-powershell.md)합니다.

## <a name="next-steps"></a>다음 단계

Linux에서 SQL Server에 대 한 자세한 내용은 참조 [Linux에서 SQL Server](sql-server-linux-overview.md)합니다.
