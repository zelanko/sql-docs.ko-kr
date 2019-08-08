---
title: Linux의 SQL Server용 애플리케이션 개발
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 584bf33201cab5d0f57205de0fed181725187d52
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077408"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Linux의 SQL Server용 애플리케이션 개발을 시작하는 방법

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

C#, Java, Node.js, PHP, Python, Ruby, C++ 등의 다양한 프로그래밍 언어에서 Linux의 SQL Server에 연결하고 SQL Server를 사용하는 애플리케이션을 만들 수 있습니다 . 또한 인기 있는 웹 프레임워크 및 ORM(개체 관계형 매핑) 프레임워크를 사용할 수도 있습니다.

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 이와 동일한 개발 옵션을 사용하여 다른 플랫폼의 SQL Server를 대상으로 지정할 수도 있습니다. 애플리케이션은 온-프레미스 또는 클라우드, macOS의 Linux, Windows 또는 Docker에서 실행되는 SQL Server를 대상으로 할 수 있습니다. 또는 Azure SQL Database 및 Azure SQL Data Warehouse를 대상으로 지정할 수 있습니다.

## <a name="try-the-tutorials"></a>자습서 사용해 보기

SQL Server를 시작하고 애플리케이션을 빌드하는 가장 좋은 방법은 직접 사용해 보는 것입니다.

- [자습서 시작](https://aka.ms/sqldev)으로 이동합니다.
- 언어 및 개발 플랫폼을 선택합니다.
- 코드 샘플을 사용해 보세요.

> [!TIP]
> Docker에서 SQL Server용 프로그램을 개발하려는 경우 **macOS** 자습서를 살펴보세요.

## <a name="create-new-applications"></a>새 애플리케이션 만들기

새 애플리케이션을 만드는 경우 다양한 프로그래밍 언어에 사용할 수 있는 커넥터 및 인기 있는 프레임워크에 대한 요약을 보려면 [연결 라이브러리](sql-server-linux-develop-connectivity-libraries.md) 목록을 살펴보세요.

## <a name="use-existing-applications"></a>기존 애플리케이션 사용

기존 데이터베이스 애플리케이션이 있는 경우에는 Linux의 SQL Server를 대상으로 지정하도록 해당 연결 문자열을 변경하면 됩니다. Linux의 SQL Server에 대한 [알려진 문제](sql-server-linux-release-notes.md) 관련 내용을 읽어보세요.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Linux의 SQL Server에서 Windows에서 기존 SQL 도구 사용

SSMS, SSDT, PowerShell 등 Windows에서 현재 실행되는 도구는 Linux의 SQL Server에서도 작동합니다. 원격 SQL Server 인스턴스가 Linux에서는 기본적으로 실행되지 않지만 Linux에서 관리할 수는 있습니다. 

자세한 내용은 다음 항목을 참조하세요.

- [SSMS(SQL Server Management Studio)](sql-server-linux-manage-ssms.md)
- [SSDT(SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> 최상의 환경을 위해 이러한 도구의 최신 버전을 사용하고 있는지 확인합니다.

## <a name="use-new-sql-tools-for-linux"></a>Linux용 새 SQL 도구 사용

Linux, macOS 및 Windows에서 [Visual Studio Code](https://code.visualstudio.com)의 새로운 [mssql 확장](https://aka.ms/mssql-marketplace)을 사용할 수 있습니다. 단계별 연습을 진행하려면 다음 자습서를 참조하세요.

- [Visual Studio Code 사용](sql-server-linux-develop-use-vscode.md)

또한 Linux에 기본적으로 제공되는 새 명령줄 도구를 사용할 수도 있습니다. 이러한 도구에는 다음이 포함됩니다.

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>다음 단계

시작하려면 다음 빠른 시작 중 하나를 사용하여 Linux에 SQL Server를 설치합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
