---
title: SQL Server on Linux FAQ | Microsoft Docs
description: 이 문서에서는 Linux에서 실행 되는 SQL Server에 대 한 질문과 대답을 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 448db7c77d26e06651e01a7e790917757aff0e9d
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713605"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Linux의 SQL Server에는 질문과 대답 (FAQ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 섹션에서는 일반적인 질문 및 답변 SQL Server에 대 한 Linux를 실행 합니다.

## <a name="general-questions"></a>일반적인 질문

1. **Linux 플랫폼 지원 되나요?**

   SQL Server는 현재 Red Hat Enterprise Server, SUSE Linux Enterprise Server 및 Ubuntu에서 지원 됩니다. Docker 컨테이너에서 실행도 지원 합니다. 지원 되는 버전에 대 한 최신 정보를 참조 하세요 [지원 되는 플랫폼](sql-server-linux-setup.md#supportedplatforms)합니다.

1. **Linux의 SQL Server는 다른 플랫폼에서 작동**?

   SQL Server는 테스트 하 고 앞에 나열 된 배포에 대 한 Linux 지원 합니다. 다른 Linux 배포판 밀접 한 관련이 및 SQL Server를 실행 하는 일을 할 수 있습니다 (예를 들어 CentOS는 밀접 하 Red Hat Enterprise Server). 지원 되지 않는 운영 체제에서 SQL Server를 설치 하려는 경우 살펴보시기 하지만 **지원 정책** 섹션을 [Microsoft SQL Server에 대 한 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) 지원 이해 영향을 줍니다. 일부 커뮤니티에서 유지 관리 되며 Linux 배포판에 정식 기본 운영 체제 문제 이면 지원을 받을 수 없는 note도 합니다.

1. **Linux에서 라이선스 작업 어떻게 하나요?**

   SQL Server는 Windows 및 Linux 모두에 대해 동일한 방식으로 허가 되어 있습니다. 사실, SQL Server의 라이선스 수 및 다음 원하는 플랫폼에서 해당 라이선스를 사용 하도록 선택할 수 있습니다. 자세한 내용은 [SQL Server 라이선스 방법](https://www.microsoft.com/sql-server/sql-server-2017-pricing)합니다.

1. **Windows에서와 같은 Linux의 SQL Server를 입니까?**

   SQL Server 용 데이터베이스 엔진의 핵심 이므로 Windows에서 Linux에서 동일 합니다. 그러나 일부 기능은 현재 사용할 수 없습니다 linux. Linux에서 지원 되지 않는 기능의 목록을 보려면 참조는 [기능 및 서비스를 지원 되지 않는](sql-server-linux-release-notes.md#Unsupported)합니다. 또한 검토 해야 합니다 [알려진 문제](sql-server-linux-release-notes.md#known-issues)합니다. 이러한 목록에 지정 되지 않으면 다른 SQL Server 기능 및 서비스는 Linux에서 지원 됩니다.

1. **SQL Server에 대 한 지원 정책은 무엇 인가요?**

   지원 정책을 이해 하려면 다음을 검토 합니다 [SQL Server에 대 한 기술 지원 정책을](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)합니다.

1. **Windows SQL Server에서 어. 리소스 Linux에서 SQL Server를 사용 하는 방법을 알아볼 수 있습니까?**

   합니다 [퀵 스타트](sql-server-linux-setup.md#platforms) Linux에서 SQL Server를 설치 하 고 TRANSACT-SQL 쿼리를 실행 하는 방법에 대 한 단계별 지침을 제공 합니다. 다른 자습서는 Linux에서 SQL Server를 사용 하 여 추가 지침을 제공 합니다. 제 3 자 목록은 팁을 참조 하세요.를 [SQL Server Linux 팁에서 동료 목록](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)합니다.

## <a name="installation"></a>설치

1. **내 Linux 서버에 설치 된 SQL Server는 어떻게 받나요?**

   Microsoft SQL Server 설치를 위한 패키지 리포지토리를 유지 관리 및 yum, zypper와 같은 네이티브 패키지 관리자를 통해 설치를 지 원하는 아파트 및 스위트룸 합니다. 신속 하 게 설치 하려면 중 하나를 참조 합니다 [퀵 스타트](sql-server-linux-setup.md#platforms)합니다.

1. **Windows 10에 대 한 Linux 하위 시스템에서 SQL Server를 설치할 수 있습니까?**

   아니요. Windows 10에서 실행 되는 Linux 아니며 현재 SQL Server 및 관련된 도구에 대 한 지원 되는 플랫폼

1. **데이터 파일에 대 한 SQL Server에서 사용할 수 있는 Linux 파일 시스템?**

   현재 SQL Server on Linux ext4 및 XFS 지원합니다. 나중에 필요에 따라 다른 파일 시스템에 대 한 지원이 추가 됩니다.

1. **SQL Server를 오프 라인으로 설치 하려면 설치 패키지를 다운로드할 수 있습니까?**

   예 자세한 내용은 다운로드 링크에서 패키지 참조를 [릴리스](sql-server-linux-release-notes.md)합니다. 또한 검토 합니다 [오프 라인 설치에 대 한 지침](sql-server-linux-setup.md#offline)합니다.

1. **Linux의 SQL Server의 무인된 설치를 수행할 수 있습니까?**

   예 무인된 설치의 논의 참조 하세요 [Linux의 SQL Server에 대 한 설치 지침은](sql-server-linux-setup.md#unattended)합니다. 에 대 한 샘플 스크립트를 참조 하세요 [Red Hat](sample-unattended-install-redhat.md)를 [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), 및 [Ubuntu](sample-unattended-install-ubuntu.md)합니다. 또한 검토할 수 있습니다 [이 샘플 스크립트](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) SQL Server 고객 자문 팀에서 만든 합니다.

## <a name="tools"></a>Tools

1. **사용할 수 있습니까 SQL Server Management Studio 클라이언트 Windows에서 Linux의 SQL Server에 액세스 하려면?**

   예, Linux의 SQL Server에 액세스 하는 Windows에서 실행 되는 모든 기존 도구를 사용할 수 있습니다. 여기에 microsoft SQL Server Management Studio (SSMS), SQL Server 데이터 도구 (SSDT) 및 OS와 같은 도구 및 타사 도구 포함 됩니다.

1. **Linux에서 실행 되는 SSMS와 같은 도구는 있나요?**

   새 Azure Data Studio (미리 보기)는 SQL Server를 관리 하기 위한 플랫폼 간 도구입니다. 자세한 내용은 [Azure Data Studio (미리 보기) 이란](../azure-data-studio/what-is.md)합니다.

1. **Linux에서 사용할 수 있는 sqlcmd 및 bcp와 같은 명령을?합니다**

   예, [sqlcmd 및 bcp](sql-server-linux-setup-tools.md) Linux, macOS 및 Windows에서 기본적으로 사용할 수 있습니다. 또한 사용 하는 새 [mssql scripter](https://github.com/Microsoft/mssql-scripter) 어디를 실행 하 여 SQL database에 대 한 T-SQL 스크립트를 생성 하도록 하는 Linux, macOS 또는 Windows에서 명령줄 도구입니다. 참고: 미리 보기 릴리스 [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)합니다.

1. **Linux에서 실행 중인 인스턴스에 대 한 Windows의 SSMS를 통해 연결 되어 있을 때 작업 모니터를 볼 수 있습니까?**

   예, Windows에서 SSMS를 사용 하 여 원격으로 연결할 수 있습니다 하 고 사용 하 여 도구 / 등의 기능이 Linux 인스턴스에서 작업 모니터 명령으로 합니다.

1. **Linux에서 SQL Server 성능 모니터링을 사용할 수 있는 도구?**

   사용할 수 있습니다 [시스템 동적 관리 뷰 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 를 다양 한 유형의 SQL Server, Linux 프로세스 정보를 포함 하는 방법에 대 한 정보를 수집 합니다. 사용할 수 있습니다 [쿼리 저장소](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) 쿼리 성능을 향상 시킵니다. 기본 제공 같은 다른 도구를 [성능 대시보드](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)원격에서 SSMS SQL Server Management Studio () Windows에서 작동 합니다.

   > [!TIP]
   > 성능 향상을 위해 한 가지 방법은 제대로 Linux 운영 체제 및 SQL Server insance를 구성 하는 것입니다. 자세한 내용은 [성능 모범 사례 및 Linux의 SQL Server에 대 한 구성 지침](sql-server-linux-performance-best-practices.md)합니다.

## <a name="administration"></a>관리

1. **Microsoft가 Linux에서 SQL Server 구성 관리자와 같은 앱을 만들고?**

   예는 Linux의 SQL Server에 대 한 구성 도구: [mssql conf](sql-server-linux-configure-mssql-conf.md)합니다.

1. **Linux의 SQL Server 같은 호스트의 여러 인스턴스를 지원 합니까?**

   여러 고유 인스턴스를 호스트에서 여러 컨테이너를 실행 하는 것이 좋습니다. 각 컨테이너는 다른 포트에서 수신 대기 해야 합니다. 자세한 내용은 [여러 SQL Server 컨테이너를 실행할](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)합니다.

1. **Active Directory 인증이 Linux에서 지원 되나요?**

   예 자세한 내용은 [Linux의 SQL Server를 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.

1. **Linux에서 지원 되는 클러스터링 및 Always On 인가요?**

   장애 조치 클러스터링 및 고가용성 on Linux: Linux의 Pacemaker를 사용 하 여 수행 됩니다. 자세한 내용은 [비즈니스 연속성 및 데이터베이스 복구-SQL Server on Linux](sql-server-linux-business-continuity-dr.md)합니다.

1. **Windows로 또는 그 반대로 Linux에서 복제를 구성할 수는?**

   읽기-배율 복제본 단방향 데이터 복제에 대 한 Windows 및 Linux 간에 사용할 수 있습니다.

1. **Linux에서 Windows 이전 버전의 SQL Server의 기존 데이터베이스를 마이그레이션할 수는?**

   예, 가지 [여러 가지 방법을](sql-server-linux-migrate-overview.md) 이 달성 하는 합니다.

1. **마이그레이션할 수 데이터를 Oracle 및 기타 데이터베이스 엔진에서 Linux의 SQL server?**

   예 SSMA에서 여러 유형의 데이터베이스 엔진 마이그레이션 지원: Microsoft Access, DB2, MySQL, Oracle 및 SAP ASE (이전의 SAP Sybase ASE). SSMA를 사용 하는 방법의 예제를 참조 하세요 [Oracle 스키마를 SQL Server Migration Assistant를 사용 하 여 Linux에서 SQL Server로 마이그레이션할](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)합니다.

1. **SQL Server 파일에 필요한 권한은 무엇입니까?**

   모든 파일을 `/var/opt/mssql` 파일 폴더에서 소유 해야 합니다 **mssql** 사용자에 속할를 **mssql** 그룹. 모두를 **mssql** 사용자 및 그룹에는 모든 파일 및 디렉터리 읽기 / 쓰기 권한이 있어야 합니다. 파일 및 디렉터리 사용 권한을 포함 하는 다음과 같은 특별 한 시나리오를 note:

   * Mssql 소유자 및 그룹 권한은 SQL Server 파일을 저장 하는 데 사용 되는 탑재 된 네트워크 공유에 대 한 필요 합니다.
   * 데이터베이스 파일 또는 백업을 기본이 아닌 디렉터리를 찾을 경우 해당 디렉터리에 대 한 권한을 설정 해야 합니다.
   * 기본 루트 umask 0022를 변경 하면 설치 후 SQL Server 구성이 실패 합니다. 그런 다음 SQL Server 시작 계정에 필요한 권한의 수동으로 적용 해야 합니다.

1. **설치 된 mssql 계정 및 그룹에서 SQL Server 파일 및 디렉터리의 소유권을 변경할 수 있나요?**

   기본 설치에서 SQL Server 디렉터리 및 파일의 소유권을 변경 지원 하지 않습니다. Mssql 계정 및 그룹 SQL Server에 대 한 구체적으로 대화형 로그인 권한이 없습니다.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
