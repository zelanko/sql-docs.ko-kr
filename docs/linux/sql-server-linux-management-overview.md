---
title: "Linux에서 SQL Server 관리 | Microsoft Docs"
description: "이 항목에서는 Linux에서 실행 중인 SQL Server에 대 한 일반 관리 작업 및 도구에 대 한 링크."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: b9fc5e53400fb83006d47213c84541dadfb11b38
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Linux에서 SQL Server를 관리 하는 적절 한 도구 선택

SQL Server 2017 RC2 linux를 관리 하는 방법은 여러 가지가 있습니다. 다음 섹션의 다른 관리 도구와 기술을 더 많은 리소스에 대 한 포인터와 간략 한 개요를 제공 합니다.

## <a name="mssql-conf"></a>mssql conf 
**mssql conf** 도구는 Linux에서 SQL Server를 구성 합니다. 자세한 내용은 참조 [mssql conf와 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.

## <a name="transact-sql"></a>Transact-SQL

클라이언트 도구에서 수행할 수 있는 모든 항목이 거의 Transact SQL 문으로 수행할 수도 있습니다. SQL Server에서 제공 [동적 관리 뷰 (Dmv)](https://msdn.microsoft.com/library/ms188754.aspx) 상태와 구성을 SQL server를 쿼리 합니다. 또한 [TRANSACT-SQL 명령을](https://msdn.microsoft.com/library/bb510741.aspx) 데이터베이스 관리 작업에 대 한 합니다. SQL Server에 연결 및 TRANSACT-SQL 쿼리를 실행할 수 있도록 하는 클라이언트 도구에서 이러한 명령을 실행할 수 있습니다. 예를 들면 [sqlcmd](sql-server-linux-setup-tools.md), [Visual Studio Code](sql-server-linux-develop-use-vscode.md), 및 [SQL Server Management Studio](sql-server-linux-manage-ssms.md)합니다.

## <a name="sql-server-management-studio-on-windows"></a>Windows에서 SQL Server Management Studio

SQL Server Management Studio (SSMS)는 SQL Server를 관리 하기 위한 그래픽 사용자 인터페이스를 제공 하는 Windows 응용 프로그램. 현재 창 에서만 실행, 원격으로 Linux SQL Server 인스턴스에 연결 하는 데 사용할 수 있습니다. SSMS를 사용 하 여 SQL Server 관리에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server 관리를 사용 하 여 SSMS](sql-server-linux-manage-ssms.md)합니다.

## <a name="powershell"></a>PowerShell

PowerShell에는 Linux에서 SQL Server를 관리 하는 풍부한 명령줄 환경을 제공 합니다. 자세한 내용은 참조 [PowerShell Linux에서 SQL Server 관리를 사용 하 여](sql-server-linux-manage-powershell.md)합니다.

## <a name="next-steps"></a>다음 단계

Linux에서 SQL Server에 대 한 자세한 내용은 참조 [Linux에서 SQL Server](sql-server-linux-overview.md)합니다.
