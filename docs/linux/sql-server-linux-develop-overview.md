---
title: "Linux에서 SQL Server에 대 한 응용 프로그램을 개발 | Microsoft Docs"
description: 
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.custom: sql-linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.workload: On Demand
ms.openlocfilehash: fb07628c8818b16709abab07efc1f52248426305
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Linux에서 SQL Server 용 응용 프로그램 개발을 시작 하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

연결 하 고 SQL Server 2017 linux 다양 한 C#, Java, Node.js, PHP, Python, Ruby, 및 c + + 프로그래밍 언어에서에서 사용 하는 응용 프로그램을 만들 수 있습니다. 인기 있는 웹 프레임 워크 및 개체 관계형 매핑 ORM () 프레임 워크를 사용할 수도 있습니다.

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 이러한 동일한 개발 옵션 또한을 사용 하면 다른 플랫폼에서 SQL Server를 대상으로 합니다. 응용 프로그램에는 온-프레미스를 실행 중인 SQL Server 대상 수 또는 클라우드에서 Linux, Windows 또는 Docker에서 macOS에서 합니다. 또는 Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 대상으로 지정할 수 있습니다.

## <a name="try-the-tutorials"></a>자습서

시작 하 고 SQL Server와 응용 프로그램을 빌드하는 가장 좋은 방법은 직접 시도해는 합니다.

- 찾아 [자습서 시작](http://aka.ms/sqldev)합니다.
- 언어 및 개발 플랫폼을 선택 합니다.
- 코드 샘플을 시도 합니다.

> [!TIP]
> Docker에서 SQL Server 2017을 개발 하려는 경우에 대해 살펴봅니다는 **macOS** 자습서입니다.

## <a name="create-new-applications"></a>새 응용 프로그램 만들기

새 응용 프로그램을 만드는 경우에 대해 살펴봅니다 목록은 [연결 라이브러리](sql-server-linux-develop-connectivity-libraries.md) 커넥터 및 다양 한 프로그래밍 언어에 사용할 수 있는 인기 있는 프레임 워크의 요약입니다.

## <a name="use-existing-applications"></a>기존 응용 프로그램을 사용 하 여

기존 데이터베이스 응용 프로그램의 경우 대상 SQL Server 2017 Linux에서 단순히 해당 연결 문자열을 변경할 수 있습니다. 에 대 한 읽을 수 있는지 확인은 [알려진 문제](sql-server-linux-release-notes.md) SQL Server 2017 linux에 있습니다.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>기존 SQL 도구를 사용 하 여 Linux에서 SQL Server와 Windows에서

SQL Server 2017 linux와 SSMS, SSDT 및 PowerShell 등의 Windows에서 현재 실행 하는 도구 에서도 작동 합니다. 하지만를 실행 하지 않으면 기본적으로 Linux에서 Linux에서 원격 SQL Server 인스턴스 계속 관리할 수 있습니다. 

자세한 내용은 다음 항목을 참조 하십시오.

- [SSMS(SQL Server Management Studio)](sql-server-linux-develop-use-ssms.md)
- [SSDT(SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note] 
> 최상의 환경을 위해 이러한 도구의 최신 버전을 사용 하 고 있는지 확인 합니다.

## <a name="use-new-sql-tools-for-linux"></a>새 SQL 도구를 사용 하 여 Linux 용

새 사용할 수 있습니다 [확장명이 mssql](https://aka.ms/mssql-marketplace) 에 대 한 [Visual Studio Code](https://code.visualstudio.com) Linux, macOS 등 창에 있습니다. 단계별 연습에서는 다음 자습서를 참조 합니다.

- [Visual Studio Code 사용](sql-server-linux-develop-use-vscode.md)

Linux 용 적용 되는 새로운 명령줄 도구를 사용할 수 있습니다. 이러한 도구는 다음과 같습니다.

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 퀵 스타트 중 하나를 사용 하 여 Linux에서 SQL Server를 설치 합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
