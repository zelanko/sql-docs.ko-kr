---
title: SQL Server linux FAQ | Microsoft Docs
description: 이 문서 Linux에서 실행 중인 SQL Server에 대 한 질문과 대답을 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 608a59138f86cf68a9e8311a4c082b15f1179ba5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Linux에서 SQL Server가 질문과 대답 (FAQ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 섹션에서는 일반적인 질문 및 답변 SQL Server에 대 한 Linux에서 실행 합니다.

## <a name="general-questions"></a>일반적인 질문

1. **Linux 플랫폼 지원 되나요?**

   SQL Server는 현재 Red Hat Enterprise Server, SUSE Linux Enterprise Server 및 Ubuntu에서 지원 됩니다. Docker가 있는 컨테이너의 실행도 지원 합니다. 지원 되는 버전에 대 한 최신 정보를 참조 하십시오. [지원 되는 플랫폼](sql-server-linux-setup.md#supportedplatforms)합니다.

1. **다른 플랫폼에서 사용할 수 Linux에서 SQL Server**?

   SQL Server는 테스트 하 고 앞에서 나열 된 분포에 대 한 Linux에서 지원 합니다. 다른 Linux 배포판 밀접 한 관련이 및 SQL Server를 실행할 수 있습니다 (예를 들어 CentOS는 밀접 한 관련이 Red Hat Enterprise Server). 하지만 지원 되지 않는 운영 체제에서 SQL Server를 설치 하기로 선택한 경우을 검토 하십시오는 **지원 정책** 섹션은 [Microsoft SQL Server에 대 한 기술 지원 정책을](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) 지원을 이해 하려면 영향을 줍니다. 또한 일부 커뮤니티-유지 관리 되도록 Linux 배포판 정식 기본 운영 체제 문제 이면 지원을 받을 수 없는 note 합니다.

1. **Linux에서 지원 되는 SQL Server 기능**

   전체 목록은 지원 되는 기능 및 알려진된 문제를 참조 하십시오.는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

1. **SQL Server에 대 한 지원 정책 이란?**

   지원 정책을 이해 하려면 검토는 [SQL Server에 대 한 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)합니다.

1. **SQL Server Windows 배경에서 어 있습니다. Linux에서 SQL Server를 사용 하는 방법을 알아보려면 도움이 되는 리소스 있습니까?**

   [퀵 스타트](sql-server-linux-setup.md#platforms) Linux에서 SQL Server를 설치 하 고 TRANSACT-SQL 쿼리를 실행 하는 방법에 대 한 단계별 지침을 제공 합니다. 다른 자습서는 SQL Server를 사용 하 여 linux에서 추가 지침을 제공 합니다. 팁의 공급 업체 목록에 대 한 참조는 [Linux 팁에서 SQL Server의 MSSQLTIPS 목록](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)합니다.

## <a name="installation"></a>설치

1. **내 Linux 서버에 설치 된 SQL Server 어떻게 합니까?**

   Microsoft SQL Server 설치를 위한 패키지 저장소를 유지 관리 하 고 yum, zypper, 같은 기본 패키지 관리자를 통해 설치를 지 원하는 아파트 및 스위트룸 합니다. 빠르게 설치 중 하나를 참조는 [퀵 스타트](sql-server-linux-setup.md#platforms)합니다.

1. **Windows 10에 대 한 Linux 하위 시스템에서 SQL Server를 설치할 수 있습니까?**

   아니요. Windows 10에서 실행 되는 Linux는 현재 SQL Server 및 관련된 도구에 대 한 지원 되는 플랫폼이 없습니다.

1. **데이터 파일에 대 한 SQL Server 2017를 사용할 수 있는 Linux 파일 시스템?**

   현재 Linux에서 SQL Server ext4 및 XFS 지원합니다. 나중에 필요에 따라 다른 파일 시스템에 대 한 지원이 추가 됩니다.

1. **SQL Server를 설치 오프 라인 설치 패키지를 다운로드할 수 있나요?**

   예 자세한 내용은 참조 링크에서 다운로드 패키지는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 또한 검토는 [오프 라인 설치에 대 한 지침](sql-server-linux-setup.md#offline)합니다.

1. **Linux에서 SQL Server의 무인된 설치를 수행할 수 있습니까?**

   예 무인된 설치의 논의 알려면 [Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md#unattended)합니다. 예제 스크립트에 대 한 참조 [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), 및 [Ubuntu](sample-unattended-install-ubuntu.md)합니다. 또한 검토할 수 있습니다 [이 샘플 스크립트](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) SQL Server 고객 자문 팀으로 생성 합니다.

## <a name="tools"></a>Tools

1. **사용할 수 있습니까 SQL Server Management Studio 클라이언트 Windows Linux에서 SQL Server에 액세스?**

   예, Linux에서 SQL Server에 액세스 하는 Windows에서 실행 하는 모든 기존 도구를 사용할 수 있습니다. 여기에 Microsoft SQL Server Management Studio (SSMS), SQL Server 데이터 도구 (SSDT), OSS 등의 도구 및 타사 도구 포함 됩니다.

1. **Linux에서 실행 되는 SSMS와 같은 도구를 거기?**

   새 Microsoft SQL Operations Studio (preview) 는 SQL Server를 관리 하기 위한 플랫폼 간 도구입니다. 자세한 내용은 참조 [Microsoft SQL 작업 Studio (미리 보기) 이란](../sql-operations-studio/what-is.md)합니다.

1. **Sqlcmd 및 bcp와 같은 명령은 Linux에서 사용할 수 있습니까?**

   예, [sqlcmd 및 bcp](sql-server-linux-setup-tools.md) Linux, macOS 등 및 Windows에서 기본적으로 사용할 수 있습니다. 또한 사용 하는 새 [mssql scripter](https://github.com/Microsoft/mssql-scripter) 곳에서 실행 되는 SQL 데이터베이스에 대 한 T-SQL 스크립트를 생성 하기 위해 Linux, macOS 등 또는 Windows 명령줄 도구입니다. 참고: 미리 보기에 대 한 릴리스 [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)합니다.

1. **Linux에서 실행 인스턴스에 대 한 Windows에서 SSMS를 통해 연결 되어 있을 때 작업 모니터를 볼 수 있습니까?**

   예, Windows에서 SSMS를 사용 하 여 원격으로 연결할 수 있습니다 및 도구 / 같은 기능을 사용 하 여 Linux 인스턴스에서 작업 모니터 명령으로 합니다.

1. **도구는 Linux에서 SQL Server 성능 모니터링을 사용할 수 있습니까?**

   사용할 수 있습니다 [시스템 동적 관리 뷰 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 를 다양 한 유형의 SQL Server, Linux 프로세스 정보를 포함 하는 방법에 대 한 정보를 수집 합니다. 사용할 수 있습니다 [쿼리 저장소](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) 쿼리 성능을 향상 시키기 합니다. 기본 제공 같은 다른 도구를 [성능 대시보드](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/), 원격으로 SQL Server Management Studio (SSMS)에서 Windows에서 작업 합니다.

## <a name="administration"></a>관리

1. **가 Microsoft SQL Server 구성 관리자와 같은 앱 Linux에서 만든?**

   예, Linux에서 SQL Server에 대 한 구성 도구는: [mssql conf](sql-server-linux-configure-mssql-conf.md)합니다.

1. **Linux에서 SQL Server는 동일한 호스트에 여러 인스턴스를 지원 합니까?**

   여러 가지 인스턴스를 호스트에서 여러 컨테이너를 실행 하는 것이 좋습니다. 각 컨테이너는 다른 포트에서 수신 대기 해야 합니다. 자세한 내용은 참조 [여러 SQL Server 컨테이너 실행](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)합니다.

1. **Active Directory 인증은 Linux에서 지원 되나요?**

   예 자세한 내용은 참조 [Linux에서 SQL Server와 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.

1. **Always On 및 클러스터링 Linux에서 지원?**

   장애 조치 클러스터링 및 고가용성 Linux에서 linux Pacemaker를 만족할 됩니다. 자세한 내용은 참조 [비즈니스 연속성 및 데이터베이스 복구-Linux에서 SQL Server](sql-server-linux-business-continuity-dr.md)합니다.

1. **이것이 가능 Windows로 그리고 반대로 Linux에서 복제를 구성 할까요?**

   읽기 확장성이 복제본 단방향 데이터 복제에 대 한 Windows 및 Linux 사용할 수 있습니다.

1. **Linux를 Windows에서 이전 버전의 SQL Server의 기존 데이터베이스를 마이그레이션할 수는?**

   예, [여러 가지 방법을](sql-server-linux-migrate-overview.md) 이 수행 합니다.

1. **마이그레이션할 수 데이터 Oracle 및 다른 데이터베이스 엔진에서 SQL server에 Linux?**

   예 SSMA는 여러 유형의 데이터베이스 엔진에서의 마이그레이션 지원: Microsoft Access, DB2, MySQL, Oracle 및 SAP ASE (이전의 SAP Sybase ASE). SSMA를 사용 하는 방법의 예제를 보려면 [SQL Server 2017 linux와 SQL Server Migration Assistant로 Oracle 스키마 마이그레이션](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)합니다.

1. **SQL Server 파일에 필요한 권한은 무엇입니까?**

   모든 파일은 `/var/opt/mssql` 파일 폴더에서 소유 해야는 **mssql** 사용자에 속한는 **mssql** 그룹입니다. 두는 **mssql** 사용자 및 그룹의 모든 파일 및 디렉터리 읽기 / 쓰기 권한이 있어야 합니다. 파일 및 디렉터리 사용 권한을 포함 하는 다음과 같은 특별 한 시나리오를 note:

   * Mssql 소유자 및 그룹에 대 한 권한은 SQL Server 파일을 저장 하는 데 사용 되는 탑재 된 네트워크 공유에 대 한 필요 합니다.
   * 기본이 아닌 디렉터리에서 데이터베이스 파일 또는 백업을 찾을 경우 해당 디렉터리에 대 한 권한을 설정 해야 합니다.
   * 기본 루트 umask 0022를 변경한 경우 설치 후 SQL Server 구성이 실패 합니다. 그런 다음 SQL Server 시작 계정에 필요한 권한의 수동으로 적용 해야 합니다.

1. **설치 된 mssql 계정 및 그룹에서 SQL Server 파일 및 디렉터리의 소유권을 변경할 수 있나요?**

   기본 설치에서 SQL Server 디렉터리 및 파일의 소유권을 변경 지원 하지 않습니다. Mssql 계정 및 그룹 특히 SQL Server에 사용 되 고 대화형 로그인 액세스할 수 없습니다.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
