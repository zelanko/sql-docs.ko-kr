---
title: "SQL Server 2017 on Linux에 대한 릴리스 정보 | Microsoft Docs"
description: "이 항목에서는 Linux에서 동작하는 SQL Server 2017에 대한 릴리스 정보 및 지원하는 기능을 포함합니다. 릴리스 정보는 가장 최신 릴리스 및 몇 가지 이전 릴리스를 포함합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/04/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: f9315ca5b46a0dc45a0f8171fa6eea67cd2f4337
ms.contentlocale: ko-kr
ms.lasthandoff: 10/18/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux">SQL Server 2017 on Linux 릴리스 정보</a>

다음 릴리스 정보는 Linux에서 동작하는 SQL Server 2017에 적용됩니다. 아래 항목은 각 릴리스에 대한 섹션으로 구분됩니다. 일반 출시 (GA) 릴리스에는 자세한 지원 내용 및 알려진 문제를 포함합니다. 각 누적 업데이트 (CU) 릴리스는 CU 변경 사항을 설명하는 지원 항목에 대한 링크 뿐만 아니라 Linux 패키지 다운로드 링크를 포함합니다.

## 지원하는 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 또는 7.4 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> SQL Server on Linux에 대한 [시스템 요구사항](sql-server-linux-setup.md#system)을 참조합니다.

## 지원하는 클라이언트 도구

