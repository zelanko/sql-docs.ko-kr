---
title: SQL Server 2017 및 2019에 대한 Linux 리포지토리 구성
description: Linux에서 SQL Server 2019 및 SQL Server 2017의 원본 리포지토리를 확인하고 구성합니다. 원본 리포지토리는 설치 및 업그레이드 중에 적용되는 SQL Server 버전에 영향을 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 5f302c774ccb4c3f98722e4b416968a813f951bd
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198430"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>SQL Server on Linux 설치 및 업그레이드를 위한 리포지토리 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
이 문서에서는 Linux에서 SQL Server 2017 및 SQL Server 2019 설치 및 업그레이드를 위해 올바른 리포지토리를 구성하는 방법을 설명합니다. 맨 위에 있는 현재 선택 항목은 **Red Hat(RHEL)** 입니다.
::: zone-end

::: zone pivot="ld2-sles"
이 문서에서는 Linux에서 SQL Server 2017 및 SQL Server 2019 설치 및 업그레이드를 위해 올바른 리포지토리를 구성하는 방법을 설명합니다. 맨 위에 있는 현재 선택 항목은 **SUSE(SLES)** 입니다.
::: zone-end

::: zone pivot="ld2-ubuntu"
이 문서에서는 Linux에서 SQL Server 2017 및 SQL Server 2019 설치 및 업그레이드를 위해 올바른 리포지토리를 구성하는 방법을 설명합니다. 맨 위에 있는 현재 선택 항목은 **Ubuntu**입니다.
::: zone-end

> [!TIP]
> 이제 SQL Server 2019를 사용할 수 있습니다! 사용해 보려면 이 문서를 사용하여 새 **mssql-server-2019** 리포지토리를 구성합니다. 그런 다음 [설치 가이드](sql-server-linux-setup.md)의 지침을 사용하여 설치합니다.

## <a name="repositories"></a><a id="repositories"></a> 리포지토리

SQL Server on Linux를 설치하는 경우 Microsoft 리포지토리를 구성해야 합니다. 이 리포지토리는 데이터베이스 엔진 패키지인 **mssql-server** 및 관련 SQL Server 패키지를 가져오는 데 사용됩니다. 현재 다음과 같은 다섯 가지 기본 리포지토리가 있습니다.

| 리포지토리 | 속성 | Description |
|---|---|---|
| **2019** | **mssql-server-2019** | SQL Server 2019 CU(누적 업데이트) 리포지토리. |
| **2019 GDR** | **mssql-server-2019-gdr** | 중요 업데이트 전용 SQL Server 2019 GDR 리포지토리. |
| **2019 미리 보기** | **mssql-server-preview** | SQL Server 2019 미리 보기 및 RC 리포지토리. |
| **2017** | **mssql-server-2017** | SQL Server 2017 CU(누적 업데이트) 리포지토리. |
| **2017 GDR** | **mssql-server-2017-gdr** | 중요 업데이트 전용 SQL Server 2017 GDR 리포지토리. |

## <a name="cumulative-update-versus-gdr"></a><a id="cuversusgdr"></a> 누적 업데이트 및 GDR

각 배포에 대해 다음과 같은 두 가지 기본 유형의 리포지토리가 있습니다.

- **CU(누적 업데이트)** : CU(누적 업데이트) 리포지토리에는 기본 SQL Server 릴리스 패키지와 해당 릴리스 이후 버그 수정 또는 향상된 기능이 포함됩니다. 누적 업데이트는 SQL Server 2019 등의 릴리스 버전에만 적용됩니다. 누적 업데이트는 정기적으로 릴리스됩니다.

- **GDR**: GDR 리포지토리에는 기본 SQL Server 릴리스 패키지 및 해당 릴리스 이후 중요 수정과 보안 업데이트만 포함됩니다. 이 업데이트는 다음 CU 릴리스에도 추가됩니다.

