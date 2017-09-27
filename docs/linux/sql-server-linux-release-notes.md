---
title: "SQL Server 2017 linux에 대 한 릴리스 정보 | Microsoft Docs"
description: "이 항목 릴리스 정보를 포함 하 고 SQL Server 2017 Linux에서 실행 중인 지원 되는 기능. 릴리스 정보는 RC2 및 이전 버전에 포함 됩니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 14277304baaaf6aa40fe279af407c7ce915eaa60
ms.contentlocale: ko-kr
ms.lasthandoff: 09/25/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>SQL Server 2017 linux에 대 한 릴리스 정보

다음 릴리스 정보는 SQL Server 2017 Linux에서 실행 중인에 적용 됩니다. 이 릴리스에서 Linux에 대 한 다양 한 SQL Server 데이터베이스 엔진 기능을 지원합니다. 아래 항목은 가장 최근 릴리스로 RC2 부터는 각 릴리스에 대 한 섹션으로 구분 됩니다. 지원 되는 플랫폼, 도구, 기능 및 알려진된 문제에 대 한 각 섹션의 정보를 참조 하십시오.

다음 표에서이 항목에서 설명 하는 SQL Server 2017 릴리스를 나열 합니다.

| 릴리스 | 버전 | 릴리스 날짜 |
|-----|-----|-----|
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| [CTP 2.1](#ctp21) | 14.0.600.250 | 5-2017 |
| [CTP 2.0](#ctp20) | 14.0.500.272 | 4-2017 |
| [1.4 CTP](#ctp14) | 14.0.405.198 | 3-2017 |
| [1.3 CTP](#ctp13) | 14.0.304.138 | 2-2017 |
| [1.2 CTP](#ctp12) | 14.0.200.24 | 1-2017 |
| [CTP 1.1](#ctp11) | 14.0.100.187 | 12-2016 |
| [CTP 1.0](#ctp10) | 14.0.1.246 | 11-2016 |

## <a id="RC2"></a>RC2 (2017 년 8 월)

이 릴리스에 대 한 SQL Server 엔진 버전 14.0.900.75입니다.

### <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE]
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 1.5 t B의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보

패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고는 다음과 같은 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.900.75-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.900.75-1 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.900.75-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.900.75-1_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.900.75-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.900.75-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.900.75-1_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [Visual Studio 용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 |

### <a name="Unsupported"></a>지원 되지 않는 기능 및 서비스

다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | 타사 연결을 통해 분산된 쿼리 |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| &nbsp; | 버퍼 풀 확장 |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, 큐 판독기, SSIS, SSAS, SSRS |
| &nbsp; | 경고 |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | 변경 데이터 캡처 |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| **서비스** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제

다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 r c 2의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반

- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- 기본 언어는 **sa** 로그인 영어입니다.

    - **해상도**:의 언어를 변경는 **sa** 사용 하 여 로그인의 **ALTER LOGIN** 문.

#### <a name="databases"></a>데이터베이스

- Mssql conf 유틸리티와 master 데이터베이스를 이동할 수 없습니다. Mssql 구성 된 다른 시스템 데이터베이스를 이동할 수 있습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

- (암호 그룹)에 대 한 보안 TLS (전송 계층) 일부 알고리즘은 Linux에서 SQL Server에서는 제대로 작동 하지 않습니다. 그러면 연결 오류가 SQL Server에 연결 하려고 할 때 뿐만 아니라 문제가 높은 가용성 그룹의 복제본 간의 연결을 설정 합니다.

   - **해상도**: 수정 된 **mssql.conf** linux에서 다음을 수행 하 여 문제가 있는 암호 그룹을 사용 하지 않으려면 SQL Server에 대 한 구성 스크립트:

      1. 다음 /var/opt/mssql/mssql.conf를 추가 합니다.

      ```
      [network]
      tlsciphers=ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

      1. 다음 명령을 사용 하 여 SQL Server를 다시 시작 합니다.
   
      ```
      sudo systemctl restart mssql-server
      ```

- SQL Server 2014 데이터베이스 메모리 내 OLTP를 사용 하는 창에 SQL Server 2017 linux에서 복원할 수 없습니다. 메모리 내 OLTP를 사용 하는 SQL Server 2014 데이터베이스를 복원 하려면 먼저 데이터베이스를 업그레이드 SQL Server 2016 또는 Windows에서 SQL Server 2017 이동 하기 전에 SQL Server로 Linux에서 백업/복원 또는 분리/연결을 통해.

#### <a name="remote-database-files"></a>원격 데이터베이스 파일

- NFS 서버에서 데이터베이스 파일을 호스팅하는이 릴리스에서 지원 되지 않습니다. NFS를 사용 하 여 공유 디스크 장애 조치 클러스터 되지 않은 인스턴스에서 데이터베이스 뿐만 아니라 클러스터링에 대 한 포함 됩니다. 작업을 이후 릴리스에서 NFS 서버 지원을 사용 하도록 설정 합니다.

#### <a name="localization"></a>지역화

- 로캘에서 영어가 아닌 (en_us) 설치 하는 동안 bash 세션/터미널에 utf-8 인코딩을 사용 해야 합니다. ASCII 인코딩을 사용 하는 경우 다음과 유사한 오류가 표시 될 수 있습니다.

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   인코딩을 u t F-8을 사용할 수 없는 경우 언어 선택 지정 하려면 MSSQL_LCID 환경 변수를 사용 하 여 설치 프로그램을 실행 합니다.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name="full-text-search"></a>전체 텍스트 검색
- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

#### <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)
Linux에서 SSIS 패키지를 실행할 수 있습니다. 자세한 내용은 다음 문서를 참조 합니다.
-   [Linux에 대 한 SSIS 지원 블로그 게시물 발표](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)합니다.
-   [Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)

이 릴리스에서 다음과 같은 알려진된 문제가 note 하십시오.

- **mssql 서버는** 패키지는이 릴리스에서 Ubuntu 및 Red Hat Enterprise Linux (RHEL)에서 지원 됩니다.

- 이상 Linux CTP 2.1 새로 고침에서 SSIS, SSIS 패키지는 Linux 기반 ODBC 연결 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버와 함께 테스트 되었습니다 하지만 또한 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 해야 합니다. 디자인 타임에 ODBC 데이터;에 연결 하는 DSN 또는 연결 문자열 중 하나를 제공할 수 있습니다. 또한 Windows 인증을 사용할 수 있습니다. 자세한 내용은 참조는 [블로그 게시물 Linux ODBC 지원 발표](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

- Linux에서 SSIS 패키지를 실행할 때이 릴리스에서 다음과 같은 기능이 지원 되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약 된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS 규모 확장
  - SSIS 용 azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="RC1"></a>RC1 (2017 년 7 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.800.90입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE]
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 최대 1TB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고는 다음과 같은 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.800.90-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.800.90-2 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.800.90-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.800.90-2_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.800.90-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.800.90-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.800.90-2_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [Visual Studio 용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 |

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 기계 학습 서비스 |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, 큐 판독기, SSIS, SSAS, SSRS |
| &nbsp; | 경고 |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | 변경 데이터 캡처 |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| &nbsp; | 가용성 그룹의 롤링 업그레이드 |
| **보안** | 확장 가능 키 관리 |
| **서비스** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 r c 1의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- 기본 언어는 **sa** 로그인 영어입니다.

    - **해상도**:의 언어를 변경는 **sa** 사용 하 여 로그인의 **ALTER LOGIN** 문.

#### <a name="databases"></a>데이터베이스

- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="remote-database-files"></a>원격 데이터베이스 파일

- NFS 서버에서 데이터베이스 파일을 호스팅하는이 릴리스에서 지원 되지 않습니다. NFS를 사용 하 여 공유 디스크 장애 조치 클러스터 되지 않은 인스턴스에서 데이터베이스 뿐만 아니라 클러스터링에 대 한 포함 됩니다. 작업을 이후 릴리스에서 NFS 서버 지원을 사용 하도록 설정 합니다.

#### <a name="cross-platform-availability-groups-and-distributed-availability-groups"></a>크로스 플랫폼 가용성 그룹 및 분산된 된 가용성 그룹

- 알려진된 문제로 인해 가용성 그룹에는 Windows 및 Linux에서 호스트 인스턴스 복제본 만들기 작동 하지 않습니다이 릴리스에서. 분산형된 가용성 그룹을 포함 합니다. 수정 프로그램은 곧 출시 될 릴리스에 후보 빌드에 사용할 수 있습니다. 

#### <a name="server-collation"></a>서버 데이터 정렬

- 재정의 MSSQL_COLLATION를 사용 하 여 시기나 지역화 (비 영어) 설치를 수행 하는 경우 SQL Server에서 덤프를 생성 하는 서버 데이터 정렬을 설정 하는 동안 교착 상태가 도달 합니다. 그러나 서버 데이터 정렬은 설정 하지 설치 프로그램이 성공적으로 완료지 않습니다. 실행 하면이 문제를 해결 합니다. / mssql conf 데이터 정렬 설정 대화 상자가 나타나면 원하는 데이터 정렬 이름을 입력 하 고 (데이터 정렬 이름이 고 줄에서 오류 로그에서 확인할 수 있습니다: "...에 기본 데이터 정렬을 변경 하 는"). 
 
#### <a name="localization"></a>지역화

- 로캘에서 영어가 아닌 (en_us) 설치 하는 동안 bash 세션/터미널에 utf-8 인코딩을 사용 해야 합니다. ASCII 인코딩을 사용 하는 경우 다음과 유사한 오류가 표시 될 수 있습니다.

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   인코딩을 u t F-8을 사용할 수 없는 경우 언어 선택 지정 하려면 MSSQL_LCID 환경 변수를 사용 하 여 설치 프로그램을 실행 합니다.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name = "fci"></a>공유 디스크 클러스터 인스턴스 업그레이드

R c 1에서 클러스터 리소스 에이전트 같이 windows 장애 조치 클러스터 인스턴스의 가상 서버 이름을 설정 합니다. RC1 이전 `@@servername` 클러스터 공유 디스크에서 특정 노드를 반환 하므로 장애 조치 후 이름을 `@@servername` 다른 값을 반환 합니다. R c 1에서 리소스를 클러스터에 추가 하는 경우 공유 디스크 클러스터 인스턴스의 serverName 리소스 이름으로 업데이트 됩니다. 이 인해 클러스터-다음 단계에 따라 업그레이드 중 수동 장애 조치 후 SQL Server를 다시 시작 해야 합니다.

1. 먼저 보조 (패시브) 클러스터 노드를 업그레이드 합니다.
   - 업그레이드 **mssql 서버** 패키지 합니다.
   - 업그레이드 **mssql-서버-ha** 패키지 합니다.
1. 수동 장애 조치를 업그레이드 된 노드로 합니다.
   `pcs resource move <resourceName>`
   - 리소스는 리소스 에이전트 및 예상 되는 실제 서버 이름으로 확인 하므로 처음에 실패 합니다. 예상된 serverName 달라 집니다.
   - 클러스터는 노드와 동일한 노드에서 SQL Server 리소스를 다시 시작 됩니다. 서버 이름을 업데이트 합니다.
1. 다른 노드를 업그레이드 합니다. 
   - 업그레이드 **mssql 서버** 패키지 합니다.
   - 업그레이드 **mssql-서버-ha** 패키지 합니다.
1. 수동 리소스 이동의 추가 제약 조건을 제거 합니다. 참조 [장애 조치 클러스터를 수동으로](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md#failManual)합니다.
2. 필요한 경우 다시 원래 주 노드를 실패 합니다. 

#### <a name="availability-group"></a>가용성 그룹

Linux의 롤링 업그레이드 SQL Server 2017 CTP 2.1 r c 1으로 지원 되지 않습니다. 보조 복제본을 업그레이드 한 후 주 복제본이 업그레이드 될 때까지 주 복제본에서 끊어집니다. Microsoft는 향후 릴리스에 대 한이 해결 하려면 계획 것입니다.

#### <a name="full-text-search"></a>전체 텍스트 검색
- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

#### <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)

- **mssql 서버는** 패키지가이 릴리스에서 SUSE에서 지원 되지 않습니다. Ubuntu 및 Red Hat Enterprise Linux (RHEL) 현재 지원 됩니다.

- Linux에서 SSIS 패키지를 실행할 때이 릴리스에서 다음과 같은 기능이 지원 되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약 된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS 규모 확장
  - SSIS 용 azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

Linux에서 SSIS에 대 한 자세한 내용은 다음 문서를 참조 합니다.
-   [Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp21"></a>CTP 2.1 (2017 년 5 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.600.250입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE]
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 최대 1TB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 다음과 같은 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.600.250-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.600.250-2 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.600.250-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.600.250-2_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.600.250-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.600.250-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.600.250-2_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [Visual Studio 용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (1.12) |

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP 2.1의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- 기본 언어는 **sa** 로그인 영어입니다.

    - **해상도**:의 언어를 변경는 **sa** 사용 하 여 로그인의 **ALTER LOGIN** 문.

#### <a name="databases"></a>데이터베이스
- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="always-on-availability-group"></a>가용성 그룹에 항상
- `sys.fn_hadr_backup_is_preffered_replica`에 대해 작동 하지 않는 `CLUSTER_TYPE=NONE` 또는 `CLUSTER_TYPE=EXTERNAL` WSFC 복제 클러스터 레지스트리를 사용 하기 때문에 키를 사용할 수 없습니다. 작업을 다른 함수를 통해 비슷한 기능을 제공 합니다. 

#### <a name="full-text-search"></a>전체 텍스트 검색
- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

#### <a name="sql-agent"></a>SQL 에이전트
- 다음 구성 요소와 SQL 에이전트 작업의 하위 시스템은 현재 Linux에서 지원 되지 않습니다.

    - 하위 시스템: CmdExec PowerShell, 복제 배포자, 스냅숏, 병합, 큐 판독기, SSIS, SSAS, SSRS
    - 경고
    - DB 메일
    - 로그 판독기 에이전트 
    - 변경 데이터 캡처

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 상대 경로 사용 하는 "/ tmp/sqlpackage 아래의 파일 매핑됩니다. \<코드 \> /시스템/system32 "폴더입니다. 

  - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

#### <a name="ssis"></a> SSIS(SQL Server Integration Services)
Linux에서 SSIS 패키지를 실행할 수 있습니다. 자세한 내용은 참조는 [Linux에 대 한 SSIS 지원 블로그 게시물 발표](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)합니다. 이 릴리스에서 다음과 같은 알려진된 문제가 note 하십시오.

- **mssql 서버는** 패키지이 이번 ubuntu 에서만 지원 됩니다.

- Linux에서 SSIS 패키지를 실행 하는 경우에 다음과 같은 기능이 지원 되지 않습니다.
  - SSIS 카탈로그 DB
  - SQL 에이전트에서 패키지 실행 일정
  - Windows 인증
  - 타사 구성 요소
  - 제 3 자 ODBC 드라이버
  - ODBC 연결 관리자, 원본 및 대상 (Linux CTP 2.1 새로 고침에 대 한 SSIS 지원)
  - CDC(변경 데이터 캡처)
  - 규모 확장
  - Azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

Linux CTP 2.1 새로 고침에 대 한 SSIS, SSIS 패키지는 Linux 기반 ODBC 연결 사용할 수 있습니다. 자세한 내용은 참조는 [블로그 게시물 Linux ODBC 지원 발표](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp20"></a>CTP 2.0 (2017 년 4 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.500.272입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 및 16.10 | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 최대 1TB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고는 다음과 같은 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.500.272-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.500.272-2 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.500.272-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |
| Ubuntu 16.10 Debian 패키지 | 14.0.500.272-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows-릴리스 후보 2 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [Visual Studio-릴리스 후보 2 용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (0.2.1) |

> [!NOTE] 
> 지정 된 SQL Server Management Studio 및 SQL Server Data Tools 버전이 위에 릴리스 후보, 따라서 프로덕션 환경에서 사용 하기 위해 권장 하지 않습니다.

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP 2.0의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- 기본 언어는 **sa** 로그인 영어입니다.

    - **해상도**:의 언어를 변경는 **sa** 사용 하 여 로그인의 **ALTER LOGIN** 문.

#### <a name="databases"></a>데이터베이스
- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="always-on-availability-group"></a>가용성 그룹에 항상
- 가용성 그룹은 pre CTP2.0 패키지를 사용 하 여 만든-Pacemaker 클러스터에 리소스로 추가 의미 하는 모든 HA 구성-새 패키지와 이전 버전과 호환 되지 않습니다. 이전에 구성 된 모든 클러스터 된 리소스를 삭제 하 고 있는 새 가용성 그룹을 만들고 `CLUSTER_TYPE=EXTERNAL`합니다. 참조 [Linux에서 SQL Server에 대 한 가용성 그룹에 항상 구성](sql-server-linux-availability-group-configure-ha.md)합니다.
- 가용성 그룹을 사용 하 여 만든 `CLUSTER_TYPE=NONE` 클러스터의에서 리소스를 업그레이드 한 후 작업을 계속는 다음에 추가 되지 않습니다. 읽기 배율 시나리오에 사용 됩니다. 참조 [Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹 구성](sql-server-linux-availability-group-configure-rs.md)합니다.
- `sys.fn_hadr_backup_is_preffered_replica`에 대해 작동 하지 않는 `CLUSTER_TYPE=NONE` 또는 `CLUSTER_TYPE=EXTERNAL` WSFC 복제 클러스터 레지스트리를 사용 하기 때문에 키를 사용할 수 없습니다. 작업을 다른 함수를 통해 비슷한 기능을 제공 합니다. 

#### <a name="full-text-search"></a>전체 텍스트 검색
- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

- 한국어 단어 분리기를 로드 하는 데 몇 초를 처음 사용할 때 오류를 생성 합니다. 이 초기 오류가 발생 한 후이 정상적으로 진행 됩니다.

#### <a name="sql-agent"></a>SQL 에이전트
- 다음 구성 요소와 SQL 에이전트 작업의 하위 시스템은 현재 Linux에서 지원 되지 않습니다.

    - 하위 시스템: CmdExec PowerShell, 복제 배포자, 스냅숏, 병합, 큐 판독기, SSIS, SSAS, SSRS
    - 경고
    - DB 메일
    - 로그 판독기 에이전트 
    - 변경 데이터 캡처

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 상대 경로 사용 하는 "/ tmp/sqlpackage 아래의 파일 매핑됩니다. \<코드 \> /시스템/system32 "폴더입니다. 

    - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

    
#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp14"></a>1.4 CTP (2017 년 3 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.405.198입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 및 16.10 | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 최대 1TB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 아래 단계를 사용 하 여 설치에서 하는 경우 이러한 패키지를 직접 다운로드 해야 하는 참고 안내
-   [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
-   [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
-   [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.405.200-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.405.200-1 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.405.200-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |
| Ubuntu 16.10 Debian 패키지 | 14.0.405.200-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows-릴리스 후보 2 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [Visual Studio-릴리스 후보 2 용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (0.2.1) |

> [!NOTE] 
> 지정 된 SQL Server Management Studio 및 SQL Server Data Tools 버전이 위에 릴리스 후보, 따라서 프로덕션 환경에서 사용 하기 위해 권장 하지 않습니다.

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP 1.4의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 이 명령을 실행 하지 않는 `ALTER SERVICE MASTER KEY REGENERATE`합니다. SQL Server를 불안정 하는 알려진된 버그가 있습니다. 서비스 마스터 키를 다시 생성 해야 하는 경우 데이터베이스 파일을 백업 제거 하 고 SQL Server를 다시 설치를 한 다음 다시 데이터베이스 파일을 복원 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- Windows 표준 시간대 이름을 정확 하 게 일부 표준 시간대 이름 Linux에 매핑하지 마세요.

    - **해상도**: TZID 열에 표준 시간대 이름을 사용 하는 '에 대 한 매핑: Windows의 섹션 테이블에는 [Unicode.org 설명서 페이지](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)합니다.

- SQL Server 엔진 CR LF (줄 서식 Windows 스타일)으로 종결 되어야 하는 텍스트 파일의 줄이 필요 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- 모든 로그 파일 및 오류 로그를 u t F-16으로 인코딩됩니다.

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- **CREATE ASSEMBLY** 파일을 사용 하는 동안 작동 하지 것입니다. 사용 하 여는 **FROM \<비트\> ** 메서드 대신 지금은 합니다. 

#### <a name="databases"></a>데이터베이스
- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="always-on-availability-group"></a>가용성 그룹에 항상
- Always On 가용성 그룹 CTP 1.3을 사용 하 여 만든 linux 클러스터 된 리소스는 HA 패키지 (mssql-서버-ha)를 업그레이드 한 후에 실패 합니다. 

   - **해상도**: HA 패키지를 업그레이드 하기 전에 클러스터 리소스 매개 변수를 설정 `notify=true`합니다. 
   
      - 다음 예제에서는 명명 된 리소스에서 클러스터 리소스 매개 변수를 설정 **ag1** RHEL 또는 Ubuntu: 

      ```bash
      sudo pcs resource update ag1-master notify=true
      ```

      - SLES에 대 한 업데이트를 추가 하려면 가용성 그룹 리소스 구성 `notify=true`합니다.  

      ```bash
      crm configure edit ms-ag_cluster 
      ```

      추가 `notify=true` 리소스 구성 하 고 저장 합니다.

- Always On 가용성 그룹 Linux에서 복제본이 동기 커밋 모드에 있을 경우 데이터 손실이 있을 수 있습니다. Linux 배포판에 따라 세부 정보를 참조 합니다. 

   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

#### <a name="full-text-search"></a>전체 텍스트 검색
- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

- 한국어 단어 분리기를 로드 하는 데 몇 초를 처음 사용할 때 오류를 생성 합니다. 이 초기 오류가 발생 한 후이 정상적으로 진행 됩니다.

#### <a name="sql-agent"></a>SQL 에이전트
- 다음 구성 요소와 SQL 에이전트 작업의 하위 시스템은 현재 Linux에서 지원 되지 않습니다.
    - 하위 시스템: CmdExec PowerShell, 복제 배포자, 스냅숏, 병합, 큐 판독기, SSIS, SSAS, SSRS
    - 경고
    - DB 메일
    - 로그 전달
    - 로그 판독기 에이전트 
    - 변경 데이터 캡처

#### <a name="in-memory-oltp"></a>메모리 내 OLTP
- 메모리 내 OLTP 데이터베이스 /var/opt/mssql 디렉터리에만 만들 수 있습니다. 자세한 내용은 참조는 [메모리 내 OLTP 항목](sql-server-linux-performance-get-started.md#use-in-memory-oltp)합니다.

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 상대 경로 사용 하는 "/ tmp/sqlpackage 아래의 파일 매핑됩니다. \<코드 \> /시스템/system32 "폴더입니다. 

    - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

    
#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- 파일 탐색기에 사용할 수는 "c:\\" 범위를 확인/var/옵트인/mssql/linux. 다른 경로 사용 하려면 UI 작업의 스크립트를 생성 하 고 c: 드라이브를 교체\\ Linux 경로가 포함 된 경로입니다. SSMS에서 스크립트를 수동으로 실행 합니다.

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp13"></a>1.3 CTP (2017 년 2 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.304.138입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 및 16.10 | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 최대 1TB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고를 다운로드 하려면 필요 하지 않으면 패키지의 단계를 사용 하는 경우 직접는 [설치 가이드](sql-server-linux-setup.md)합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.304.138-1 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[mssql-서버-ha 높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[mssql-서버-fts 전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.304.138-1 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[mssql-서버-ha 높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[mssql-서버-fts 전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.304.138-1 | [mssql 서버 엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[mssql-서버-ha 높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[mssql-서버-fts 전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |
| Ubuntu 16.10 Debian 패키지 | 14.0.304.138-1 | [mssql 서버 엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[mssql-서버-ha 높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[mssql-서버-fts 전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows-릴리스 후보 2 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [Visual Studio-릴리스 후보 2 용 SQL Server Data Tools](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (0.2.1) |

> [!NOTE] 
> 지정 된 SQL Server Management Studio 및 SQL Server Data Tools 버전이 위에 릴리스 후보, 따라서 프로덕션 환경에서 사용 하기 위해 권장 하지 않습니다.

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server 에이전트 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP 1.3의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 이 명령을 실행 하지 않는 `ALTER SERVICE MASTER KEY REGENERATE`합니다. SQL Server를 불안정 하는 알려진된 버그가 있습니다. 서비스 마스터 키를 다시 생성 해야 하는 경우 데이터베이스 파일을 백업 제거 하 고 SQL Server를 다시 설치를 한 다음 다시 데이터베이스 파일을 복원 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- Windows 표준 시간대 이름을 정확 하 게 일부 표준 시간대 이름 Linux에 매핑하지 마세요.

    - **해상도**: TZID 열에 표준 시간대 이름을 사용 하는 '에 대 한 매핑: Windows의 섹션 테이블에는 [Unicode.org 설명서 페이지](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)합니다.

- SQL Server 엔진 CR LF (줄 서식 Windows 스타일)으로 종결 되어야 하는 텍스트 파일의 줄이 필요 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- 모든 로그 파일 및 오류 로그를 u t F-16으로 인코딩됩니다.

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- **CREATE ASSEMBLY** 파일을 사용 하는 동안 작동 하지 것입니다. 사용 하 여는 **FROM \<비트\> ** 메서드 대신 지금은 합니다. 

#### <a name="databases"></a>데이터베이스
- TempDB 데이터 및 로그 파일의 위치 변경은 지원 되지 않습니다.

- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

- Always On 가용성 그룹 Linux에서 복제본이 동기 커밋 모드에 있을 경우 데이터 손실이 있을 수 있습니다. 참조 항목 
 
   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   
#### <a name="full-text-search"></a>전체 텍스트 검색
- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

- 한국어 단어 분리기를 로드 하는 데 몇 초를 처음 사용할 때 오류를 생성 합니다. 이 초기 오류가 발생 한 후이 정상적으로 진행 됩니다.

#### <a name="in-memory-oltp"></a>메모리 내 OLTP
- 메모리 내 OLTP 데이터베이스 /var/opt/mssql 디렉터리에만 만들 수 있습니다. 자세한 내용은 참조는 [메모리 내 OLTP 항목](sql-server-linux-performance-get-started.md#use-in-memory-oltp)합니다.  

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 아래에 있는 파일의 상대 경로 사용 하 여 매핑됩니다는 "/tmp/sqlpackage./ <code/> /시스템/system32" 폴더입니다. 

    - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 및 ODBC 
- SQL Server 명령줄 도구 (mssql 도구) 및 ODBC 드라이버 (배치한) 사용자 지정 unixODBC 드라이버 관리자에 따라 달라 집니다. 이전에 설치 된 unixODBC 드라이버 관리자를 설정한 경우 충돌이 발생 합니다. 

    - **해결 방법**: Ubuntu, 충돌은 자동으로 해결할 수 있습니다. 기존 unixODBC 드라이버 관리자를 제거 하려는 경우 메시지가 표시 되 면 'y'를 입력 하 고 설치를 계속 합니다. RedHat을에 기존 unixODBC 드라이버 관리자를 수동으로 제거 해야 합니다를 사용 하 여 `yum remove unixODBC`합니다. म RHEL 및 SUSE에 대 한이 제한을 해결 작업 중 이며 있습니다에 대 한 업데이트가 곧 있어야 합니다.  
    
#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- SQL Server 에이전트를 아직 지원 되지 않습니다. 따라서 SSMS의 SQL Server 에이전트 기능 않습니다 하지 현재 Linux에서 작동 됩니다.

- 파일 탐색기에 사용할 수는 "c:\\" 범위를 확인/var/옵트인/mssql/linux. 다른 경로 사용 하려면 UI 작업의 스크립트를 생성 하 고 c: 드라이브를 교체\\ Linux 경로가 포함 된 경로입니다. SSMS에서 스크립트를 수동으로 실행 합니다.

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp12-ctp-12-january-2017"></a><a id="ctp12">CTP 1.2 (2017 년 1 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.200.24입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 및 16.10 | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진만 되었습니다.이 이번에는 최대 256 GB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고를 다운로드 하려면 필요 하지 않으면 패키지의 단계를 사용 하는 경우 직접는 [설치 가이드](sql-server-linux-setup.md)합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| RPM 패키지 | 14.0.200.24-2 | [mssql 서버 14.0.200.24-2 엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.200.24-2.x86_64.rpm)</br>[mssql 서버 14.0.200.24-2 높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.200.24-2.x86_64.rpm) | 
| Debian 패키지 | 14.0.200.24-2 | [mssql 서버 14.0.200.24-2 엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.200.24-2_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows-릴리스 후보 1 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools for Visual Studio-릴리스 후보 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (0.2) |

> [!NOTE] 
> 지정 된 SQL Server Management Studio 및 SQL Server Data Tools 버전이 위에 릴리스 후보, 따라서 프로덕션 환경에서 사용 하기 위해 권장 하지 않습니다.

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 전체 텍스트 검색 |
| &nbsp; | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | Always On 가용성 그룹 |
| &nbsp; | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server 에이전트 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP 1.2의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 이 명령을 실행 하지 않는 `ALTER SERVICE MASTER KEY REGENERATE`합니다. SQL Server를 불안정 하는 알려진된 버그가 있습니다. 서비스 마스터 키를 다시 생성 해야 하는 경우 데이터베이스 파일을 백업 제거 하 고 SQL Server를 다시 설치를 한 다음 다시 데이터베이스 파일을 복원 합니다.

- SQL 리소스 ocf:mssql:fci ocf:sql:fci에서 변경에 대 한 리소스 이름입니다. 공유 디스크 장애 조치 클러스터를 찾을 수를 구성 하는 방법에 대 한 자세한 내용은 [여기](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure)합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- Windows 표준 시간대 이름을 정확 하 게 일부 표준 시간대 이름 Linux에 매핑하지 마세요.

    - **해상도**: TZID 열에 표준 시간대 이름을 사용 하는 '에 대 한 매핑: Windows의 섹션 테이블에는 [Unicode.org 설명서 페이지](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)합니다.

- SQL Server 엔진 CR LF (줄 서식 Windows 스타일)으로 종결 되어야 하는 텍스트 파일의 줄이 필요 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- 모든 로그 파일 및 오류 로그를 u t F-16으로 인코딩됩니다.

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- **CREATE ASSEMBLY** 파일을 사용 하는 동안 작동 하지 것입니다. 사용 하 여는 **FROM \<비트\> ** 메서드 대신 지금은 합니다. 

#### <a name="databases"></a>데이터베이스
- TempDB 데이터 및 로그 파일의 위치 변경은 지원 되지 않습니다.

- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="in-memory-oltp"></a>메모리 내 OLTP
- 메모리 내 OLTP 데이터베이스 /var/opt/mssql 디렉터리에만 만들 수 있습니다. 이러한 데이터베이스도 해야 할는 "c:\\" 참조 될 때 표기법입니다. 자세한 내용은 참조는 [메모리 내 OLTP 항목](sql-server-linux-performance-get-started.md#use-in-memory-oltp)합니다.  

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 상대 경로 사용 하는 "/ tmp/sqlpackage 아래의 파일 매핑됩니다. \<코드 \> /시스템/system32 "폴더입니다. 

    - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 및 ODBC 
- 이전 버전의 SQL Server 명령줄 도구 (mssql 도구) 및 ODBC 드라이버 (배치한)가 사용자 지정 unixODBC 드라이버 관리자 (unixODBC utf16) 설치 될 수 있습니다. 사용자 지정 드라이버 관리자를 더 이상 사용이 충돌 가능성이 일으킬 수 없습니다. 

    - **해결 방법**: Ubuntu 및 SLES 충돌은 자동으로 해결할 수 있습니다. 기존 unixODBC 드라이버 관리자를 제거 하려는 경우 메시지가 표시 되 면 'y'를 입력 하 고 설치를 계속 합니다. RedHat을에 기존 unixODBC 드라이버 관리자를 수동으로 제거 해야 합니다를 사용 하 여 `yum remove unixODBC-utf16 unixODBC-utf16-devel` 설치를 다시 시도 하십시오.
    
#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- SQL Server 에이전트를 아직 지원 되지 않습니다. 따라서 SSMS의 SQL Server 에이전트 기능 않습니다 하지 현재 Linux에서 작동 됩니다.

- 파일 탐색기에 사용할 수는 "c:\\" 범위를 확인/var/옵트인/mssql/linux. 다른 경로 사용 하려면 UI 작업의 스크립트를 생성 하 고 c: 드라이브를 교체\\ Linux 경로가 포함 된 경로입니다. SSMS에서 스크립트를 수동으로 실행 합니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp11-ctp-11-december-2016"></a><a id="ctp11">CTP 1.1 (2016 년 12 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.100.187입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS 및 16.10 | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진만 되었습니다.이 이번에는 최대 256 GB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고를 다운로드 하려면 필요 하지 않으면 패키지의 단계를 사용 하는 경우 직접는 [설치 가이드](sql-server-linux-setup.md)합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| RPM 패키지 | 14.0.100.187-1 | [mssql 서버 14.0.100.187-1 엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.100.187-1.x86_64.rpm)</br>[mssql 서버 14.0.100.187-1 높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.100.187-1.x86_64.rpm) | 
| Debian 패키지 | 14.0.100.187-1 | [mssql 서버 14.0.100.187-1 엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.100.187-1_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows-릴리스 후보 1 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools for Visual Studio-릴리스 후보 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (0.2) |

> [!NOTE] 
> 지정 된 SQL Server Management Studio 및 SQL Server Data Tools 버전이 위에 릴리스 후보, 따라서 프로덕션 환경에서 사용 하기 위해 권장 하지 않습니다.

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 전체 텍스트 검색 |
| &nbsp; | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | Always On 가용성 그룹 |
| &nbsp; | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server 에이전트 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP 1.1의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 이 명령을 실행 하지 않는 `ALTER SERVICE MASTER KEY REGENERATE`합니다. SQL Server를 불안정 하는 알려진된 버그가 있습니다. 서비스 마스터 키를 다시 생성 해야 하는 경우 데이터베이스 파일을 백업 제거 하 고 SQL Server를 다시 설치를 한 다음 다시 데이터베이스 파일을 복원 합니다.

- SQL 리소스 ocf:mssql:fci ocf:sql:fci에서 변경에 대 한 리소스 이름입니다. 공유 디스크 장애 조치 클러스터를 찾을 수를 구성 하는 방법에 대 한 자세한 내용은 [여기](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure)합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- Windows 표준 시간대 이름을 정확 하 게 일부 표준 시간대 이름 Linux에 매핑하지 마세요.

    - **해상도**: TZID 열에 표준 시간대 이름을 사용 하는 '에 대 한 매핑: Windows의 섹션 테이블에는 [Unicode.org 설명서 페이지](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)합니다.

- SQL Server 엔진 CR LF (줄 서식 Windows 스타일)으로 종결 되어야 하는 텍스트 파일의 줄이 필요 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- 모든 로그 파일 및 오류 로그를 u t F-16으로 인코딩됩니다.

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- **CREATE ASSEMBLY** 파일을 사용 하는 동안 작동 하지 것입니다. 사용 하 여는 **FROM \<비트\> ** 메서드 대신 지금은 합니다. 

#### <a name="databases"></a>데이터베이스
- TempDB 데이터 및 로그 파일의 위치 변경은 지원 되지 않습니다.

- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="in-memory-oltp"></a>메모리 내 OLTP
- 메모리 내 OLTP 데이터베이스 /var/opt/mssql 디렉터리에만 만들 수 있습니다. 이러한 데이터베이스도 해야 할는 "c:\" 표기법 참조 합니다. 자세한 내용은 참조는 [메모리 내 OLTP 항목](sql-server-linux-performance-get-started.md#use-in-memory-oltp)합니다.  

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 상대 경로 사용 하는 "/ tmp/sqlpackage 아래의 파일 매핑됩니다. \<코드 \> /시스템/system32 "폴더입니다. 

    - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 및 ODBC 
- SQL Server 명령줄 도구 (mssql 도구) 및 ODBC 드라이버 (배치한) 사용자 지정 unixODBC 드라이버 관리자에 따라 달라 집니다. 이전에 설치 된 unixODBC 드라이버 관리자를 설정한 경우 충돌이 발생 합니다. 

    - **해결 방법**: Ubuntu, 충돌은 자동으로 해결할 수 있습니다. 기존 unixODBC 드라이버 관리자를 제거 하려는 경우 메시지가 표시 되 면 'y'를 입력 하 고 설치를 계속 합니다. RedHat을에 기존 unixODBC 드라이버 관리자를 수동으로 제거 해야 합니다를 사용 하 여 `yum remove unixODBC`합니다. म RHEL 및 SUSE에 대 한이 제한을 해결 작업 중 이며 있습니다에 대 한 업데이트가 곧 있어야 합니다.  
    
#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- SQL Server 에이전트를 아직 지원 되지 않습니다. 따라서 SSMS의 SQL Server 에이전트 기능 않습니다 하지 현재 Linux에서 작동 됩니다.

- 파일 탐색기에 사용할 수는 "c:\\" 범위를 확인/var/옵트인/mssql/linux. 다른 경로 사용 하려면 UI 작업의 스크립트를 생성 하 고 c: 드라이브를 교체\\ Linux 경로가 포함 된 경로입니다. SSMS에서 스크립트를 수동으로 실행 합니다.

v

![분리 모음 그래픽](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp10-ctp-10-november-2016"></a><a id="ctp10">CTP 1.0 (2016 년 11 월)
이 릴리스에 대 한 SQL Server 엔진 버전 14.0.1.246입니다.

### <a name="supported-platforms"></a>지원 플랫폼 

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.2 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진만 되었습니다.이 이번에는 최대 256 GB의 메모리를 테스트 합니다.

### <a name="package-details"></a>패키지 세부 정보
패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고를 다운로드 하려면 필요 하지 않으면 패키지의 단계를 사용 하는 경우 직접는 [설치 가이드](sql-server-linux-setup.md)합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| RPM 패키지 | 14.0.1.246-6 | [mssql 서버 14.0.1.246-6 엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.1.246-6.x86_64.rpm)</br>[mssql 서버 14.0.1.246-6 높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.1.246-6.x86_64.rpm) | 
| Debian 패키지 | 14.0.1.246-6 | [mssql 서버 14.0.1.246-6 엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.1.246-6_amd64.deb) |

### <a name="supported-client-tools"></a>지원 되는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [Windows-릴리스 후보 1 용 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools for Visual Studio-릴리스 후보 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) 와 [mssql 확장](https://aka.ms/mssql-marketplace) | 최신 (0.1.5) |

> [!NOTE] 
> 지정 된 SQL Server Management Studio 및 SQL Server Data Tools 버전이 위에 릴리스 후보, 따라서 프로덕션 환경에서 사용 하기 위해 권장 하지 않습니다.

### <a name="unsupported-features-and-services"></a>지원 되지 않는 기능 및 서비스
다음 기능 및 서비스에서 사용할 수 없는 Linux이 이번에 있습니다. 이러한 기능의 지원 미리 보기 프로그램의 월별 업데이트 흐름 중 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 전체 텍스트 검색 |
| &nbsp; | 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| **고가용성** | Always On 가용성 그룹 |
| &nbsp; | 데이터베이스 미러링  |
| **보안** | Active Directory 인증 |
| &nbsp; | Windows 인증 |
| &nbsp; | 확장 가능 키 관리 |
| &nbsp; | SSL 또는 TLS에 대 한 사용자가 제공한 인증서의 사용 |
| **서비스** | SQL Server 에이전트 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |

### <a name="known-issues"></a>알려진 문제
다음 섹션에서는 Linux에서이 버전의 SQL Server 2017 CTP1의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반
- 여기서 SQL Server는 15 자가 하 여야 필요 설치 또는 호스트 이름의 길이입니다. 

    - **해결 방법**: 항목 합계의 15 자 이하의/등/호스트 이름에 이름을 변경 합니다.

- 수동으로 시간에 시스템 시간을 이전 버전과 설정 하면 SQL Server를 SQL Server 내에서 내부 시스템 시간을 업데이트를 중지 합니다.

    - **해결 방법**: SQL Server 다시 시작 합니다.

- Windows 표준 시간대 이름을 정확 하 게 일부 표준 시간대 이름 Linux에 매핑하지 마세요.

    - **해상도**: TZID 열에 표준 시간대 이름을 사용 하는 '에 대 한 매핑: Windows의 섹션 테이블에는 [Unicode.org 설명서 페이지](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)합니다.

- SQL Server 엔진 CR LF (줄 서식 Windows 스타일)으로 종결 되어야 하는 텍스트 파일의 줄이 필요 합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 된 호스트에 둘 이상의 인스턴스를 원하는 경우 Vm을 사용 하십시오 또는 Docker 컨테이너입니다. 

- 모든 로그 파일 및 오류 로그를 u t F-16으로 인코딩됩니다.

- SQL Server 구성 관리자는 Linux에서 SQL Server에 연결할 수 없습니다.

- **CREATE ASSEMBLY** 파일을 사용 하는 동안 작동 하지 것입니다. 사용 하 여는 **FROM \<비트\> ** 메서드 대신 지금은 합니다.

#### <a name="databases"></a>데이터베이스
- TempDB 데이터 및 로그 파일의 위치 변경은 지원 되지 않습니다.

- Mssql conf 유틸리티와 시스템 데이터베이스를 이동할 수 없습니다.

- Windows에서 SQL Server에서 백업 된 데이터베이스를 복원할 때 사용 해야는 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server를 SQL Server 분산된 트랜잭션이 지원 됩니다.

#### <a name="in-memory-oltp"></a>메모리 내 OLTP
- 메모리 내 OLTP 데이터베이스 /var/opt/mssql 디렉터리에만 만들 수 있습니다. 이러한 데이터베이스도 해야 할는 "c:\\" 참조 될 때 표기법입니다. 자세한 내용은 참조는 [메모리 내 OLTP 항목](sql-server-linux-performance-get-started.md#use-in-memory-oltp)합니다.  

#### <a name="sqlpackage"></a>SqlPackage
- SqlPackage를 사용 하 여 파일에 대 한 절대 경로 지정 해야 합니다. 상대 경로 사용 하는 "/ tmp/sqlpackage 아래의 파일 매핑됩니다. \<코드 \> /시스템/system32 "폴더입니다. 

    - **해결 방법**: 절대 파일 경로 사용 합니다.

- SqlPackage 사용 하 여 파일의 위치를 표시는 "c:\\" 접두사입니다.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 및 ODBC 
- SQL Server 명령줄 도구 (mssql 도구) 및 ODBC 드라이버 (배치한) 사용자 지정 unixODBC 드라이버 관리자에 따라 달라 집니다. 이전에 설치 된 unixODBC 드라이버 관리자를 설정한 경우 충돌이 발생 합니다. 

    - **해결 방법**: Ubuntu, 충돌은 자동으로 해결할 수 있습니다. 기존 unixODBC 드라이버 관리자를 제거 하려는 경우 메시지가 표시 되 면 'y'를 입력 하 고 설치를 계속 합니다. RedHat을에 기존 unixODBC 드라이버 관리자를 수동으로 제거 해야 합니다를 사용 하 여 `yum remove unixODBC`합니다. म RHEL 및 SUSE에 대 한이 제한을 해결 작업 중 이며 있습니다에 대 한 업데이트가 곧 있어야 합니다.  
    
#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)
Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- SQL Server 에이전트를 아직 지원 되지 않습니다. 따라서 SSMS의 SQL Server 에이전트 기능 않습니다 하지 현재 Linux에서 작동 됩니다.

- 파일 탐색기에 사용할 수는 "c:\\" 범위를 확인/var/옵트인/mssql/linux. 다른 경로 사용 하려면 UI 작업의 스크립트를 생성 하 고 c: 드라이브를 교체\\ Linux 경로가 포함 된 경로입니다. SSMS에서 스크립트를 수동으로 실행 합니다.

### <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

