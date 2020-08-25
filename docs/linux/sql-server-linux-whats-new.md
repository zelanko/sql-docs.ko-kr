---
title: SQL Server 2017 on Linux의 새로운 기능
description: 이 문서에서는 Linux에서 실행되는 SQL Server 2017에 사용할 수 있는 주요 기능 및 서비스에 대해 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 489b2bda31554766a874fb7d09d259fbc96a3398
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088747"
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>SQL Server 2017 on Linux의 새로운 기능

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux에서 실행되는 SQL Server 2017에 사용할 수 있는 주요 기능 및 서비스에 대해 설명합니다.

> [!NOTE]
> 이 문서의 이러한 기능 외에도 누적 업데이트가 정기적으로 릴리스됩니다. 이러한 누적 업데이트는 다양한 향상된 기능 및 수정 사항을 제공합니다. 최신 CU 릴리스에 대한 자세한 내용은 [https://aka.ms/sql2017cu](https://aka.ms/sql2017cu)를 참조하세요. 패키지 다운로드 및 알려진 문제에 대해서는 [릴리스 정보](sql-server-linux-release-notes.md)를 참조하세요.

## <a name="ubuntu-1804-supported"></a>Ubuntu 18.04 지원됨

SQL Server 2017 CU20부터 Ubuntu 18.04가 지원됩니다. [Ubuntu에 SQL Server를 설치하고 데이터베이스를 만드는 방법](quickstart-install-connect-ubuntu.md?view=sql-server-2017)에 대한 빠른 시작을 확인합니다.

## <a name="rhel-8-supported"></a>RHEL 8 지원됨

SQL Server 2017 CU20부터 RHEL 8이 지원됩니다. [Red Hat에 SQL Server를 설치하고 데이터베이스를 만드는 방법](quickstart-install-connect-red-hat.md?view=sql-server-2017)에 대한 빠른 시작을 확인합니다.

## <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진

- 핵심 SQL Server 데이터베이스 엔진 기능 사용.
- 네이티브 Linux 경로 지원.
- IPV6 지원.
- NFS에서 데이터베이스 파일 지원.
- TLS([전송 계층 보안](sql-server-linux-encrypted-connections.md)) 암호화 사용.
- [Active Directory 인증](sql-server-linux-active-directory-authentication.md) 사용.
- 고가용성을 위한 [가용성 그룹 기능](sql-server-linux-availability-group-overview.md).
- [전체 텍스트 검색](sql-server-linux-setup-full-text-search.md) 지원.

## <a name="sql-server-agent"></a>SQL Server 에이전트

- 다음 작업에 대해 [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md) 지원 사용:
  - [Transact-SQL 작업](sql-server-linux-run-sql-server-agent-job.md)
  - [DB 메일](sql-server-linux-db-mail-sql-agent.md)
  - [로그 전달](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)

- Linux에서 SSIS 패키지를 실행하는 기능. 자세한 내용은 [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)을 참조하세요.

## <a name="other-improvements"></a>기타 개선 사항

- 명령줄 구성 도구인 [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- [환경 변수](sql-server-linux-configure-environment-variables.md)를 사용한 무인 설치 지원.
- 플랫폼 간 [Visual Studio Code mssql-server 확장](sql-server-linux-develop-use-vscode.md).
- 플랫폼 간 스크립트 생성기인 [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- 플랫폼 간 DMV(동적 관리 뷰) 모니터인 [DBFS 도구](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>다음 단계

SQL Server on Linux를 설치하려면 다음 자습서 중 하나를 사용합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요. SQL Server 2017에 도입된 다른 향상된 기능을 보려면 [SQL Server 2017의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)을 참조하세요.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
