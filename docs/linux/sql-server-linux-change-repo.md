---
title: Linux에서 SQL Server에 대 한 저장소를 구성 | Microsoft Docs
description: 확인 하 고 SQL Server 2017 linux에 대 한 소스 저장소를 구성 합니다. 소스 저장소 버전을의 설치 및 업그레이드 하는 동안 적용 되는 SQL Server에 영향을 줍니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 63cb2f56852a668bc48aa85cd31a72a2b583463b
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323374"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>설치 및 Linux에서 SQL Server 업그레이드에 대 한 저장소를 구성 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 SQL Server 2017 설치 및 업그레이드에 대 한 올바른 저장소를 구성 하는 방법을 설명 합니다.

> [!IMPORTANT]
> CTP 또는 SQL Server 2017의 RC 버전을 이전에 설치한 경우 GA (일반 공급) 리포지토리를 등록 하 고 업그레이드 또는 다시 설치 하려면이 문서의 단계를 사용 해야 합니다. 미리 보기 릴리스의 SQL Server 2017 지원 되지 않으며 만료 됩니다.

## <a id="repositories"></a>저장소

Linux에서 SQL Server를 설치 하는 경우 Microsoft 저장소를 구성 해야 합니다. 이 저장소는 데이터베이스 엔진 패키지를 얻는 데 **mssql 서버**, 및 관련 SQL Server 패키지 합니다. 세 가지 주 저장소는 현재:

| 리포지토리 | 이름 | Description |
|---|---|---|
| **미리 보기** | **mssql-server** | CTP 및 RC 버전의 SQL Server에 대 한 미리 보기 리포지토리. 이 저장소는 SQL Server 2017에 대 한 지원 되지 않습니다. |
| **CU** | **mssql-server-2017** | SQL Server 2017 CU (누적 업데이트) 리포지토리. |
| **GDR** | **mssql-server-2017-gdr** | 중요 한 업데이트에만 SQL Server 2017 GDR 리포지토리. |

## <a id="cuversusgdr"></a> GDR 및 누적 업데이트

같은 두 가지 유형의 각 배포에 대 한 저장소는을 고려해 야 합니다.

- **CU (누적 업데이트)**: The CU (누적 업데이트) 저장소 해당 릴리스 이후 기본 SQL Server 릴리스 및 버그 수정 또는 향상 된 기능에 대 한 패키지를 포함 합니다. 누적 업데이트는 SQL Server 2017 등의 릴리스 버전에 고유 합니다. 일반 주기로 릴리스되는 합니다.

- **GDR**: The GDR 리포지토리 해당 릴리스 이후는 기본 SQL Server 릴리스만 주요 수정 프로그램 및 보안 업데이트에 대 한 패키지를 포함 합니다. 이러한 업데이트는 다음 CU 릴리스로 추가 됩니다.