| 도구 | 최소 버전 |
|-----|-----|
| [SQL Server Management Studio (SSMS) for Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools for Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com) with the [mssql extension](https://aka.ms/mssql-marketplace) | 최신 |

## 릴리스 내역

다음 표는 SQL Server 2017에 대한 릴리스 내역 목록을 보여줍니다.

| 릴리스 | 버전 | 릴리스 날짜 |
|-----|-----|-----|
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <A id="CU1"></a> 누적 업데이트 1 (2017년 10월)

SQL Server 2017 누적 업데이트 1 (CU1) 릴리스입니다. 해당 릴리스에 대한 SQL Server 엔진 버전은 14.0.3006.16 입니다. 해당 릴리스 내 수정 및 개선 사항에 관한 정보는 [https://support.microsoft.com/help/4038634](https://support.microsoft.com/help/4038634) 를 참조합니다.

### 설치

누적 업데이트 저장소를 이미 구성하였다면, 새로운 설치를 진행할 때에 최신 SQL Server 누적 업데이트 패키지를 얻을 것입니다. 누적 업데이트 저장소는 SQL Server on Linux에 대한 모든 패키지 설치 항목을 디폴트로 합니다. 저장소 구성에 대한 보다 자세한 정보는 [저장소 소스](sql-server-linux-setup.md#repositories) 를 참조합니다.

기본 SQL Server 패키지를 업데이트하려면, 각 패키지에 대해 적절한 업데이트 명령어를 실행하여 최신 누적 업데이트를 얻습니다. 각 릴리스에 대한 구체적인 업데이트 안내에 대해서는 다음 설치 가이드를 참조합니다:

- [SQL Server 패키지 설치](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지](sql-server-linux-setup-sql-agent.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)

### 패키지 세부 정보

수동 또는 오프라인 패키지 설치를 위해, RPM 및 Debian 패키지를 다음 표에 있는 정보를 통해 다운로드할 수 있습니다:

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3006.16-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3006.16-3 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3006.16-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (2017년 10 월)

SQL Server 2017 에 대한 일반 출시 (GA) 릴리스입니다. 이 릴리스에 대한 SQL Server 엔진 버전은 14.0.1000.169입니다.

### 패키지 세부 정보

다음 표에서는 RPM 및 Debian 패키지에 대한 패키지 세부 정보 및 다운로드 위치를 나열합니다. 참고로 다음 설치 가이드 내 단계를 사용하는 경우에는 해당 패키지를 다운로드할 필요가 없습니다:

- [SQL Server 패키지 설치](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지 설치](sql-server-linux-setup-sql-agent.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.1000.169-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.1000.169-2 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.1000.169-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

### <a name="Unsupported"></a>지원하지 않는 기능 및 서비스

다음 기능 및 서비스는 현재 Linux에서 사용할 수 없습니다. 해당 기능에 대한 지원은 시간이 지남에 따라 점차적으로 활성화될 것입니다.

| 영역 | 지원하지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | 타사 연결을 통한 분산 쿼리 |
| &nbsp; | 시스템 확장 저장 프로시저 (XP_CMDSHELL 등) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | EXTERNAL_ACCESS 또는 UNSAFE 권한 설정을 통한 CLR 어셈블리 |
| &nbsp; | 버퍼 풀 확장 |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, 큐 판독기, SSIS, SSAS, SSRS |
| &nbsp; | 경고 |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | 변경 데이터 캡처 |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| &nbsp; | 연결된 서버에 대한 AD 인증 | 
| &nbsp; | 가용성 그룹 (AG)에 대한 AD 인증 | 
| &nbsp; | 타사 AD 도구 (Centrify, Vintela, Powerbroker) | 
| **서비스** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting  Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### 알려진 문제

다음 섹션에서는 SQL Server 2017 on Linux에 대한 일반 출시 (GA) 릴리스의 알려진 문제를 설명합니다.

#### 일반

- SQL Server 2017 GA 릴리스에 대한 업그레이드는 CTP 2.1 이상에서만 지원됩니다. 

- SQL Server가 설치되는 호스트 이름 길이는 15 글자 이하일 필요가 있습니다. 

    - **해결 방법**: /etc/hostname 내 이름을 15 글자 길이 이하로 변경합니다.

- 수동으로 시스템 시간을 이전 시간으로 설정하면 SQL Server가 SQL Server 내 내부 시스템 시간을 업데이트하는 것을 중지시킵니다.

    - **해결 방법**: SQL Server를 다시 시작합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해결 방법**: 지정된 호스트에 둘 이상의 인스턴스를 원하는 경우 VM 또는 Docker 컨테이너 사용을 고려합니다. 

- SQL Server 구성 관리자는 SQL Server on Linux에 연결할 수 없습니다.

- **sa** 로그인 기본 언어가 영어입니다.

    - **해결 방법**: **sa** 로그인 언어를 **ALTER LOGIN** 문으로 변경합니다.

#### 데이터베이스

- mssql-conf 유틸리티를 사용하여 master 데이터베이스를 이동할 수 없습니다. 다른 시스템 데이터베이스는 mssql-conf를 사용하여 이동할 수 있습니다.

- Windows용 SQL Server 에서 백업한 데이터베이스를 복원할 때, Transact SQL 문에 **WITH MOVE** 절을 사용해야 합니다.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션은 Linux에서 동작하는 SQL Server에서 지원하지 않습니다. SQL Server 에서 SQL Server 로의 분산 트랜잭션은 지원됩니다.

- TLS(전송 계층 보안)에 대한 특정 알고리즘 (암호화 집합)은 SQL Server on Linux에서 정상적으로 동작하지 않습니다. 이는 SQL Server에 연결을 시도할 때 연결 오류 뿐만 아니라 고가용성 그룹에서 복제 간 연결을 하려고 할 때 문제를 야기합니다.

   - **해결 방법**: SQL Server on Linux 에 대한 구성 스크립트인 **mssql.conf** 를 수정하여 문제가 있는 암호화 집합을 비활성화 합니다. 다음과 같이 실행합니다:

      1. 다음을 /var/opt/mssql/mssql.conf 에 추가합니다.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >앞의 코드에서, `!` 는 표현식을 무효화합니다. 이는 OpenSSL이 해당 암호화 집합을 사용하지 않도록 합니다.

      1. 다음 명령을 사용하여 SQL Server를 다시 시작합니다.

      ```bash
      sudo systemctl restart mssql-server
      ```

- 메모리 내 OLTP를 사용하는 Windows용 SQL Server 2014 데이터베이스는 SQL Server 2017 on Linux에서 복원할 수 없습니다. 메모리 내 OLTP를 사용 하는 SQL Server 2014 데이터베이스를 복원하려면 백업/복구 또는 분리/연결을 통해 SQL Server on Linux로 이동하기 전에 먼저 Windows에서 데이터베이스를 SQL Server 2016 또는 SQL Server 2017로 업그레이드합니다.

- 사용자 권한 **ADMINISTER BULK OPERATIONS** 은 현재 Linux에서 지원되지 않습니다.

#### 네트워킹

연결된 서버 또는 가용성 그룹과 같은 sqlservr 프로세스로부터 아웃바운드 TCP 연결을 포함하는 기능은 다음 조검을 모두 충족하는 경우 동작하지 않을 수 있습니다:

1. 대상 서버를 IP 주소가 아닌 호스트 이름으로 지정하였습니다.

1. 원본 인스턴스가 커널 내에서 IPv6를 비활성화였습니다. 시스템이 커널 내에서 IPv6를 활성화하였는지를 확인하려면, 다음 테스트를 모두 통과해야 합니다:

   - `cat /proc/cmdline` 은 현재 커널에 대한 부팅 cmdline을 출력할 것입니다. 출력값에 `ipv6.disable=1` 을 포함하지 않아야 합니다.
   - /proc/sys/net/ipv6/ 디렉터리가 존재햐아 합니다.
   - `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` 을 호출하는 C 프로그램이 성공해야 합니다 - syscall이 fd != -1 인 값을 반환해야 하고 EAFNOSUPPORT와 함께 실패하지 않아야 합니다.

정확한 오류는 기능에 따라 달라집니다. 연결된 서버의 경우, 이는 로그인 시간 초과 오류로 나타납니다. 가용성 그룹의 경우, 보조 구성 요소의 `ALTER AVAILABILITY GROUP JOIN` DDL은 다운로드 구성 시간 초과 오류와 함께 5분 후에 실패합니다.

이 문제를 해결하려면 다음 중 하나를 수행합니다:

1. TCP 연결 대상을 지정하기 위해 호스트 이름 대신 IP를 사용합니다.

1. 부팅 cmdline에서 `ipv6.disable=1` 을 제거하여 커널 내 IPv6를 활성화합니다. 이 작업을 수행하는 방법은 grub과 같은 부팅 로더와 Linux 배포판에 따라 다릅니다. IPv6를 비활성화하기를 원하는 경우, `sysctl` 구성 (예: `/etc/sysctl.conf`) 내에 `net.ipv6.conf.all.disable_ipv6 = 1` 를 설정하여 여전히 비활성화할 수 있습니다. 이는 시스템 네트워크 어댑터가 IPv6 주소를 가지지 못하도록 막으면서도, sqlservr 기능을 동작하도록 합니다.

#### 네트워크 파일 시스템 (NFS)
**네트워크 파일 시스템 (NFS)** 원격 공유를 프로덕션 환경에서 사용하는 경우, 다음과 같은 지원 요구 사항을 확인합니다:

- NFS 버전을 **4.2 이상** 으로 사용합니다. 이전 NFS 버전은 최신 파일 시스템에서 흔히 사용하는 fallocate 및 스파스 파일 생성과 같은 필수 기능을 지원하지 않습니다.
- **/var/opt/mssql** 디렉터리만을 NFS 마운트로 위치합니다. SQL Server 시스템 바이너리와 같은 다른 파일들은 지원하지 않습니다.
- 원격 공유를 마운트할 때 NFS 클라이언트가 'nolock' 옵션을 사용하는지 확인합니다.

#### 지역화

- 설치시 로캘이 영어(en_us)가 아닌 경우, bash 세션/터미널에서 UTF-8 인코딩을 사용해야 합니다. ASCII 인코딩을 사용하는 경우, 다음과 유사한 오류가 표시될 수 있습니다:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   UTF-8 인코딩을 사용할 수 없는 경우,  MSSQL_LCID 환경 변수를 사용하여 설치 프로그램을 실행하여 언어 선택을 지정합니다.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- mssql-conf 설치 프로그램을 실행하여 SQL Server 비 영어 버전 설치를 수행하는 경우, 잘못된 확장 문자열이 "Configuring SQL Server..."를 지역화한 텍스트 이후에 표시됩니다. 또는, 비라틴 기반 설치의 경우, 문장이 누락될 수 있습니다. 누락된 문장은 "The licensing PID was successfully processed.  The new edition is [\<Name\> edition]”를 지역화한 문자열을 출력해야 합니다. 이 문자열은 정보 목적만을 위한 출력으로, 다음 SQL Server 누적 업데이트에서는 모든 언어에 대해 해결할 것입니다. 어떤 방식으로든 SQL Server의 성공적인 설치에는 영향을 주지 않습니다.

#### 전체 텍스트 검색

- Office 문서에 대한 필터를 포함하여, 이 릴리스에서 모든 필터를 사용할 수 있는 것은 아닙니다. 지원하는 필터 목록에 대해서는, [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters) 를 참조합니다.

#### <a id="ssis"></a> SSIS(SQL Server Integration Services)

- **mssql-server-is** 패키지는 이 릴리스에서 SUSE를 지원하지 않습니다. 현재는 Ubuntu 및 Red Hat Enterprise Linux (RHEL)를 지원합니다.

- SSIS on Linux CTP 2.1 Refresh 및 이후에서, SSIS 패키지는 Linux에서 ODBC 연결을 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버와 함게 테스트가 이루어졌으나, ODBC 사양을 따르는 임의의 유니코드 ODBC 드라이버 또한 작동할 것으로 예상됩니다. 디자인 시점에, DSN 또는 연결 문자열을 ODBC 데이터에 연결하기 위해 제공할 수 있습니다. Windows 인증 또한 사용할 수 있습니다. 보다 자세한 정보는, [Linux ODBC 지원 발표 블로그 게시물](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/) 을 참조합니다.

- Linux에서 SSIS 패키지를 실행할 때 다음 기능은 이 릴리스에서 지원되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS 규모 확장
  - SSIS를 위한 Azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

  현재 지원하지 않거나 제한적으로 지원하는 기본 제공 SSIS 구성 요소에 대한 목록에 대해서는 [Linux에서 SSIS에 대한 알려진 문제 및 제한](sql-server-linux-ssis-known-issues.md#components) 을 참조합니다.

Linux에서 SSIS에 대한 자세한 내용은 다음 문서를 참조합니다.
-   [Linux에 대한 SSIS 지원 발표 블로그 게시물](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Linux에서 SQL Server Integration Services (SSIS) 설치](sql-server-linux-setup-ssis.md)
-   [SSIS와 함께 Linux에서 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)

#### SSMS(SQL Server Management Studio)

SQL Server on Linux에 연결하는 Windows에서 실행하는 SSMS에서는 다음과 같은 제한 사항이 적용됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- SSMS에서 데이터 웨어하우스 관리 (MDW) 및 데이터 수집기를 지원하지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션을 가지는 SSMS UI 구성 요소가 Linux 작동하지 않습니다. SQL 로그인과 같은 다른 옵션과 함께 하는 기능은 계속 사용할 수 있습니다. 

- 보관하는 로그 파일 개수를 수정할 수 없습니다.

### 다음 단계

시작 하려면 다음 빠른 시작 자습서를 참조하세요:

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
