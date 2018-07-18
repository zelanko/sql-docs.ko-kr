---
title: SQL Server 2017 on Linux에 대한 릴리스 정보 | Microsoft Docs
description: 이 항목에서는 Linux에서 동작하는 SQL Server 2017에 대한 릴리스 정보 및 지원하는 기능을 포함합니다. 릴리스 정보는 가장 최신 릴리스 및 몇 가지 이전 릴리스를 포함합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 85fb0060a7143aa77cd5495a6140a33d5ac881cc
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854365"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux의 SQL Server 2017 릴리스 정보

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 릴리스 정보는 Linux에서 실행 되는 SQL Server 2017로 적용 됩니다. 이 문서는 각 릴리스에 대 한 섹션으로 구분 됩니다. GA 릴리스는 지원 가능성을 자세히 설명 있고 알려진 문제를 나열 합니다. 각 CU (누적 업데이트) 릴리스에 CU 변경 뿐만 아니라 Linux 패키지 다운로드에 대 한 링크를 설명 하는 기술 지원 문서에 대 한 링크가 있습니다.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 또는 7.4 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8 + Windows, Mac 또는 Linux에서 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 다음을 검토 합니다 [시스템 요구 사항](sql-server-linux-setup.md#system) Linux의 SQL Server에 대 한 합니다. SQL Server 2017에 대 한 최신 지원 정책을 참조 합니다 [Microsoft SQL Server에 대 한 기술 지원 정책을](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)합니다.

## <a name="tools"></a>Tools

SQL Server를 대상으로 하는 대부분의 기존 클라이언트 도구는 Linux에서 실행 중인 SQL Server를 대상 원활 하 게 수 있습니다. 일부 도구는 Linux에서 작동 하도록 특정 버전 요구 사항이 있을 수 있습니다. SQL Server 도구의 전체 목록을 참조 하세요 [SQL Tools 및 SQL Server 유틸리티](../tools/overview-sql-tools.md)합니다.

## <a name="release-history"></a>릴리스 기록

다음 표에서 SQL Server 2017 릴리스 기록을 나열합니다.

| 릴리스     | 버전       | 릴리스 날짜 |
|-------------|---------------|--------------|
| [CU8](#CU8) | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7) | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6) | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5) | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4) | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3) | 14.0.3015.40  | 2017-01-03   |
| [CU2](#CU2) | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1) | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)   | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a> 누적 업데이트를 설치 하는 방법

구성한 경우 누적 업데이트 리포지토리를 새 설치를 수행 하는 경우에 SQL Server 패키지의 최신 누적 업데이트를 갖게 됩니다. 누적 업데이트 리포지토리는 Linux의 SQL Server에 대 한 모든 패키지 설치 문서에 대 한 기본값입니다. 리포지토리 구성에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server에 대 한 리포지토리를 구성](sql-server-linux-change-repo.md)합니다.

기존 SQL Server 패키지를 업데이트 하는 경우에 최신 누적 업데이트를 가져오려면 각 패키지에 대 한 적절 한 업데이트 명령을 실행 합니다. 각 패키지에 대 한 특정 업데이트 지침은 다음 설치 가이드를 참조 합니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지를 설치 합니다.](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [SQL Server 에이전트를 사용 하도록 설정](sql-server-linux-setup-sql-agent.md)

## <a id="CU8"></a> CU8 (2018 년 6 월)

이 SQL Server 2017 누적 업데이트 8 (CU8) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3029.16 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/en-us/help/4229789 ](https://support.microsoft.com/en-us/help/4229789)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3029.16-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3029.16-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3029.16-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (2018 년 5 월)

이 SQL Server 2017 누적 업데이트 7 (CU7) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3026.27 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/en-us/help/4229789 ](https://support.microsoft.com/en-us/help/4229789)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3026.27-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3026.27-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3026.27-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (2018 년 4 월)

이 SQL Server 2017 누적 업데이트 6 (CU6) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3025.34 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3025.34-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3025.34-3 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3025.34-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (2018 년 3 월)

이 SQL Server 2017 누적 업데이트 5(cu5) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3023.8 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643)합니다.

### <a name="known-upgrade-issue"></a>알려진된 업그레이드 문제

이전 릴리스에서 CU5를 업그레이드 하면 SQL Server 다음 오류로 시작에 실패할 수 있습니다.

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

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3023.8-5 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3023.8-5 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3023.8-5 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (2018 년 2 월)

이 SQL Server 2017 누적 업데이트 4 (CU4) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3022.28 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/en-us/help/4056498 ](https://support.microsoft.com/en-us/help/4056498)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU4에서 현재 SQL Server 에이전트는 더 이상 별도 패키지로 설치 됩니다. 엔진 패키지와 함께 설치 되 고 사용 하도록 설정 해야 합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3022.28-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3022.28-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3022.28-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU3"></a> CU3 (2018 년 1 월)

이 SQL Server 2017 누적 업데이트 3 (CU3) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3015.40 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/en-us/help/4052987 ](https://support.microsoft.com/en-us/help/4052987)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3015.40-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3015.40-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3015.40-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (2017 년 11 월)

이 SQL Server 2017 누적 업데이트 2(cu2) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3008.27 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3008.27-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3008.27-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3008.27-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (2017 년 10 월)

이 SQL Server 2017 누적 업데이트 1(cu1) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3006.16 됩니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3006.16-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3006.16-3 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3006.16-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (2017 년 10 월)

이 SQL Server 2017의 일반 가용성 (GA) 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.1000.169 됩니다.

### <a name="package-details"></a>패키지 세부 정보

패키지 세부 정보 및 Debian 및 RPM 패키지를 다운로드 위치는 다음 표에 나열 됩니다. 참고를 다음 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지를 설치 합니다.](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지를 설치 합니다.](sql-server-linux-setup-sql-agent.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.1000.169-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.1000.169-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.1000.169-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> 지원 되지 않는 기능 및 서비스

다음 기능 및 서비스에서 사용할 수 없는 Linux GA 릴리스 시입니다. 이 작업을 수행 하는 방법은 배포와 같은 grub 부팅 로더를 Linux 배포에 따라 달라 집니다.

| 영역 | 사용 하지 않도록 설정할 IPv6 않으려면 비활성화할 수 있습니다 계속 설정 하 여  에  구성 (예: ). |
|-----|-----|
| **이 여전히 시스템의 네트워크 어댑터 IPv6 주소를 가져오는 없지만 sqlservr 기능만 작동 하도록 허용 합니다.** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | 네트워크 파일 시스템 (NFS) |
| &nbsp; | Polybase |
| &nbsp; | 사용 하는 경우 네트워크 파일 시스템 (NFS) 프로덕션 환경에서 원격 공유 다음 지원 요구 사항을 note 합니다. |
| &nbsp; | 사용 하 여 NFS 버전 4.2 이상합니다. |
| &nbsp; | 이전 버전의 NFS fallocate 및 스파스 파일 만들기, 최신 파일 시스템에 공통적으로 적용 등 필수 기능을 지원 하지 않습니다. |
| &nbsp; | 만 찾습니다 합니다 /var/opt/mssql NFS 탑재 디렉터리입니다. |
| &nbsp; | SQL Server 시스템 이진 파일을 같은 다른 파일을 사용할 수 없습니다. |
| &nbsp; | Buffer Pool Extension |
| **SQL Server 에이전트** |  된 NFS 클라이언트 원격 공유를 탑재 하는 경우 'nolock' 옵션을 사용 하는 것을 확인 합니다. |
| &nbsp; | , |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | 변경 데이터 캡처 |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| &nbsp; | 사용자 로캘이 영어가 아니므로 (en_us) 설치 하는 동안, bash 세션/터미널에서 utf-8 인코딩을 사용 해야 합니다. | 
| &nbsp; | ASCII 인코딩을 사용 하는 경우 다음과 유사한 오류가 표시 될 수 있습니다. | 
| &nbsp; | U t F-8 인코딩를 사용할 수 없는 경우 선택한 언어에 따라 지정 MSSQL_LCID 환경 변수를 사용 하 여 설치 프로그램을 실행 합니다. | 
| **Services** | SQL Server Browser |
| &nbsp; | 경우 mssql-conf를를 실행 하 고 확장 문자가 잘못 된 SQL Server의 영어 이외의 설치를 수행 하는 지역화 된 텍스트를 "구성 SQL Server..." 후 표시 됩니다. |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | 데이터베이스 엔진 서비스 |
| &nbsp; | Master  Data  Services |
| &nbsp; | 비 라틴 기반된 설치에 대 한 문장 누락 될 수 있습니다 또는 완전히 합니다. |

## <a name="known-issues"></a>알려진 문제

누락 된 문장에는 다음의 지역화 된 문자열 표시 됩니다: "라이선싱 PID가 성공적으로 처리 합니다.

#### <a name="general"></a>일반

- 새 버전은 [이름을 버전] "입니다. 

- 이 문자열은 정보 제공만을 위한 출력 하 고 SQL Server 누적 업데이트는이 모든 언어에 대 한 해결 합니다. 

    - **어떤 방식으로 SQL Server의 성공적인 설치에는 영향을 주지 않습니다.

- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스에서 사용할 수 있습니다.

    - **지원 되는 필터의 목록을 참조 하세요 **Linux에서 SQL Server 전체 텍스트 검색 설치**합니다.

- 합니다 mssql server는 패키지가이 릴리스에서 SUSE에 지원 되지 않습니다.

    - **Ubuntu 및 Red Hat Enterprise Linux (RHEL) 현재 지원 됩니다. 

- 이상 Linux CTP 2.1 새로 고침에서 SSIS를 사용 하 여 SSIS 패키지는 Linux에서 ODBC 연결을 사용할 수 있습니다.

- 이 기능은 SQL Server 및 MySQL ODBC 드라이버를 사용 하 여 테스트 되었습니다 있지만 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 하 합니다.

    - **디자인 타임에 ODBC 데이터에 연결할 DSN 또는 연결 문자열을 제공할 수 있습니다. Windows 인증을 사용할 수도 있습니다.

#### <a name="databases"></a>데이터베이스

- 자세한 내용은 참조는 블로그 Linux의 ODBC 지원 발표 게시물합니다. Linux에서 SSIS 패키지를 실행할 때 다음과 같은 기능이이 릴리스에서 지원 되지 않습니다.

- SSIS 카탈로그 데이터베이스

- SQL 에이전트에서 예약 된 패키지 실행 타사 구성 요소 SSIS Scale Out

- Azure Feature Pack for SSIS Hadoop 및 HDFS 지원

   - **현재 지원 되지 않거나 제한 사항과 함께 지원 되는 기본 제공 SSIS 구성 요소 목록을 참조 하세요 **제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제**합니다.

      1. Linux에서 SSIS에 대 한 자세한 내용은 다음 문서를 참조 합니다.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Linux에 대 한 SSIS 지원 블로그 게시물 발표합니다.

      ```bash
      sudo systemctl restart mssql-server
      ```

- Linux의 SQL Server Integration Services (SSIS)를 설치 합니다. < a = "ssms" > SQL Server Management Studio (SSMS)

- Linux의 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

#### <a name="networking"></a>네트워킹

유지 관리 계획을 사용 하는 것이 없습니다.

1. 관리 데이터 웨어하우스 (MDW) 및 SSMS에서 데이터 수집기가 지원 되지 않습니다.

1. Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소는 Linux와 함께 작동 하지 않습니다. SQL 로그인 등의 다른 옵션을 사용 하 여 이러한 기능을 계속 사용할 수 있습니다.

   - `cat /proc/cmdline` 유지 하려면 로그 파일의 수를 수정할 수 없습니다. 시작 하려면 다음 빠른 시작을 참조 하세요.
   - Red Hat Enterprise Linux 설치
   - SUSE Linux Enterprise Server에 설치

Docker에서 실행 자주 묻는 질문에 답변에 대 한 참조를 의 SQL Server Linux FAQ합니다. 가용성 그룹에 대 한는 `ALTER AVAILABILITY GROUP JOIN` 다운로드 구성 제한 시간 오류를 5 분 후에 보조 데이터베이스에서 DDL는 실패 합니다.

이 문제를 해결 하려면 다음 중 하나를 수행 합니다.

1. TCP 연결의 대상을 지정 하려면 호스트 이름 대신 Ip를 사용 합니다.

1. 제거 하 여 커널에는 IPv6를 활성화 `ipv6.disable=1` 부팅 명령줄에서. 이 작업을 수행 하는 방법은 배포와 같은 grub 부팅 로더를 Linux 배포에 따라 달라 집니다. 사용 하지 않도록 설정할 IPv6 않으려면 비활성화할 수 있습니다 계속 설정 하 여 `net.ipv6.conf.all.disable_ipv6 = 1` 에 `sysctl` 구성 (예: `/etc/sysctl.conf`). 이 여전히 시스템의 네트워크 어댑터 IPv6 주소를 가져오는 없지만 sqlservr 기능만 작동 하도록 허용 합니다.

#### <a name="network-file-system-nfs"></a>네트워크 파일 시스템 (NFS)
사용 하는 경우 **네트워크 파일 시스템 (NFS)** 프로덕션 환경에서 원격 공유 다음 지원 요구 사항을 note 합니다.

- 사용 하 여 NFS 버전 **4.2 이상**합니다. 이전 버전의 NFS fallocate 및 스파스 파일 만들기, 최신 파일 시스템에 공통적으로 적용 등 필수 기능을 지원 하지 않습니다.
- 만 찾습니다 합니다 **/var/opt/mssql** NFS 탑재 디렉터리입니다. SQL Server 시스템 이진 파일을 같은 다른 파일을 사용할 수 없습니다.
- 된 NFS 클라이언트 원격 공유를 탑재 하는 경우 'nolock' 옵션을 사용 하는 것을 확인 합니다.

#### <a name="localization"></a>지역화

- 사용자 로캘이 영어가 아니므로 (en_us) 설치 하는 동안, bash 세션/터미널에서 utf-8 인코딩을 사용 해야 합니다. ASCII 인코딩을 사용 하는 경우 다음과 유사한 오류가 표시 될 수 있습니다.

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   U t F-8 인코딩를 사용할 수 없는 경우 선택한 언어에 따라 지정 MSSQL_LCID 환경 변수를 사용 하 여 설치 프로그램을 실행 합니다.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 경우 mssql-conf를를 실행 하 고 확장 문자가 잘못 된 SQL Server의 영어 이외의 설치를 수행 하는 지역화 된 텍스트를 "구성 SQL Server..." 후 표시 됩니다. 비 라틴 기반된 설치에 대 한 문장 누락 될 수 있습니다 또는 완전히 합니다. 누락 된 문장에는 다음의 지역화 된 문자열 표시 됩니다: "라이선싱 PID가 성공적으로 처리 합니다.  새 버전은 [\<이름을\> 버전] "입니다. 이 문자열은 정보 제공만을 위한 출력 하 고 SQL Server 누적 업데이트는이 모든 언어에 대 한 해결 합니다. 어떤 방식으로 SQL Server의 성공적인 설치에는 영향을 주지 않습니다. 

#### <a name="full-text-search"></a>전체 텍스트 검색

- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스에서 사용할 수 있습니다. 지원 되는 필터의 목록을 참조 하세요 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

#### <a id="ssis"></a> SSIS(SQL Server Integration Services)

- 합니다 **mssql server는** 패키지가이 릴리스에서 SUSE에 지원 되지 않습니다. Ubuntu 및 Red Hat Enterprise Linux (RHEL) 현재 지원 됩니다.

- 이상 Linux CTP 2.1 새로 고침에서 SSIS를 사용 하 여 SSIS 패키지는 Linux에서 ODBC 연결을 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버를 사용 하 여 테스트 되었습니다 있지만 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 하 합니다. 디자인 타임에 ODBC 데이터에 연결할 DSN 또는 연결 문자열을 제공할 수 있습니다. Windows 인증을 사용할 수도 있습니다. 자세한 내용은 참조는 [블로그 Linux의 ODBC 지원 발표 게시물](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

- Linux에서 SSIS 패키지를 실행할 때 다음과 같은 기능이이 릴리스에서 지원 되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약 된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS Scale Out
  - Azure Feature Pack for SSIS
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

현재 지원 되지 않거나 제한 사항과 함께 지원 되는 기본 제공 SSIS 구성 요소 목록을 참조 하세요 [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md#components)합니다.

Linux에서 SSIS에 대 한 자세한 내용은 다음 문서를 참조 합니다.
-   [Linux에 대 한 SSIS 지원 블로그 게시물 발표](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)합니다.
-   [Linux의 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)

#### <a name="-a-idssmsa-sql-server-management-studio-ssms"></a>< a = "ssms" ></a> SQL Server Management Studio (SSMS)

Linux의 SQL Server에 연결 하는 Windows에서 SSMS에 다음과 같은 제한 사항이 적용 됩니다.

- 유지 관리 계획을 사용 하는 것이 없습니다.

- 관리 데이터 웨어하우스 (MDW) 및 SSMS에서 데이터 수집기가 지원 되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션 있는 SSMS UI 구성 요소는 Linux와 함께 작동 하지 않습니다. SQL 로그인 등의 다른 옵션을 사용 하 여 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작을 참조 하세요.

- [Red Hat Enterprise Linux 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

자주 묻는 질문에 답변에 대 한 참조를 [의 SQL Server Linux FAQ](sql-server-linux-faq.md)합니다.
