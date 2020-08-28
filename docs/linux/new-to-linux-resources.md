---
title: Linux를 처음 사용하는 SQL 사용자를 위한 리소스
titleSuffix: SQL Server
description: Linux를 처음 사용하는 SQL Server 사용자를 위한 리소스 및 참고 자료입니다.
author: VanMSFT
ms.author: vanto
ms.date: 08/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 789178113f1e22df2d2cf028d2f6e5f93e9b5b0e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646823"
---
# <a name="new-to-linux-resources-for-sql-users"></a>Linux를 처음 사용하는 SQL 사용자를 위한 리소스

이 문서는 Linux 개념 소개를 통해 학습 경로를 제공합니다. 이 문서의 섹션을 단계별 학습 경로로 사용하여 Linux 환경에 익숙해질 수 있습니다.

여기에서는 종합적인 목록이 아니라 SQL Server on Linux 환경을 관리하고 탐색하는 데 필요한 최소한의 정보를 제공합니다. 자세한 내용은 [자습서 전체 목록](https://www.linux.org/forums/linux-beginner-tutorials.123/)을 참조하세요. 

## <a name="what-is-linux"></a>Linux란?

[What is Linux](https://www.linux.org/threads/what-is-linux.4106/)(Linux란?) 모듈에서는 Linux 운영 체제의 역사를 소개합니다. 이 모듈은 *커널*과 오늘날 Linux의 평판을 설명합니다. 이 자습서는 Linux를 소개하며 사용자가 시작하는 데 도움이 됩니다. 

## <a name="select-a-distribution"></a>배포 선택

Linux의 역사를 알고난 후에는 비즈니스 요구 사항에 가장 적합한 [Linux 배포](https://www.linux.org/threads/selecting-a-linux-distribution.4117/)를 선택합니다. RHEL(RedHat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 및 Ubuntu와 같은 다양한 배포에서 [SQL Server가 지원](sql-server-linux-release-notes-2019.md#supported-platforms)됩니다.


## <a name="get-around-directories"></a>디렉터리 파악

적절한 Linux 배포를 선택한 다음에는 [Linux 디렉터리를 충분히 파악](https://www.linux.org/threads/getting-around-in-linux-directories.4120/)해야 합니다.

이 모듈을 학습하면 다음 질문에 답할 수 있습니다.

- 파일 간 이동하는 방법 
- 디렉터리에서 파일을 파악하는 방법
- 다른 디렉터리 파악 


## <a name="install-new-software"></a>새 소프트웨어 설치 

다음으로, 새로운 Linux 운영 체제에 [새 소프트웨어를 설치](https://www.linux.org/threads/installing-new-software-debian-red-hat-slackware.4119/)하는 방법을 학습합니다. 이 모듈에서는 Debian 및 Red Hat Linux 운영 체제에 새 소프트웨어를 설치하는 방법을 자세히 설명합니다. 


## <a name="root-versus-system-user"></a>루트 사용자와 시스템 사용자 비교

사용자 권한 및 [루트 사용자와 시스템 사용자](https://www.linux.org/threads/when-to-work-as-root-when-to-work-as-a-system-user.4136/)의 차이점을 파악합니다. 이 모듈을 학습하면 시나리오에 따라 어떤 사용자 권한이 적합한지 결정할 수 있습니다. 

## <a name="file-system-and-permissions"></a>파일 시스템 및 권한

Linux의 다양한 사용자 및 그룹에 익숙해지면 [chown(소유권 변경)](https://www.linux.org/threads/file-permisions-chown.4125/) 및 [chmod(권한 변경)](https://www.linux.org/threads/file-permissions-chmod.4124) 명령을 사용하여 Linux 운영 체제의 다양한 파일에 대한 소유권 및 파일 권한을 변경하는 방법을 학습합니다. 


## <a name="commands-for-system-administration"></a>시스템 관리 명령

시스템 관리자가 Linux 운영 체제를 제어하는 데 [자주 사용하는 명령](https://www.linux.org/threads/commands-for-system-administration.4126/)을 숙지합니다. 이러한 명령에는 `df`, `du`, `TOP`, `ps`, `mkdir`, `rmdir`, `rm` 및 `mv` 등이 있습니다. 


## <a name="next-steps"></a>다음 단계

Linux 환경에 익숙해지면 SQL Server on Linux의 [버전 및 구성 요소](sql-server-linux-editions-and-components-2019.md)와 [지원되는 Linux 플랫폼](sql-server-linux-release-notes-2019.md)을 검토합니다. 

자세한 내용은 [기타 Linux 자습서](https://www.linux.org/forums/linux-beginner-tutorials.123/) 및 [자주 묻는 질문](sql-server-linux-faq.md)을 참조하세요.
