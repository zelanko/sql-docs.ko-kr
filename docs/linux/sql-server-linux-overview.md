---
title: SQL Server on Linux 개요
description: 이 문서에서는 Linux에서 SQL Server를 실행하는 방법을 설명하고 자세히 알아볼 수 있는 방법에 대한 정보를 제공합니다.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 31904a43dba642c73620a66bcf4abaa066b5ef82
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531275"
---
# <a name="sql-server-on-linux"></a>SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
SQL Server 2017부터 SQL Server가 Linux에서 실행됩니다. 운영 체제에 관계없이 많은 유사한 기능과 서비스를 포함하는 동일한 SQL Server 데이터베이스 엔진입니다.
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
SQL Server 2019는 Linux에서 실행됩니다. 운영 체제에 관계없이 많은 유사한 기능과 서비스를 포함하는 동일한 SQL Server 데이터베이스 엔진입니다. 이 릴리스에 대한 자세한 내용은 [Linux용 SQL Server 2019의 새로운 기능](sql-server-linux-whats-new-2019.md)을 참조하세요.
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [SQL Server 2019](sql-server-linux-overview.md?view=sql-server-ver15)를 사용할 수 있습니다! 최신 릴리스에 있는 Linux의 새로운 기능을 알아보려면 [Linux용 SQL Server 2019의 새로운 기능](sql-server-linux-whats-new-2019.md?view=sql-server-ver15)을 참조하세요.
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [SQL Server 2019](sql-server-linux-overview.md?view=sql-server-linux-ver15)를 사용할 수 있습니다! 최신 릴리스에 있는 Linux의 새로운 기능을 알아보려면 [Linux용 SQL Server 2019의 새로운 기능](sql-server-linux-whats-new-2019.md?view=sql-server-linux-ver15)을 참조하세요.
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> SQL Server 2019를 사용할 수 있습니다! 최신 릴리스에 있는 Linux의 새로운 기능을 알아보려면 [Linux용 SQL Server 2019의 새로운 기능](sql-server-linux-whats-new-2019.md)을 참조하세요.
::: moniker-end

## <a name="install"></a>설치

시작하려면 다음 빠른 시작 중 하나를 사용하여 SQL Server on Linux를 설치합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

> [!NOTE]
> Docker 자체는 다양한 플랫폼에서 실행되므로, Linux, Mac 및 Windows에서 Docker 이미지를 실행할 수 있습니다.

## <a name="connect"></a>연결

설치 후 Linux 머신의 SQL Server 인스턴스에 연결합니다. 다양한 도구 및 드라이버를 사용하여 로컬 또는 원격으로 연결할 수 있습니다. 빠른 시작은 [sqlcmd](sql-server-linux-setup-tools.md) 명령줄 도구를 사용하는 방법을 보여 줍니다. 다른 도구에는 다음이 포함됩니다.

| 도구 | 자습서 |
|-----|-----|
| VS Code(Visual Studio Code) | [SQL Server on Linux와 함께 VS Code 사용](sql-server-linux-develop-use-vscode.md) |
| SSMS(SQL Server Management Studio) | [Windows에서 SSMS를 사용하여 SQL Server on Linux에 연결](sql-server-linux-manage-ssms.md) |
| SSDT(SQL Server Data Tools) | [SQL Server on Linux와 함께 SSDT 사용](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>탐색

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SQL Server 2017에는 Linux를 포함하여 지원되는 모든 플랫폼에서 동일한 기본 데이터베이스 엔진이 있습니다. 따라서 대부분의 기존 기능이 Linux에서 동일한 방식으로 작동합니다. 설명서의 이 영역에서는 Linux 관점에서 이와 같은 일부 기능을 공개합니다. 또한 Linux에서 고유한 요구 사항이 있는 영역을 설명합니다.

SQL Server에 이미 익숙한 경우 이 릴리스의 일반적인 지침과 알려진 문제에 대한 [릴리스 정보](sql-server-linux-release-notes.md)를 검토하세요. 그런 다음, [SQL Server on Linux의 새로운 기능](sql-server-linux-whats-new.md) 및 [SQL Server 2017 전체의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)을 살펴봅니다.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]에는 Linux를 포함한 지원되는 모든 플랫폼에서 동일한 기본 데이터베이스 엔진이 있습니다. 따라서 대부분의 기존 기능이 Linux에서 동일한 방식으로 작동합니다. 설명서의 이 영역에서는 Linux 관점에서 이와 같은 일부 기능을 공개합니다. 또한 Linux에서 고유한 요구 사항이 있는 영역을 설명합니다.

SQL Server on Linux에 이미 익숙한 경우 이 릴리스의 일반적인 지침과 알려진 문제에 대한 [릴리스 정보](sql-server-linux-release-notes-2019.md)를 검토하세요. 그런 다음, [Linux에 대한 SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)을 살펴봅니다.

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 및 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]에는 Linux를 포함하여 지원되는 모든 플랫폼에서 동일한 기본 데이터베이스 엔진이 있습니다. 따라서 대부분의 기존 기능이 Linux에서 동일한 방식으로 작동합니다. 설명서의 이 영역에서는 Linux 관점에서 이와 같은 일부 기능을 공개합니다. 또한 Linux에서 고유한 요구 사항이 있는 영역을 설명합니다.

SQL Server on Linux에 이미 익숙한 경우 릴리스 정보를 검토하세요.

- [SQL Server 2017 릴리스 정보](sql-server-linux-release-notes.md)
- [SQL Server 2019 릴리스 정보](sql-server-linux-release-notes-2019.md)

그런 다음, 새로운 기능을 살펴봅니다.

- [SQL Server 2017의 새로운 기능](sql-server-linux-whats-new.md)
- [Linux에 대한 SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> 질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
