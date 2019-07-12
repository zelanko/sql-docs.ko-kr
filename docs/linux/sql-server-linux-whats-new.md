---
title: Linux의 SQL Server 2017의 새로운 기능
description: 이 문서에서는 Linux의 SQL Server 2017의 새로운 기능을 강조 합니다.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: 3852a4b29cab1b0fe8ab44a4b65fc344f6adfb49
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834646"
---
# <a name="whats-new-for-sql-server-on-linux"></a>Linux의 SQL Server의 새로운 기능

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 실행되는 SQL Server 2017에 대한 주요 기능 및 사용 가능한 서비스를 설명합니다.

SQL Server 2019 preview가 출시되었습니다. 이 문서에서는 SQL Server 2019 미리 보기 릴리스를 다루지 않습니다. SQL Server 2019 미리 보기를 알아보려면 [Linux 용 SQL Server 2019 미리 보기의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)을 참조하세요.

> [!NOTE]
> 이 문서에서의 이러한 기능 외에도, 누적 업데이트는 GA 릴리스 이후 정기적으로 배포됩니다. 이러한 누적 업데이트는 다양한 향상된 기능 및 수정 사항을 제공합니다. 최신 CU 릴리스에 대한 자세한 내용은 [ https://aka.ms/sql2017cu ](https://aka.ms/sql2017cu)를 참조하세요. 패키지 다운로드 및 알려진  문제는 [릴리스 노트](sql-server-linux-release-notes.md)를 참조하세요.

## <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진

- 핵심 SQL Server 데이터베이스 엔진 기능을 사용할 수 있습니다.
- 네이티브 Linux 경로 대 한 지원입니다.
- IPV6 지원 합니다.
- NFS의 데이터베이스 파일을 지원 합니다.
- 사용 하도록 설정 [Transport Layer Security](sql-server-linux-encrypted-connections.md) (TLS) 암호화 합니다.
- [Active Directory 인증](sql-server-linux-active-directory-authentication.md)을 사용할 수 있습니다.
- 고가용성을 위한 [가용성 그룹 기능](sql-server-linux-availability-group-overview.md)
- [전체 텍스트 검색](sql-server-linux-setup-full-text-search.md)을 지원합니다.

## <a name="sql-server-agent"></a>SQL Server 에이전트

- [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md)가 다음과 같은 작업을 사용할 수 있도록 지원:
  - [TRANSACT-SQL 작업](sql-server-linux-run-sql-server-agent-job.md)
  - [DB 메일](sql-server-linux-db-mail-sql-agent.md)
  - [로그 전달](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)

- Linux에서 SSIS 패키지를 실행할 수 있습니다. 자세한 내용은 [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

## <a name="other-improvements"></a>기타 향상 된 기능

- 명령줄 구성 도구, [mssql conf](sql-server-linux-configure-mssql-conf.md)
- [환경 변수](sql-server-linux-configure-environment-variables.md)를 사용한 무인된 설치 지원
- 크로스 플랫폼 [Visual Studio Code-mssql server 확장](sql-server-linux-develop-use-vscode.md)
- 크로스 플랫폼 스크립트 생성기, [mssql scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)
- 크로스 플랫폼 동적 관리 뷰(DMV) 모니터, [DBFS 도구](https://github.com/Microsoft/dbfs)

## <a name="next-steps"></a>다음 단계

Linux의 SQL Server를 설치하려면 다음 자습서 중 하나를 사용합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

SQL Server 2017에 도입된 다른 개선 사항은 [What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)을 참조하세요.

> [!TIP]
> 자주 묻는 질문에 대한 답변은, [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
