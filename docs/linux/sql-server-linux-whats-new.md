---
title: "SQL Server 2017 linux에 대 한 새로운 기능 | Microsoft Docs"
description: "이 항목에 대 한 SQL Server 2017 Linux에서 새로운 강조 표시 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 11/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.workload: On Demand
ms.openlocfilehash: 3e4a3e19fd9d03d3f6e4dd4a68a5a15b922f348d
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>SQL Server 2017 linux에 대 한 새로운 기능

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 문서에서는 SQL Server 2017 Linux에서 실행 중인에 대 한 주요 기능 및 서비스를 사용할 수 있는 설명입니다.

> [!NOTE]
> 이 문서에서 이러한 기능을 외에도 누적 업데이트는 GA 릴리스에서 정기적으로 해제 됩니다. 이러한 누적 업데이트는 다양한 향상된 기능 및 수정 사항을 제공합니다. 최신 CU 릴리스에 대 한 자세한 내용은 참조 하십시오. [http://aka.ms/sql2017cu](http://aka.ms/sql2017cu)합니다. 패키지 다운로드 및 알려진된 문제에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

## <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진

- 핵심 SQL Server 데이터베이스 엔진 기능을 사용할 수 있습니다.
- 기본 Linux 경로 대 한 지원입니다.
- IPV6 지원 합니다.
- NFS에 데이터베이스 파일을 지원 합니다.
- 활성화 [계층 보안 투명](sql-server-linux-encrypted-connections.md) (TLS) 암호화 합니다.
- 활성화 [Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.
- [가용성 그룹 기능이](sql-server-linux-availability-group-overview.md) 고가용성에 대 한 합니다.
- [전체 텍스트 검색](sql-server-linux-setup-full-text-search.md) 지원 합니다.

## <a name="sql-server-agent"></a>SQL Server 에이전트

- 활성화 [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md) 다음과 같은 작업에 대 한 지원:
  - [Transact SQL 작업](sql-server-linux-run-sql-server-agent-job.md)
  - [DB 메일](sql-server-linux-db-mail-sql-agent.md)
  - [로그 전달](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)

- Linux에서 SSIS 패키지를 실행할 수 있습니다. 자세한 내용은 참조 [ssis conf와 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)합니다.

## <a name="other-improvements"></a>기타 개선 기능

- 명령줄 구성 도구, [mssql conf](sql-server-linux-configure-mssql-conf.md)합니다.
- 사용 하 여 무인된 설치 지원을 [환경 변수](sql-server-linux-configure-environment-variables.md)합니다.
- 플랫폼 간 [Visual Studio Code mssql 서버 확장](sql-server-linux-develop-use-vscode.md)합니다.
- 플랫폼 간 스크립트 생성기 [mssql scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)합니다.
- 플랫폼 간 동적 관리 뷰 (DMV) 모니터 [DBFS 도구](https://github.com/Microsoft/dbfs)합니다.

## <a name="next-steps"></a>다음 단계

Linux에서 SQL Server를 설치 하려면 다음 자습서 중 하나를 사용 합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-docker.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

Linux에서 SQL Server에 대 한 다른 정보에 대 한 참조는 [개요](sql-server-linux-overview.md)합니다. 패키지 다운로드 및 지원 되지 않는 기능 및 알려진된 문제 목록에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

SQL Server 2017에 도입 된 기타 개선 기능, 참조 [What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)합니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
