---
title: SQL Server 2017 on Linux에 대한 릴리스 정보 | Microsoft Docs
description: 이 항목에서는 Linux에서 동작하는 SQL Server 2017에 대한 릴리스 정보 및 지원하는 기능을 포함합니다. 릴리스 정보는 가장 최신 릴리스 및 몇 가지 이전 릴리스를 포함합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.workload: Active
ms.openlocfilehash: 786153cf6d3f9cee30a01d3b6e3a94646a75eecc
ms.sourcegitcommit: f3aa02a0f27cc1d3d5450f65cc114d6228dd9d49
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2018
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>SQL Server 2017 linux에 대 한 릴리스 정보

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 릴리스 정보는 SQL Server 2017 Linux에서 실행 중인에 적용 됩니다. 이 문서는 각 릴리스에 대 한 섹션으로 구분 됩니다. GA 릴리스 지원 가능성을 자세히 개이고 알려진 문제를 나열 합니다. 각 CU (누적 업데이트) 릴리스 CU 변경 뿐만 아니라 패키지 다운로드 Linux에 대 한 링크를 설명 하는 고객 지원 문서에 대 한 링크를 있습니다.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 또는 7.4 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 참조는 [시스템 요구 사항](sql-server-linux-setup.md#system) Linux에서 SQL Server에 대 한 합니다. SQL Server 2017에 대 한 최신 지원 정책에 대 한 참조는 [Microsoft SQL Server에 대 한 기술 지원 정책을](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)합니다.

## <a name="tools"></a>Tools

기존 클라이언트 도구는 대부분 SQL Server를 대상으로 하는 Linux에서 실행 중인 SQL Server 대상으로 원활 하 게 지정할 수 있습니다. 일부 도구는 Linux에서 작동 하도록 특정 버전 요구 사항이 있을 수 있습니다. SQL Server 도구 목록은 전체 참조 [SQL 도구 및 SQL Server 유틸리티](../tools/overview-sql-tools.md)합니다.

## <a name="release-history"></a>릴리스 기록

다음 표에서 SQL Server 2017에 대 한 출시 내역을 나열합니다.

| 릴리스 | 버전 | 릴리스 날짜 |
|-----|-----|-----|
| [CU6 적용](#CU6) | 14.0.3025.34 | 2018 4 |
| [CU5](#CU5) | 14.0.3023.8 | 2018 3 |
| [CU4](#CU4) | 14.0.3022.28 | 2018 2 |
| [CU3](#CU3) | 14.0.3015.40 | 1-2018 |
| [CU2](#CU2) | 14.0.3008.27 | 11-2017 |
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <a id="cuinstall"></a> 누적 업데이트를 설치 하는 방법

구성한 경우 누적 업데이트 저장소에서는 최신 누적 업데이트 패키지를 SQL Server의 새 설치를 수행할 때 발생 합니다. 누적 업데이트 저장소에는 Linux에서 SQL Server에 대 한 모든 패키지 설치 아티클에 대 한 기본값입니다. 저장소 구성에 대 한 자세한 내용은 참조 [Linux에서 SQL Server에 대 한 저장소를 구성](sql-server-linux-change-repo.md)합니다.

기존 SQL Server 패키지를 업데이트 하는 경우에 각 패키지를 최신 누적 업데이트에 대 한 적절 한 업데이트 명령을 실행 합니다. 각 패키지에 대 한 특정 업데이트 지침은 다음 설치 가이드를 참조 합니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [SQL Server 에이전트를 사용 하도록 설정](sql-server-linux-setup-sql-agent.md)

## <a id="CU6"></a> Cu6 적용 (2018 년 4 월)

이 SQL Server 2017의 누적 업데이트 6 (cu6)가 적용 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3025.34입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3025.34-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3025.34-3 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3025.34-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (2018 년 3 월)

이 SQL Server 2017의 누적 업데이트 5 (CU5) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3023.8입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643)합니다.

### <a name="known-upgrade-issue"></a>알려진된 업그레이드 문제

이전 릴리스에서 CU5를 업그레이드 하면 SQL Server는 다음 오류로 시작에 실패할 수 있습니다.

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

이 오류를 해결 하려면 SQL Server 에이전트를 사용 하도록 설정 하 고 다음 명령을 사용 하 여 SQL Server를 다시 시작 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3023.8-5 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3023.8-5 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3023.8-5 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (2 월 2018)

이 SQL Server 2017의 누적 업데이트 4 (CU4) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3022.28입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/en-us/help/4056498 ](https://support.microsoft.com/en-us/help/4056498)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> C u 4에서 기준으로 SQL Server 에이전트는 더 이상 별도 패키지로 서 설치 됩니다. 엔진이 패키지와 함께 설치 하 고 사용 하도록 설정 해야 합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3022.28-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3022.28-2 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3022.28-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU3"></a> C u 3 (1 월 2018)

이 SQL Server 2017의 누적 업데이트 3 (CU3) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3015.40입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/en-us/help/4052987 ](https://support.microsoft.com/en-us/help/4052987)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3015.40-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3015.40-1 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3015.40-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (2017 년 11 월)

이 SQL Server 2017의 누적 업데이트 2 (CU2) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3008.27입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3008.27-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3008.27-1 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3008.27-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (2017 년 10 월)

이 SQL Server 2017의 누적 업데이트 1 (CU1) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3006.16입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3006.16-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3006.16-3 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3006.16-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (2017 년 10 월)

SQL Server 2017의 GA (일반 공급) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.1000.169입니다.

### <a name="package-details"></a>패키지 세부 정보

패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고는 다음과 같은 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.1000.169-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.1000.169-2 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.1000.169-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> 지원 되지 않는 기능 및 서비스

다음 기능 및 서비스에서 사용할 수 없는 Linux의 GA 릴리스 시입니다. 이러한 기능의 지원 시간이 지남에 따라 점점 더 사용할 수 있습니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | 타사 연결을 통해 분산된 쿼리 |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL 등). |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| &nbsp; | 버퍼 풀 확장 |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, 큐 판독기, SSIS, SSAS, SSRS |
| &nbsp; | 경고 |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | 변경 데이터 캡처 |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| &nbsp; | 연결 된 서버에 대 한 AD 인증 | 
| &nbsp; | 가용성 그룹 (Ag)에 대 한 AD 인증 | 
| &nbsp; | AD 타사 도구 (Centrify, Vintela, Powerbroker) | 
| **Services** | SQL Server Browser |
| &nbsp; | SQL Server R 서비스 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | 데이터베이스 엔진 서비스 |
| &nbsp; | Master  Data  Services |
| &nbsp; | Distributed Transaction Coordinator (DTC) |

## <a name="known-issues"></a>알려진 문제

다음 섹션에서는 Linux에서 SQL Server 2017의 GA (일반 공급) 릴리스의 알려진된 문제에 설명 합니다.

#### <a name="general"></a>일반

- SQL Server 2017의 GA 릴리스에 대 한 업그레이드 이상 CTP 2.1 에서만에서 지원 됩니다. 

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

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 Linux에서 실행 중인 SQL Server에서 지원 되지 않습니다. SQL Server 연결 된 서버에 SQL Server에서 DTC를 포함 하지 않는 한 사용할 수 있습니다. 자세한 내용은 참조 [Linux에서 실행 중인 SQL Server에서 Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 지원 되지 않습니다](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)합니다.

- (암호 그룹)에 대 한 보안 TLS (전송 계층) 일부 알고리즘은 Linux에서 SQL Server에서는 제대로 작동 하지 않습니다. 그러면 연결 오류가 SQL Server에 연결 하려고 할 때 뿐만 아니라 문제가 높은 가용성 그룹의 복제본 간의 연결을 설정 합니다.

   - **해상도**: 수정 된 **mssql.conf** linux에서 다음을 수행 하 여 문제가 있는 암호 그룹을 사용 하지 않으려면 SQL Server에 대 한 구성 스크립트:

      1. 다음 /var/opt/mssql/mssql.conf를 추가 합니다.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 다음 명령을 사용 하 여 SQL Server를 다시 시작 합니다.

      ```bash
      sudo systemctl restart mssql-server
      ```

- SQL Server 2014 데이터베이스 메모리 내 OLTP를 사용 하는 창에 SQL Server 2017 linux에서 복원할 수 없습니다. 메모리 내 OLTP를 사용 하는 SQL Server 2014 데이터베이스를 복원 하려면 먼저 데이터베이스를 업그레이드 SQL Server 2016 또는 Windows에서 SQL Server 2017 이동 하기 전에 SQL Server로 Linux에서 백업/복원 또는 분리/연결을 통해.

- 사용자 권한 **ADMINISTER BULK OPERATIONS** 이 이번에 Linux에서 지원 되지 않습니다.

#### <a name="networking"></a>네트워킹

Sqlservr 프로세스 예: 연결 된 서버 또는 가용성 그룹의에서 아웃 바운드 TCP 연결을 포함 하는 기능에는 다음 두 조건이 모두 충족 될 경우 작동 하지 않을 수 없습니다.:

1. 대상 서버는 호스트 이름 및 IP 주소가 아니라로 지정 됩니다.

1. 원본 인스턴스의 커널에서 사용 하지 않도록 설정 하는 i p v 6에 있습니다. 시스템에 커널에서 사용할 수는 IPv6 있는지를 확인 하려면 다음 모든 테스트를 통과 해야 합니다.

   - `cat /proc/cmdline` 현재 커널 부팅 cmdline를 인쇄 됩니다. 출력 없어야 `ipv6.disable=1`합니다.
   - / Proc/sys/net/ipv6/디렉터리가 있어야 합니다.
   - 호출 하는 C 프로그램 `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` 는 성공적으로-는 syscall는 fd 반환 해야 합니다! =-1 및 EAFNOSUPPORT와 함께 실패 하지 않습니다.

정확한 오류는 기능에 따라 달라 집니다. 연결 된 서버에이 로그인 제한 시간 오류도 매니페스트합니다. 가용성 그룹에 대 한는 `ALTER AVAILABILITY GROUP JOIN` 다운로드 구성 제한 시간 오류로 5 분 후에 보조 데이터베이스에서 DDL 실패 합니다.

이 문제를 해결 하려면 다음 중 하나를 수행 합니다.

1. TCP 연결의 대상을 지정 하려면 호스트 이름 대신 Ip를 사용 합니다.

1. 제거 하 여 커널에서 i p v 6을 사용 하도록 설정 `ipv6.disable=1` 부팅 cmdline에서 합니다. 이 작업을 수행 하는 방법은 grub와 같은 부팅 로더와 Linux 배포에 따라 다릅니다. 비활성화할 수는 IPv6을 하려는 경우 비활성화할 수 있습니다 여전히 설정 하 여 `net.ipv6.conf.all.disable_ipv6 = 1` 에 `sysctl` 구성 (예: `/etc/sysctl.conf`). 이 여전히 시스템의 네트워크 어댑터 IPv6 주소를 얻지 못하도록 방지 않지만 sqlservr 기능만 작동 하도록 합니다.

#### <a name="network-file-system-nfs"></a>네트워크 파일 시스템 (NFS)
사용 하는 경우 **네트워크 파일 시스템 (NFS)** 프로덕션 환경에서 원격 공유에는 다음과 같은 지원 요구 사항을 확인 하세요.

- 사용 하 여 NFS 버전 **4.2 이상**합니다. 이전 버전의 NFS fallocate, 최신 파일 시스템에 공통 스파스 파일 만들기 등 필수 기능을 지원 하지 않습니다.
- 만 찾습니다는 **/var/opt/mssql** NFS 탑재 디렉터리입니다. SQL Server 시스템 이진 파일 등의 기타 파일 지원 되지 않습니다.
- 원격 공유 마운트할 때 NFS 클라이언트 'nolock' 옵션을 사용 하도록 확인 합니다.

#### <a name="localization"></a>지역화

- 로캘에서 영어가 아닌 (en_us) 설치 하는 동안 bash 세션/터미널에 utf-8 인코딩을 사용 해야 합니다. ASCII 인코딩을 사용 하는 경우 다음과 유사한 오류가 표시 될 수 있습니다.

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   인코딩을 u t F-8을 사용할 수 없는 경우 언어 선택 지정 하려면 MSSQL_LCID 환경 변수를 사용 하 여 설치 프로그램을 실행 합니다.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 경우 mssql conf 설치 프로그램을 실행 하 고 확장 문자가 잘못 된 SQL Server의 영어 이외의 설치를 수행 하는 지역화 된 텍스트를 "구성 SQL Server …" 후 표시 됩니다. 또는 비 라틴 기반된 설치에 대 한 문장에는 누락 될 수 있습니다 완전히 합니다. 누락 된 문장에는 다음의 지역화 된 문자열에 표시 됩니다: "라이선스 PID가 성공적으로 처리 합니다.  새 버전은 [\<이름\> 버전] "입니다. 이 문자열은 정보 제공 목적 으로만,에 대 한 출력 하 고 SQL Server 누적 업데이트는이 모든 언어에 대 한 처리 합니다. 어떤 방식으로든에서 SQL Server의 성공적인 설치에는 영향을 주지 않습니다. 

#### <a name="full-text-search"></a>전체 텍스트 검색

- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스와 함께 제공 합니다. 지원 되는 필터 목록에 대 한 참조 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

#### <a id="ssis"></a> SSIS(SQL Server Integration Services)

- **mssql 서버는** 패키지가이 릴리스에서 SUSE에서 지원 되지 않습니다. Ubuntu 및 Red Hat Enterprise Linux (RHEL) 현재 지원 됩니다.

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

목록이 현재 지원 되지 않거나 제한 사항과 함께 지원 되는 기본 제공 SSIS 구성 요소에 대 한 참조 [Linux에서 SSIS에 대 한 알려진된 문제 및 제한](sql-server-linux-ssis-known-issues.md#components)합니다.

Linux에서 SSIS에 대 한 자세한 내용은 다음 문서를 참조 합니다.
-   [Linux에 대 한 SSIS 지원 블로그 게시물 발표](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)합니다.
-   [Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)

Linux에서 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용할 수 없습니다.

- 데이터 웨어하우스 MDW (관리) 및 데이터 수집기 SSMS에서 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소와 Linux 작동 하지 않습니다. SQL 로그인 등의 다른 옵션으로 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 퀵 스타트를 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

자주 묻는 질문에 대 한 답을 참조 하십시오.는 [Linux FAQ에서 SQL Server](sql-server-linux-faq.md)합니다.