각 CU 및 GDR 릴리스에는 전체 SQL Server 패키지 및 해당 리포지토리의 모든 이전 업데이트가 포함됩니다. SQL Server에 대해 구성된 리포지토리를 변경하여 GDR 릴리스에서 CU 릴리스로 업데이트할 수 있습니다. 주 버전 내(예: 2017)의 모든 릴리스로 [다운그레이드](sql-server-linux-setup.md#rollback)할 수도 있습니다.

> [!NOTE]
> 언제든지 리포지토리를 변경하여 GDR 릴리스에서 CU 릴리스로 업데이트할 수 있습니다. CU 릴리스에서 GDR 릴리스로 업데이트할 수는 없습니다.

## <a name="configure-repositories"></a>리포지토리 구성

::: zone pivot="ld2-rhel"
다음 섹션의 단계를 사용하여 RHEL(Red Hat Enterprise Server)에서 리포지토리를 구성합니다.
::: zone-end

::: zone pivot="ld2-sles"
다음 섹션의 단계를 사용하여 SLES(SUSE Linux Enterprise Server)에서 리포지토리를 구성합니다.
::: zone-end

::: zone pivot="ld2-ubuntu"
다음 섹션의 단계를 사용하여 Ubuntu에서 리포지토리를 구성합니다.
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>이전에 구성한 리포지토리를 확인합니다.

<!--RHEL-->
::: zone pivot="ld2-rhel"
먼저 SQL Server 리포지토리를 이미 등록했는지 확인합니다.

1. 다음 명령을 사용하여 **/etc/yum.repos.d** 디렉터리의 파일을 확인합니다.

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. SQL Server 디렉터리를 구성하는 파일(예: **mssql-server.repo**)을 검색합니다.

3. 파일의 콘텐츠를 인쇄합니다.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **name** 속성은 구성된 리포지토리입니다. 이 문서의 [리포지토리](#repositories) 섹션에 있는 표를 사용하여 식별할 수 있습니다.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
먼저 SQL Server 리포지토리를 이미 등록했는지 확인합니다.

1. **zypper info**를 사용하여 이전에 구성한 리포지토리 관련 정보를 가져옵니다.

   ```bash
   sudo zypper info mssql-server
   ```

2. **Repository** 속성은 구성된 리포지토리입니다. 이 문서의 [리포지토리](#repositories) 섹션에 있는 표를 사용하여 식별할 수 있습니다.

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
먼저 SQL Server 리포지토리를 이미 등록했는지 확인합니다.

1. **/etc/apt/sources.list** 파일의 콘텐츠를 확인합니다.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. mssql-server의 패키지 URL을 확인합니다. 이 문서의 [리포지토리](#repositories) 섹션에 있는 표를 사용하여 식별할 수 있습니다.

::: zone-end

## <a name="remove-old-repository"></a>이전 리포지토리 제거

<!--RHEL-->
::: zone pivot="ld2-rhel"
필요한 경우 다음 명령을 사용하여 이전 리포지토리를 제거합니다.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

이 명령은 이전 섹션에서 식별된 파일의 이름이 **mssql-server.repo**였다고 가정합니다.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
필요한 경우 이전 리포지토리를 제거합니다. 이전에 구성한 리포지토리의 유형에 따라 다음 명령 중 하나를 사용합니다.

| 리포지토리 | 제거할 명령 |
|---|---|
| **미리 보기(2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **2019 CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019'` |
| **2019 GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019-gdr'`|
| **2017 CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **2017 GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
필요한 경우 이전 리포지토리를 제거합니다. 이전에 구성한 리포지토리의 유형에 따라 다음 명령 중 하나를 사용합니다.

> [!NOTE]
> SQL Server 2019 CU3부터 Ubuntu 18.04가 지원됩니다. Ubuntu 16.04를 사용하는 경우 아래 경로를 `/ubuntu/18.04` 대신 `/ubuntu/16.04`로 변경합니다.

| 리포지토리 | 제거할 명령 |
|---|---|
| **미리 보기(2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **2019 CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019 xenial main'` | 
| **2019 GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019-gdr xenial main'` |
| **2017 CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **2017 GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>새 리포지토리 구성

<!--RHEL-->
::: zone pivot="ld2-rhel"
SQL Server 설치 및 업그레이드에 사용할 새 리포지토리를 구성합니다. 다음 명령 중 하나를 사용하여 선택한 리포지토리를 구성합니다.

> [!NOTE]
> SQL Server 2019에 대한 다음 명령은 RHEL 8 리포지토리를 가리킵니다. RHEL 8에는 SQL Server에 필요한 python2이 사전 설치되어 있지 않습니다. 자세한 내용은 python2 설치 및 기본 인터프리터로 구성하는 방법에 대한 블로그(https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta )를 참조하세요.
>
> RHEL 7을 사용 중인 경우 아래 경로를 `/rhel/8` 대신 `/rhel/7`(으)로 변경합니다.

| 리포지토리 | 버전 | 명령 |
|---|---|---|
| **2019 CU** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo` |
| **2019 GDR** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019-gdr.repo` |
| **2017 CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **2017 GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
SQL Server 설치 및 업그레이드에 사용할 새 리포지토리를 구성합니다. 다음 명령 중 하나를 사용하여 선택한 리포지토리를 구성합니다.

| 리포지토리 | 버전 | 명령 |
|---|---|---|
| **2019 CU** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo` |
| **2019 GDR** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019-gdr.repo` |
| **2017 CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **2017 GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
SQL Server 설치 및 업그레이드에 사용할 새 리포지토리를 구성합니다.

> [!NOTE]
> SQL Server 2019 CU3부터 Ubuntu 18.04가 지원됩니다. SQL Server 2019에서 다음 명령은 Ubuntu 18.04 리포지토리를 가리킵니다.
>
> Ubuntu 16.04를 사용하는 경우 아래 경로를 `/ubuntu/18.04` 대신 `/ubuntu/16.04`로 변경합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 다음 명령 중 하나를 사용하여 선택한 리포지토리를 구성합니다.

   | 리포지토리 | 버전 | 명령 |
   |---|---|---|
   | **2019 CU** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"` |
   | **2019 GDR** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019-gdr.list)"` |
   | **2017 CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **2017 GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. **apt-get update**를 실행합니다.

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>다음 단계

올바른 리포지토리를 구성한 후에는 새 리포지토리에서 SQL Server 및 관련 패키지를 [설치](sql-server-linux-setup.md#platforms) 또는 [업데이트](sql-server-linux-setup.md#upgrade)할 수 있습니다.

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> 이때 [RHEL 빠른 시작](quickstart-install-connect-red-hat.md)을 사용하도록 선택하는 경우에는 대상 리포지토리를 이미 구성했어야 합니다. 자습서에서 해당 단계를 반복하지 마세요. 빠른 시작에서 CU 리포지토리를 사용하므로 특히 GDR 리포지토리를 구성하는 경우가 여기에 해당합니다.
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> 이때 [SLES 빠른 시작](quickstart-install-connect-suse.md)을 사용하도록 선택하는 경우에는 대상 리포지토리를 이미 구성했어야 합니다. 자습서에서 해당 단계를 반복하지 마세요. 빠른 시작에서 CU 리포지토리를 사용하므로 특히 GDR 리포지토리를 구성하는 경우가 여기에 해당합니다.
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> 이때 [Ubuntu 빠른 시작](quickstart-install-connect-ubuntu.md)을 사용하도록 선택하는 경우에는 대상 리포지토리를 이미 구성했어야 합니다. 자습서에서 해당 단계를 반복하지 마세요. 빠른 시작에서 CU 리포지토리를 사용하므로 특히 GDR 리포지토리를 구성하는 경우가 여기에 해당합니다.
::: zone-end

SQL Server 2017 on Linux를 설치하는 방법에 대한 자세한 내용은 [SQL Server on Linux 설치 지침](sql-server-linux-setup.md)을 참조하세요.
