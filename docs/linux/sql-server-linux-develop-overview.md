---
title: Linux의 SQL Server 용 응용 프로그램 개발
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 584bf33201cab5d0f57205de0fed181725187d52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077408"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Linux의 SQL Server에 대 한 응용 프로그램 개발을 시작 하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

연결 하 고 같은 다양 한 프로그래밍 언어에서에서 Linux의 SQL Server를 사용 하는 응용 프로그램을 만들 수 있습니다 C#, Java, Node.js, PHP, Python, Ruby 및 C++합니다. 또한 인기 있는 웹 프레임 워크 및 개체 관계형 매핑 (ORM) 프레임 워크를 사용할 수 있습니다.

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 이러한 동일한 개발 옵션 또한을 사용 하면 다른 플랫폼에서 SQL Server를 대상으로 합니다. 응용 프로그램 온-프레미스를 실행 중인 SQL Server 대상으로 지정할 수 또는 클라우드에서 Linux, Windows, 또는 Docker에서 macOS에서. 또는 Azure SQL Database 및 Azure SQL Data Warehouse 대상으로 지정할 수 있습니다.

## <a name="try-the-tutorials"></a>자습서

시작 하 고 SQL Server를 사용 하 여 응용 프로그램을 빌드하는 가장 좋은 방법은 직접 사용해 됩니다.

- 이동할 [시작 하기 자습서](https://aka.ms/sqldev)합니다.
- 언어 및 개발 플랫폼을 선택 합니다.
- 코드 샘플을 시도 합니다.

> [!TIP]
> Docker에서 SQL Server에 대 한 개발 하려는 경우 잠시 살펴 합니다 **macOS** 자습서입니다.

## <a name="create-new-applications"></a>새 응용 프로그램 만들기

새 응용 프로그램을 만들 경우 살펴보겠습니다 목록을 합니다 [연결 라이브러리](sql-server-linux-develop-connectivity-libraries.md) 커넥터 및 다양 한 프로그래밍 언어에 사용할 수 있는 인기 있는 프레임 워크의 개요입니다.

## <a name="use-existing-applications"></a>기존 응용 프로그램 사용

기존 데이터베이스 응용 프로그램에 있는 경우 Linux의 SQL Server 대상에 연결 문자열을 간단히 변경할 수 있습니다. 에 대 한 읽을 수 있는지 확인 합니다 [알려진 문제](sql-server-linux-release-notes.md) Linux의 SQL Server에서 합니다.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Linux의 SQL Server를 사용 하 여 Windows에서 기존 SQL 도구 사용

현재 SSMS, SSDT, PowerShell 등 Windows에서 실행 되는 도구는 또한 Linux에서 SQL Server를 사용 하 여 작동 합니다. 기본적으로 Linux에서 실행 하지 않아서, 있지만 Linux에서 원격 SQL Server 인스턴스를 계속 관리할 수 있습니다. 

자세한 내용은 다음 항목을 참조 하세요.

- [SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)
- [SSDT(SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> 최상의 환경을 위해 최신 버전의 이러한 도구를 사용 하 고 있는지 있는지 확인 합니다.

## <a name="use-new-sql-tools-for-linux"></a>새 SQL 도구를 사용 하 여 Linux 용

새 사용할 수 있습니다 [mssql 확장](https://aka.ms/mssql-marketplace) 에 대 한 [Visual Studio Code](https://code.visualstudio.com) Linux, macOS 및 Windows에서. 단계별 연습은 다음 자습서를 참조 하세요.

- [Visual Studio Code 사용](sql-server-linux-develop-use-vscode.md)

또한 Linux 용 네이티브는 새로운 명령줄 도구를 사용할 수 있습니다. 이러한 도구는 다음과 같습니다.

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>다음 단계

시작하려면 다음 빠른 시작 자습서 중 하나를 참고하여 SQL Server on Linux를 설치합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
