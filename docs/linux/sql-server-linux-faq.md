---
title: Linux의 SQL Server FAQ
description: 이 문서에서는 Linux에서 실행되는 SQL Server 관련 FAQ(자주 묻는 질문)에 대한 답변을 제공합니다.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7b6583ce7fb4ae2d0b37d898b549a385cfc09763
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115458"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Linux의 SQL Server FAQ(질문과 대답)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

다음 섹션에서는 Linux에서 실행되는 SQL Server에 대한 일반적인 질문과 대답을 제공합니다.

## <a name="general-questions"></a>일반적인 질문

1. **어떤 Linux 플랫폼이 지원되나요?**

   SQL Server는 현재 Red Hat Enterprise Server, SUSE Linux Enterprise Server 및 Ubuntu에서 지원됩니다. Docker를 사용하여 컨테이너에서 실행할 수도 있습니다. 지원되는 버전에 대한 최신 정보는 [지원되는 플랫폼](sql-server-linux-setup.md#supportedplatforms)을 참조하세요.

1. **Linux의 SQL Server가 다른 플랫폼에서 작동하나요?**

   SQL Server는 앞에 나열된 배포에 대해 Linux에서 테스트되었으며 지원됩니다. 다른 Linux 배포판은 밀접하게 관련되어 있으며 SQL Server를 실행할 수도 있습니다(예: CentOS는 Red Hat Enterprise Server와 밀접하게 관련되어 있음). 그러나 지원되지 않는 운영 체제에 SQL Server를 설치하도록 선택하는 경우 [Microsoft SQL Server 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)의 **지원 정책** 섹션을 검토하여 자세한 지원 정보를 참조하세요. 또한 일부 커뮤니티에서 유지 관리하는 Linux 배포판에는 기본 운영 체제가 문제가 될 경우 지원을 받을 수 있는 공식적인 방법이 없습니다.

1. **Linux의 SQL Server가 Windows의 SQL Server와 동일한가요?**

   SQL Server의 핵심 데이터베이스 엔진은 Windows와 Linux가 동일합니다. 그러나 일부 기능은 현재 Linux에서 지원되지 않습니다. Linux에서 지원되지 않는 기능 목록은 [지원되지 않는 기능 및 서비스](sql-server-linux-editions-and-components-2019.md#Unsupported)를 참조하세요. [알려진 문제](sql-server-linux-release-notes.md#known-issues)도 검토하세요. 이러한 목록에 지정되지 않은 다른 SQL Server 기능 및 서비스는 Linux에서 지원됩니다.

1. **SQL Server에 대한 지원 정책은 무엇인가요?**

   지원 정책을 이해하려면 [SQL Server에 대한 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)을 검토하세요.

1. **Windows SQL Server를 사용하던 작업자입니다. Linux에서 SQL Server를 사용하는 방법을 익히는 데 도움이 되는 리소스가 있나요?**

   [빠른 시작](sql-server-linux-setup.md#platforms)은 Linux에서 SQL Server를 설치하고 Transact-SQL 쿼리를 실행하는 방법에 대한 단계별 지침을 제공합니다. 다른 자습서에서는 Linux에서 SQL Server를 사용하기 위한 추가 지침을 제공합니다. 타사 팁 목록을 보려면 [Linux의 SQL Server에 대한 MSSQLTIPS 팁 목록](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)을 참조하세요.

## <a name="licensing"></a>라이선스

1. **Linux에서 라이선스는 어떻게 작동하나요?**

   SQL Server는 Windows 및 Linux에서 동일한 방식으로 사용이 허가됩니다. 실제로 SQL Server 라이선스를 획득한 후 원하는 플랫폼에서 해당 라이선스를 사용하도록 선택할 수 있습니다. 자세한 내용은 [SQL Server 라이선스 획득 방법](https://www.microsoft.com/sql-server/sql-server-2017-pricing)을 참조하세요.

1. **이미 구매한 경우 어떤 SQL Server 버전을 선택해야 하나요?**

   mssql-conf 설치 프로그램을 실행하는 경우 다음 옵션이 표시됩니다.
   
   ```
   Choose an edition of SQL Server:
      1. Evaluation (free, no production use rights, 180-day limit)
      2. Developer (free, no production use rights)
      3. Express (free)
      4. Web (PAID)
      5. Standard (PAID)
      6. Enterprise (PAID)
      7. Enterprise Core (PAID)
      8. I bought a license through a retail sales channel and have a product key to enter.
   ```
     
   기업계약의 일부로 볼륨 라이선스를 통해 또는 MSDN 구독을 통해 라이선스를 획득한 경우 옵션 4~7을 선택해야 합니다. 이 단계에서는 라이선스를 입력하라는 메시지가 표시되지 않으며, 구성에 적합한 라이선스를 이전에 구입했어야 합니다. 정품 구입 채널을 통해 Standard Edition을 구매한 경우 옵션 8을 선택합니다. 이 옵션을 선택하면 키를 입력하라는 메시지가 표시됩니다. 

1. **Linux에 설치된 SQL Server 버전 및 에디션을 확인하려면 어떻게 하나요?**

   **sqlcmd**, **mssql-cli** 또는 Visual Studio Code와 같은 클라이언트 도구를 사용하여 SQL Server 인스턴스에 연결합니다. 그런 후 다음 Transact-SQL 쿼리를 실행하여 실행 중인 SQL Server 버전 및 에디션을 확인합니다. 

   ```sql
   SELECT @@VERSION
   SELECT SERVERPROPERTY('Edition')
   ```

## <a name="installation"></a>설치

1. **Linux 서버에 설치된 SQL Server를 가져오려면 어떻게 하나요?**

   Microsoft는 SQL Server를 설치하기 위한 패키지 리포지토리를 유지 관리하고 yum, zypper 및 apt와 같은 네이티브 패키지 관리자를 통해 설치를 지원합니다. 빠르게 설치하려면 [빠른 시작](sql-server-linux-setup.md#platforms) 중 하나를 참조하세요.

1. **Windows 10용 Linux 하위 시스템에 SQL Server를 설치할 수 있나요?**

   아니요. Windows 10에서 실행되는 Linux는 현재 SQL Server 및 관련 도구의 지원되는 플랫폼이 아닙니다.

1. **SQL Server는 데이터 파일을 위해 어떤 Linux 파일 시스템을 사용할 수 있나요?**

   현재, Linux의 SQL Server는 ext4 및 XFS를 지원합니다. 나중에 필요에 따라 다른 파일 시스템에 대한 지원이 추가될 예정입니다.

1. **오프라인으로 SQL Server를 설치하기 위한 설치 패키지를 다운로드할 수 있나요?**

   예. 자세한 내용은 [릴리스 정보](sql-server-linux-release-notes.md)의 패키지 다운로드 링크를 참조하세요. 또한 [오프라인 설치 지침](sql-server-linux-setup.md#offline)을 검토하세요.

1. **Linux에서 SQL Server 무인 설치를 수행할 수 있나요?**

   예. 무인 설치에 대한 설명은 [Linux의 SQL Server 설치 지침](sql-server-linux-setup.md#unattended)을 참조하세요. [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md) 및 [Ubuntu](sample-unattended-install-ubuntu.md)에 대한 샘플 스크립트를 참조하세요. SQL Server 고객 자문 팀에서 만든 [이 샘플 스크립트](/archive/blogs/sqlcat/unattended-install-and-configuration-for-sql-server-2017-on-linux)를 검토할 수도 있습니다.

## <a name="tools"></a>도구

1. **Windows에서 SQL Server Management Studio 클라이언트를 사용하여 Linux의 SQL Server에 액세스할 수 있나요?**

   예. Windows에서 실행되는 기존의 모든 도구를 사용하여 Linux의 SQL Server에 액세스할 수 있습니다. 여기에는 SSMS(SQL Server Management Studio), SSDT(SQL Server Data Tools), OSS 등의 Microsoft 도구와 타사 도구가 포함됩니다.

1. **Linux에서 실행되는 SSMS와 같은 도구가 있나요?**

   새 Azure Data Studio는 SQL Server를 관리하기 위한 플랫폼 간 도구입니다. 자세한 내용은 [Azure Data Studio란?](../azure-data-studio/what-is.md)을 참조하세요.

1. **Linux에서 sqlcmd 및 bcp와 같은 명령을 사용할 수 있나요?**

   예. [sqlcmd 및 bcp](sql-server-linux-setup-tools.md)는 Linux, macos 및 Windows에서 기본적으로 사용할 수 있습니다. 또한 Linux, macos 또는 Windows에서 새로운 [mssql-scripter](https://github.com/Microsoft/mssql-scripter) 명령줄 도구를 사용하여 어디서나 실행되는 SQL 데이터베이스용 T-SQL 스크립트를 생성합니다. 또한 미리 보기 릴리스에서 [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)를 참조하세요.

1. **Linux에서 실행되는 인스턴스를 위해 Windows에서 SSMS를 통해 연결할 경우 작업 모니터를 볼 수 있나요?**

   예. Windows에서 SSMS를 사용하여 원격으로 연결하고, Linux 인스턴스에서 작업 모니터 명령과 같은 도구/기능을 사용할 수 있습니다.

1. **Linux에서 SQL Server 성능을 모니터링하는 데 어떤 도구를 사용할 수 있나요?**

   [시스템 DMV(동적 관리 뷰)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 사용하여 Linux 프로세스 정보를 비롯한 SQL Server에 대한 다양한 유형의 정보를 수집할 수 있습니다. [쿼리 저장소](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)를 사용하여 쿼리 성능을 향상시킬 수 있습니다. 기본 제공 [성능 대시보드](/archive/blogs/sql_server_team/new-in-ssms-performance-dashboard-built-in) 등의 기타 도구는 Windows의 SSMS(SQL Server Management Studio)에서 원격으로 작동합니다.

   > [!TIP]
   > 성능을 향상시키는 한 가지 방법은 Linux 운영 체제와 SQL Server 인스턴스를 올바르게 구성하는 것입니다. 자세한 내용은 [SQL Server on Linux의 성능 모범 사례 및 구성 지침](sql-server-linux-performance-best-practices.md)을 참조하세요.

## <a name="administration"></a>관리

1. **Microsoft가 Linux의 SQL Server 구성 관리자와 같은 앱을 만들었나요?**

   예. Linux의 SQL Server를 위한 구성 도구인 [mssql-conf](sql-server-linux-configure-mssql-conf.md)가 있습니다.

1. **Linux의 SQL Server는 동일한 호스트에서 여러 인스턴스를 지원하나요?**

   호스트에서 여러 컨테이너를 실행하여 여러 개의 고유 인스턴스를 유지하는 것이 좋습니다. docker를 사용하면 쉽게 이렇게 할 수 있지만, 컨테이너마다 다른 포트에서 수신해야 합니다. 자세한 내용은 [여러 SQL Server 컨테이너 실행](./sql-server-linux-docker-container-deployment.md#multiple)을 참조하세요.

1. **Linux에서 Active Directory 인증이 지원되나요?**

   예. 자세한 내용은 [Linux의 SQL Server에 대한 Active Directory 인증](sql-server-linux-active-directory-authentication.md)을 참조하세요.

1. **Linux에서 Always On 및 클러스터링이 지원되나요?**

   Linux의 장애 조치(failover) 클러스터링 및 고가용성은 Linux의 Pacemaker를 통해 구현됩니다. 자세한 내용은 [비즈니스 연속성 및 데이터베이스 복구 - Linux의 SQL Server](sql-server-linux-business-continuity-dr.md)를 참조하세요.

1. **Linux에서 Windows로 또는 그 반대로 복제를 구성할 수 있나요?**

   읽기 확장 복제본은 Windows와 Linux 간에 단방향 데이터 복제에 사용할 수 있습니다.

1. **이전 버전의 SQL Server에 있는 기존 데이터베이스를 Windows에서 Linux로 마이그레이션할 수 있나요?**

   예. 이를 위한 [몇 가지 방법](sql-server-linux-migrate-overview.md)이 있습니다.

1. **Oracle 및 다른 데이터베이스 엔진에서 Linux의 SQL Server로 데이터를 마이그레이션할 수 있나요?**

   예. SSMA는 Microsoft Access, DB2, MySQL, Oracle 및 SAP ASE(이전의 SAP Sybase ASE)를 비롯한 여러 유형의 데이터베이스 엔진에서 마이그레이션하도록 지원합니다. SSMA를 사용하는 방법에 대한 예제는 [SQL Server Migration Assistant를 사용하여 Oracle 스키마를 Linux의 SQL Server로 마이그레이션](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=/sql/toc/toc.json)을 참조하세요.

1. **SQL Server 파일에는 어떤 사용 권한이 필요한가요?**

   `/var/opt/mssql` 파일 폴더의 모든 파일은 **mssql** 사용자가 소유하고 **mssql** 그룹에 속해야 합니다. **mssql** 사용자 및 그룹은 모든 파일 및 디렉터리에 대한 읽기/쓰기 권한이 있어야 합니다. 파일 및 디렉터리 사용 권한과 관련된 다음과 같은 특수한 시나리오를 확인합니다.

   * SQL Server 파일을 저장하는 데 사용되는 탑재된 네트워크 공유에는 mssql 소유자 및 그룹에 대한 권한이 필요합니다.
   * 기본 디렉터리가 아닌 디렉터리에서 데이터베이스 파일 또는 백업을 찾은 경우해당 디렉터리에 대한 사용 권한도 설정해야 합니다.
   * 기본 루트 umask를 0022와는 다르게 변경하면 설치 후에 SQL Server 구성이 실패합니다. 그런 다음, 필요한 권한을 SQL Server 시작 계정에 수동으로 적용해야 합니다.

1. **설치된 mssql 계정 및 그룹에서 SQL Server 파일 및 디렉터리의 소유권을 변경할 수 있나요?**

   기본 설치에서 SQL Server 디렉터리 및 파일의 소유권을 변경하는 것은 지원되지 않습니다. mssql 계정 및 그룹은 특별한 경우에 SQL Server에 사용되며 대화형 로그인 액세스 권한이 없습니다.
   
 1. **SQL Server 데이터 및 로그 디렉터리에 대해 바로 가기 링크가 지원되나요?** 
    
    아니요. 바로 가기 링크는 SQL Server 데이터 및 로그 디렉터리에 대해 지원되지 않습니다. 기본 데이터 및 로그 디렉터리를 변경하려면 [기본 데이터 또는 로그 디렉터리 위치 변경](sql-server-linux-configure-mssql-conf.md#datadir)을 참조하세요.
    
[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]