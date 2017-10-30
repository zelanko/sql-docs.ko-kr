---
title: "Linux에서 SQL Server 개요 | Microsoft Docs"
description: "이 항목에서는 SQL 서버가 Linux에서 실행 하 고 자세한 방법에 대해 설명 하는 방법을 설명 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 48e2d1ae54100f7ea83bdd677bf4a98859825b67
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="sql-server-on-linux"></a>Linux의 SQL Server

SQL Server 2017 Linux에서 실행 됩니다. 많은 유사 기능 및 운영 체제와 관계 없이 서비스와 동일한 SQL Server 데이터베이스 엔진은

## <a name="install"></a>Install

시작 하려면 다음 빠른 시작 자습서 중 하나를 사용 하 여 Linux에서 SQL Server를 설치 합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker 자체 즉, Linux, Mac 및 Windows에서 Docker 이미지를 실행할 수 있습니다 여러 플랫폼에서 실행 됩니다.

## <a name="connect"></a>Connect

설치가 끝나면 Linux 컴퓨터에서 SQL Server 인스턴스에 연결 합니다. 로컬 또는 원격으로 및 다양 한 도구 및 드라이버와 연결할 수 있습니다. 빠른 시작 자습서에 사용 하는 방법을 보여 주기는 [sqlcmd](sql-server-linux-setup-tools.md) 명령줄 도구입니다. 다른 도구는 다음과 같습니다.

| 도구 | 자습서 |
|-----|-----|
| Visual Studio Code (VS Code) | [VS Code Linux에서 SQL Server 사용](sql-server-linux-develop-use-vscode.md) |
| SSMS(SQL Server Management Studio) | [Windows에서 SSMS를 사용 하 여 Linux에서 SQL Server에 연결](sql-server-linux-develop-use-ssms.md) |
| SQL  Server  Data  Tools(SSDT) | [Linux에서 SQL Server와 함께 SSDT 사용](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>탐색

SQL Server 2017 Linux를 포함 하 여 모든 지원 되는 플랫폼에서 동일한 기본 데이터베이스 엔진을 있습니다. 너무 많은 기존 기능과 성능을 Linux에서 동일한 방식으로 작동합니다. 설명서의이 영역 Linux 관점에서 이러한 기능 중 일부를 노출합니다. 또한 Linux에서 고유한 요구 사항이 영역 호출 합니다.

SQL Server에 익숙한 경우 검토는 [릴리스 정보](sql-server-linux-release-notes.md) 일반적인 지침과이 릴리스의 알려진된 문제에 대 한 합니다. 다음 확인 [Linux에서 SQL Server에 대 한 새로운](sql-server-linux-whats-new.md) 으로 [SQL Server 2017 전체에 대 한 새로운](../sql-server/what-s-new-in-sql-server-2017.md)합니다.

##  <a name="infotipmediageneralinfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](./media/general/info_tip.png) SQL Server 엔지니어링 팀에 문의

- [DBA 스택 Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): 데이터베이스 관리 질문 하기
- [스택 오버플로](http://stackoverflow.com/questions/tagged/sql-server): 개발 질문 하기
- [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): 기술 관련 질문
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): 요청 기능 및 버그를 보고 합니다.
- [Reddit](https://www.reddit.com/r/SQLServer/): SQL Server에 설명

