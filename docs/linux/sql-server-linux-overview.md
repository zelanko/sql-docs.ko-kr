---
title: SQL Server on Linux 개요 | Microsoft Docs
description: 이 항목에서는 SQL 서버를 Linux에서 실행하는 방법 및 자세한 학습 방법에 대한 정보를 제공합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: c24e4fa86c92a183c957c44a33a2d3524cdd1f8c
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63457369"
---
# <a name="sql-server-on-linux"></a>SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
SQL Server 2017부터 SQL Server는 Linux에서 실행 됩니다. 많은 유사 기능 및 운영 체제에 관계 없이 서비스를 사용 하 여 동일한 SQL Server 데이터베이스 엔진, 것입니다.
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
SQL Server 2019 미리 보기는 Linux에서 실행 됩니다. 많은 유사 기능 및 운영 체제에 관계 없이 서비스를 사용 하 여 동일한 SQL Server 데이터베이스 엔진, 것입니다. 이 릴리스에 대 한 자세한 내용을 참조 하세요 [Linux 용 SQL Server 2019 미리 보기의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)합니다.
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [SQL Server 2019 미리 보기](sql-server-linux-overview.md?view=sql-server-ver15) 놓았습니다. Linux 용 최신 릴리스의 새로운 기능을 확인 하려면 [Linux 용 SQL Server 2019 미리 보기의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)을 참조합니다.
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [SQL Server 2019 미리 보기](sql-server-linux-overview.md?view=sql-server-linux-ver15) 놓았습니다. Linux 용 최신 릴리스의 새로운 기능을 확인 하려면 [Linux 용 SQL Server 2019 미리 보기의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-linux-ver15#sql-server-on-linux)을 참조합니다.
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> SQL Server 2019 미리 보기가 공개되었습니다. Linux 용 최신 릴리스의 새로운 기능을 확인 하려면 [Linux 용 SQL Server 2019 미리 보기의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)을 참조합니다.
::: moniker-end

## <a name="install"></a>Install

시작하려면 다음 빠른 시작 자습서 중 하나를 참고하여 SQL Server on Linux를 설치합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker 자체는 여러 플랫폼에서 실행됩니다. 즉, Linux, Mac 및 Windows에서 Docker 이미지를 실행할 수 있습니다.

## <a name="connect"></a>연결

설치를 완료한 후, Linux 컴퓨터에서 SQL Server 인스턴스에 연결합니다 로컬 또는 원격으로 다양한 도구 및 드라이버를 사용하여 연결할 수 있습니다. 빠른 시작 자습서에서는 [sqlcmd](sql-server-linux-setup-tools.md) 명령줄 도구를 사용하는 방법을 보여줍니다. 다음과 같은 다른 도구들도 있습니다.

| 도구 | 자습서 |
|-----|-----|
| Visual Studio Code (VS Code) | [SQL Server on Linux에서 VS Code 사용](sql-server-linux-develop-use-vscode.md) |
| SSMS(SQL Server Management Studio) | [Windows에서 SSMS를 사용하여 SQL Server on Linux에 연결](sql-server-linux-manage-ssms.md) |
| SQL  Server  Data  Tools(SSDT) | [SQL Server on Linux에서 SSDT 사용](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>탐색

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SQL Server 2017은 Linux를 포함하여 모든 지원되는 플랫폼에 동일한 기본 데이터베이스 엔진을 가지고 있습니다 따라서 여러 기존 기능을 Linux에서 동일한 방식으로 작동합니다. 이 문서에서는 이러한 기능 중 일부를 Linux 관점에서 설명합니다 또한 Linux에만 해당하는 요구 사항에 대해 설명합니다.

SQL Server에 이미 익숙한 경우, [릴리스 정보](sql-server-linux-release-notes.md) 를 참고하여 일반적인 지침과 릴리스의 알려진 문제를 살펴봅니다. 그리고 [SQL Server on Linux의 새로운 기능](sql-server-linux-whats-new.md) 과 [SQL Server 2017 전반에 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md) 을 살펴봅니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Linux를 비롯 한 모든 지원 되는 플랫폼에서 동일한 기본 데이터베이스 엔진을 있습니다. 따라서 여러 기존 기능을 Linux에서 동일한 방식으로 작동합니다. 이 문서에서는 이러한 기능 중 일부를 Linux 관점에서 설명합니다 또한 Linux에만 해당하는 요구 사항에 대해 설명합니다.

Linux의 SQL Server에 익숙한 경우 검토 합니다 [릴리스](sql-server-linux-release-notes-2019.md) 일반 지침 및이 릴리스의 알려진된 문제에 대 한 합니다. 그러면 [Linux에서 SQL Server 2019 미리 보기에 대 한 새로운](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)합니다.

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 및 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Linux를 비롯 한 모든 지원 되는 플랫폼에 동일한 기본 데이터베이스 엔진에 있습니다. 따라서 여러 기존 기능을 Linux에서 동일한 방식으로 작동합니다. 이 문서에서는 이러한 기능 중 일부를 Linux 관점에서 설명합니다 또한 Linux에만 해당하는 요구 사항에 대해 설명합니다.

Linux의 SQL Server에 익숙한 경우 릴리스 정보를 검토 합니다.

- [SQL Server 2017 릴리스 정보](sql-server-linux-release-notes.md)
- [SQL Server 2019 미리 보기 릴리스 정보](sql-server-linux-release-notes-2019.md)

그런 다음 새로운 살펴보겠습니다.

- [SQL Server 2017의 새로운 기능](sql-server-linux-whats-new.md)
- [Linux용 SQL Server 2019 미리 보기의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> 자주 묻는 질문에 대한 답변은, [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
