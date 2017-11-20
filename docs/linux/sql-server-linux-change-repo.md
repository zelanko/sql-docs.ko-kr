---
title: "등록은 Linux에서 SQL Server에 대 한 일반 공급 리포지토리 | Microsoft Docs"
description: "Linux의 GA (일반 공급) 저장소에 SQL Server 2017 미리 보기 저장소에서 리포지토리를 변경 (GA는 또한 라고도 RTM)."
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: a0d6ff0a983f1d1d1ad8fdcc7de37d9a06032025
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="change-repositories-from-the-preview-repository-to-the-ga-repository"></a>GA 저장소에 미리 보기 저장소에서 저장소 변경

SQL Server 2017 CTP 2.1, RC1, 또는 r c 2에서 GA (일반 공급) 릴리스 버전으로 업그레이드 하면 저장소를 전환 해야 합니다. 다음 섹션에서는 선택한 리포지토리와 업그레이드 하기 전에 변경 작업을 수행 하는 방법에 설명 합니다.

## <a name="repository-choices"></a>리포지토리 선택

같은 두 가지 유형의 각 배포에 대 한 저장소는을 고려해 야 합니다.

  > [!IMPORTANT]
  > CTP 2.1 이전의 모든 버전 2.1 이상 ga에 있습니다. 업그레이드 하기 전에 업그레이드 해야 합니다.

- **CU (누적 업데이트)**: The CU (누적 업데이트) 저장소 해당 릴리스 이후 기본 SQL Server 릴리스 및 버그 수정 또는 향상 된 기능에 대 한 패키지를 포함 합니다. 누적 업데이트는 SQL Server 2017 등의 릴리스 버전에 고유 합니다. 일반 주기로 릴리스되는 합니다.

- **GDR**: The GDR 리포지토리 해당 릴리스 이후는 기본 SQL Server 릴리스만 주요 수정 프로그램 및 보안 업데이트에 대 한 패키지를 포함 합니다. 이러한 업데이트는 다음 CU 릴리스로 추가 됩니다.

각 CU 및 GDR 릴리스에 전체 SQL Server 패키지 및 해당 저장소에 대 한 모든 이전 업데이트를 포함합니다. CU 릴리스에 GDR 릴리스의 업데이트는 SQL Server에 대 한 구성된 저장소를 변경 하 여 지원 됩니다. 수도 있습니다 [다운 그레이드](sql-server-linux-setup.md#rollback) 주요 버전 내에서 모든 릴리스를 (예: 2017).

> [!NOTE]
> CU GDR 릴리스에서 업데이트할 있습니다 저장소를 변경 하 여 언제 든 지 해제 합니다. 업데이트 CU에서 릴리스를 GDR 릴리스 지원 되지 않습니다. 

## <a name="change-to-a-ga-repository"></a>GA 리포지토리에 변경

미리 보기 리포지토리에서 (CU 또는 GDR)에 하나의 소스 리포지토리를 변경 하려면 다음 단계를 사용 합니다.

1. 미리 보기 이전에 구성 된 저장소를 제거 합니다.

   | 플랫폼 | 저장소 제거 명령 |
   |-----|-----|
   | RHEL | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | Ubuntu | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |

1. 에 대 한 **Ubuntu만**, 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 새 저장소를 구성 합니다.

   | 플랫폼 | 리포지토리 | Command |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [설치](sql-server-linux-setup.md#platforms) 또는 [업데이트](sql-server-linux-setup.md#upgrade) GA 저장소를 사용 하 여 SQL Server.

   > [!IMPORTANT]
   > 사용 하 여 전체 설치를 수행 하도록 선택한 경우이 시점에서 [빠른 시작 자습서](#platforms), 대상 저장소 방금 구성한 기억 합니다. 이 자습서에서 해당 단계를 반복 하지 않습니다. 이 빠른 시작 자습서 CU 리포지토리를 사용 하기 때문에 GDR 저장소를 구성 하는 경우에 특히 그렇습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 2017 Linux를 설치 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md)합니다.