각 CU 및 GDR 릴리스에 전체 SQL Server 패키지 및 해당 저장소에 대 한 모든 이전 업데이트를 포함합니다. CU 릴리스에 GDR 릴리스의 업데이트는 SQL Server에 대 한 구성된 저장소를 변경 하 여 지원 됩니다. 수도 있습니다 [다운 그레이드](sql-server-linux-setup.md#rollback) 주요 버전 내에서 모든 릴리스를 (예: 2017).

> [!NOTE]
> CU GDR 릴리스에서 업데이트할 있습니다 저장소를 변경 하 여 언제 든 지 해제 합니다. 업데이트 CU에서 릴리스를 GDR 릴리스 지원 되지 않습니다. 

## <a id="configure"></a> 저장소 구성

다음 섹션에서는 다음과 같은 지원 되는 플랫폼에 대 한 저장소를 구성 하 고 확인 하는 방법에 설명 합니다.

- [Red Hat Enterprise 서버](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> RHEL 저장소 구성
Red Hat Enterprise 서버 (RHEL) 저장소를 구성 하려면 다음 단계를 사용 합니다.

### <a name="check-for-previously-configured-repositories-rhel"></a>이전에 구성 된 저장소 (RHEL)에 대 한 확인
먼저 SQL Server 저장소 이미 등록 하는지 여부를 확인 합니다.

1. 파일을 볼는 **/etc/yum.repos.d** 다음 명령을 사용 하 여 디렉터리:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 와 같은 SQL Server 디렉터리를 구성 하는 파일을 찾도록 **mssql server.repo**합니다.

3. 파일의 내용을 출력 합니다.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **이름** 속성은 구성된 저장소입니다. 테이블에서 확인할 수 있습니다는 [저장소](#repositories) 이 문서의 섹션.

### <a name="remove-old-repository-rhel"></a>이전 리포지토리 (RHEL)를 제거 합니다.
필요한 경우 다음 명령 사용 하 여 이전 저장소를 제거 합니다.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

이 명령에서는 이전 섹션에서 식별 된 파일 이름이 **mssql server.repo**합니다.

### <a name="configure-new-repository-rhel"></a>새 저장소 (RHEL) 구성
SQL Server 설치 및 업그레이드에 사용할 새 저장소를 구성 합니다. 사용자가 선택한 저장소를 구성 하려면 다음 명령 중 하나를 사용 합니다.

| 리포지토리 | Command |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> SLES 저장소 구성
SLES에서 저장소를 구성 하려면 다음 단계를 사용 합니다.

### <a name="check-for-previously-configured-repositories-sles"></a>이전에 구성 된 저장소 (SLES)에 대 한 확인
먼저 SQL Server 저장소 이미 등록 하는지 여부를 확인 합니다.

1. 사용 하 여 **zypper 정보** 는 이전에 구성 된 저장소에 대 한 정보를 얻을 수 있습니다.

   ```bash
   sudo zypper info mssql-server
   ```

2. **리포지토리** 속성은 구성된 저장소입니다. 테이블에서 확인할 수 있습니다는 [저장소](#repositories) 이 문서의 섹션.

### <a name="remove-old-repository-sles"></a>이전 리포지토리 (SLES)를 제거 합니다.
필요한 경우 이전 저장소를 제거 합니다. 이전에 구성 된 저장소 형식에 따라 다음 명령 중 하나를 사용 합니다.

| 리포지토리 | 제거 하려면 명령 |
|---|---|
| **미리 보기** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>새 저장소 (SLES) 구성
SQL Server 설치 및 업그레이드에 사용할 새 저장소를 구성 합니다. 사용자가 선택한 저장소를 구성 하려면 다음 명령 중 하나를 사용 합니다.

| 리포지토리 | Command |
|---|---|
| **CU** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> Ubuntu 저장소 구성
Ubuntu에서 저장소를 구성 하려면 다음 단계를 사용 합니다.

### <a name="check-for-previously-configured-repositories-ubuntu"></a>이전에 구성 된 저장소 (Ubuntu)에 대 한 확인
먼저 SQL Server 저장소 이미 등록 하는지 여부를 확인 합니다.

1. 내용 보기는 **/etc/apt/sources.list** 파일입니다.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Mssql 서버에 대 한 패키지 URL을 검사 합니다. 테이블에서 확인할 수 있습니다는 [저장소](#repositories) 이 문서의 섹션.

### <a name="remove-old-repository-ubuntu"></a>이전 리포지토리 (Ubuntu)를 제거 합니다.
필요한 경우 이전 저장소를 제거 합니다. 이전에 구성 된 저장소 형식에 따라 다음 명령 중 하나를 사용 합니다.

| 리포지토리 | 제거 하려면 명령 |
|---|---|
| **미리 보기** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>새 저장소 (Ubuntu) 구성
SQL Server 설치 및 업그레이드에 사용할 새 저장소를 구성 합니다.

1. 공용 저장소 GPG 키를 가져옵니다.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 사용자가 선택한 저장소를 구성 하려면 다음 명령 중 하나를 사용 합니다.

   | 리포지토리 | Command |
   |---|---|
   | **CU** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 실행 **apt get 업데이트**합니다.

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>다음 단계

으로 이동 하려면 올바른 저장소를 구성 하 고 나면 [설치](sql-server-linux-setup.md#platforms) 또는 [업데이트](sql-server-linux-setup.md#upgrade) 새 저장소에서 SQL Server 및 모든 관련 패키지 합니다.

> [!IMPORTANT]
> 와 같은 설치 문서 중 하나를 사용 하기로 선택한 경우이 시점에서 [퀵 스타트](sql-server-linux-setup.md#platforms), 대상 저장소 이미 구성 되었다는 기억 합니다. 이 자습서에서 해당 단계를 반복 하지 않습니다. 퀵 스타트 CU 리포지토리를 사용 하기 때문에 이것이 GDR 저장소를 구성 하는 경우에 특히 그렇습니다.

SQL Server 2017 Linux를 설치 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md)합니다.
