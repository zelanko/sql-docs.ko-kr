---
title: SQL Server 2017 on Linux에 대한 릴리스 정보 | Microsoft Docs
description: 이 항목에서는 Linux에서 동작하는 SQL Server 2017에 대한 릴리스 정보 및 지원하는 기능을 포함합니다. 릴리스 정보는 가장 최신 릴리스 및 몇 가지 이전 릴리스를 포함합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: feba6aca66d4428733b11db778c6b590dfde9f8b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290779"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux의 SQL Server 2017 릴리스 정보

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 릴리스 정보에 적용할 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] Linux를 실행 합니다. 이 문서는 각 릴리스에 대 한 섹션으로 구분 됩니다. GA 릴리스는 지원 가능성을 자세히 설명 있고 알려진 문제를 나열 합니다. 각 CU (누적 업데이트) 또는 일반 배포 릴리스 (GDR)에 CU 변경 뿐만 아니라 Linux 패키지 다운로드에 대 한 링크를 설명 하는 기술 지원 문서에 대 한 링크가 있습니다.

> [!TIP]
> 이러한 릴리스 정보는 특히 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 해제 합니다. 새에 대 한 자세한 내용은 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 참조 하세요 [Linux에서 SQL Server 2019 미리 보기에 대 한 릴리스](sql-server-linux-release-notes-2019.md?view=sql-server-ver15)합니다.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 또는 7.6 Server | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8 + Windows, Mac 또는 Linux에서 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 검토 합니다 [시스템 요구 사항](sql-server-linux-setup.md#system) 에 대 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux. 에 대 한 최신 지원 정책에 대 한 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]를 참조 합니다 [Microsoft SQL Server에 대 한 기술 지원 정책을](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)합니다.

## <a name="tools"></a>Tools

대부분의 기존 클라이언트 대상으로 하는 도구 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 대상으로 원활 하 게 지정할 수 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux를 실행 합니다. 일부 도구는 Linux에서 작동 하도록 특정 버전 요구 사항이 있을 수 있습니다. 전체 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구를 참조 하세요 [SQL Tools 및 SQL Server 유틸리티](../tools/overview-sql-tools.md)합니다.

## <a name="release-history"></a>릴리스 기록

다음 표에서 대 한 릴리스 기록을 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다.

| 릴리스               | 버전       | 릴리스 날짜 |
|-----------------------|---------------|--------------|
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a> 업데이트를 설치 하는 방법

CU 리포지토리를 구성한 경우 (**mssql server 2017**)의 최신 CU를 갖게 됩니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 새 설치를 수행 하는 경우 패키지 있습니다. 모든 패키지에 대 한 설치 문서에 대 한 CU 리포지토리는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux. GDR 리포지토리를 구성한 경우 (**mssql server-2017 gdr**), 조지아 이후 발표 된 중요 보안 업데이트에 한 해 Docker 컨테이너 CU 또는 GDR 업데이트를 필요로 하는 경우에 대 한 공식 이미지를 참조 하세요 [Docker 엔진에 대 한 Linux의 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server)합니다. 리포지토리 구성에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server에 대 한 리포지토리를 구성](sql-server-linux-change-repo.md)합니다.

기존 업데이트 하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 패키지를 최신 CU를 가져오려는 각 패키지에 대 한 적절 한 업데이트 명령을 실행 합니다. 각 패키지에 대 한 특정 업데이트 지침은 다음 설치 가이드를 참조 합니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지를 설치 합니다.](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [SQL Server 에이전트를 사용 하도록 설정](sql-server-linux-setup-sql-agent.md)

## <a id="CU13"></a> CU13 (2018 년 12 월)

누적 업데이트 13 (CU13) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3048.4 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4466404 ](https://support.microsoft.com/help/4466404)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3048.4-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3048.4-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3048.4-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12 (2018 년 10 월)

누적 업데이트 12 (CU12) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3045.24 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4464082 ](https://support.microsoft.com/help/4464082)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3045.24-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3045.24-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3045.24-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11 (9 월 2018)

누적 업데이트 11 (CU11) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3038.14 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4462262 ](https://support.microsoft.com/help/4462262)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3038.14-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3038.14-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3038.14-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (2018 년 8 월)

누적 업데이트 10 (CU10) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3037.1 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4342123 ](https://support.microsoft.com/help/4342123)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3037.1-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3037.1-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3037.1-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> Cu9까지 포함-GDR2 (2018 년 8 월)

또한 이전에 릴리스된 CU (cu9까지 포함)를 포함 하는 보안 업데이트에 대 한 이것이 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3035.2 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4293805 ](https://support.microsoft.com/help/4293805)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3035.2-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM 패키지 | 14.0.3035.2-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3035.2-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (2018 년 8 월)

이 GDR2 (및 GDR1) 보안 수정 프로그램에 대 한 포함 하는 보안 업데이트 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다.  [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.2002.14 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4293803 ](https://support.microsoft.com/help/4293803)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.2002.14-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.2002.14-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.2002.14-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> Cu9까지 포함 합니다 (2018 년 7 월)

누적 업데이트 9(cu9) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3030.27 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4341265 ](https://support.microsoft.com/help/4341265)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3030.27-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3030.27-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3030.27-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (2018 년 6 월)

누적 업데이트 8 (CU8) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3029.16 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4338363 ](https://support.microsoft.com/help/4338363)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3029.16-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3029.16-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3029.16-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (2018 년 5 월)

누적 업데이트 7 (CU7) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3026.27 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4229789 ](https://support.microsoft.com/help/4229789)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3026.27-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3026.27-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3026.27-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (2018 년 4 월)

누적 업데이트 6 (CU6) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3025.34 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3025.34-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3025.34-3 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3025.34-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (2018 년 3 월)

누적 업데이트 5(cu5) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3023.8 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643)합니다.

### <a name="known-upgrade-issue"></a>알려진된 업그레이드 문제

이전 릴리스에서 업그레이드 CU5, 하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다음 오류로 인해 시작 하지 못할 수 있습니다.

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

이 오류를 해결 하려면 SQL Server 에이전트를 사용 하도록 설정 하 고 다시 시작 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다음 명령을 사용 하 여:

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

누적 업데이트 4 (CU4) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3022.28 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4056498 ](https://support.microsoft.com/help/4056498)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU4에서 현재 SQL Server 에이전트는 더 이상 별도 패키지로 설치 됩니다. 엔진 패키지와 함께 설치 되 고 사용 하도록 설정 해야 합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3022.28-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3022.28-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3022.28-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (2018 년 1 월)

이 보안에 대 한 수정 GDR1 포함 하는 보안 업데이트 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.2000.63 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4057122 ](https://support.microsoft.com/help/4057122)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.2000.63-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.2000.63-3 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.2000.63-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3 (2018 년 1 월)

누적 업데이트 3 (CU3) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3015.40 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4052987 ](https://support.microsoft.com/help/4052987)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3015.40-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3015.40-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3015.40-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (2017 년 11 월)

누적 업데이트 2(cu2) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3008.27 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3008.27-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3008.27-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3008.27-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (2017 년 10 월)

누적 업데이트 1(cu1) 릴리스입니다 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.3006.16 합니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하세요 [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3006.16-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3006.16-3 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트의 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3006.16-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 에이전트의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (2017 년 10 월)

이 GA (일반 공급) 릴리스의 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 이 릴리스에 대 한 버전이 14.0.1000.169 합니다.

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

다음 기능 및 서비스에서 사용할 수 없는 Linux GA 릴리스 시입니다. 이러한 기능의 지원 시간이 지남에 따라 점점 더 많이 사용 됩니다.

| 영역 | 지원 되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | 변경 데이터 캡처 (SQL Server 에이전트 참조) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | 타사 연결을 사용 하 여 분산된 쿼리 |
| &nbsp; | 이외의 데이터 원본에 연결 된 서버 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | 시스템 확장 저장된 프로시저 (XP_CMDSHELL, 등) |
| &nbsp; | Filetable에서 FILESTREAM |
| &nbsp; | CLR 어셈블리 EXTERNAL_ACCESS 또는 UNSAFE 권한 설정 |
| &nbsp; | Buffer Pool Extension |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, Queue Reader, SSIS, SSAS, SSRS |
| &nbsp; | , |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | CDC(변경 데이터 캡처) |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| &nbsp; | 연결 된 서버에 대 한 AD 인증 | 
| &nbsp; | 가용성 그룹 (Ag)에 대 한 AD 인증 | 
| &nbsp; | AD 타사 도구 (Centrify, Vintela, Powerbroker) | 
| **Services** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master  Data  Services |
| &nbsp; | Distributed Transaction Coordinator (DTC) |

## <a name="known-issues"></a>알려진 문제

GA (일반 공급) 릴리스를 사용 하 여 알려진된 문제를 설명 하는 다음 섹션에서는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] linux.

#### <a name="general"></a>일반

- 호스트 이름의 길이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작거나 설치 요구 사항 15 자 여야 합니다. 

    - **해상도**: 항목 15 자 이하의 /etc/hostname의 이름을 변경 합니다.

- 수동으로 시점의 시스템 시간을 뒤로 설정 하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 내에서 내부 시스템에 업데이트를 중지 하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다.

    - **해상도**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다시 시작합니다.

- 단일 인스턴스 설치만 지원 됩니다.

    - **해상도**: 지정된 된 호스트에서 둘 이상의 인스턴스가 있는 하려는 경우 Vm을 사용 하 여 고려 또는 Docker 컨테이너입니다. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager에 연결할 수 없습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux.

- 기본 언어를 **sa** 로그인 영어입니다.

    - **해상도**: 언어를 변경 합니다 **sa** 사용 하 여 로그인 합니다 **ALTER LOGIN** 문입니다.

#### <a name="databases"></a>데이터베이스

- Mssql conf 유틸리티를 사용 하 여 master 데이터베이스를 이동할 수 없습니다. Mssql 구성이 사용 하 여 다른 시스템 데이터베이스를 이동할 수 있습니다.

- 백업한 데이터베이스를 복원 하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 Windows를 사용 해야 합니다 **WITH MOVE** Transact SQL 문 절.

- Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 지원 되지 않습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux를 실행 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DTC을 포함 하지 않으면 연결 된 서버 지원 됩니다. 자세한 내용은 [Linux에서 실행 되는 SQL Server에서 Microsoft Distributed Transaction Coordinator 서비스를 필요로 하는 분산 트랜잭션 지원 되지 않습니다](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)합니다.

- 전송 계층 보안 (TLS)에 대 한 특정 알고리즘 (암호 그룹) 사용 하 여 제대로 작동 하지 않습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux. 에 연결 하려고 할 때이 인해 연결 오류가 발생할에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 높은 가용성 그룹의 복제본 간의 연결을 설정 하는 문제 뿐만 아니라 합니다.

   - **해상도**: 수정 된 **mssql.conf** 에 대 한 구성 스크립트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 문제가 있는 암호 그룹을 사용 하지 않으려면 다음을 수행 하 여 Linux에서:

      1. /Var/opt/mssql/mssql.conf에 다음을 추가 합니다.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 다시 시작 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다음 명령을 사용 합니다.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 메모리 내 OLTP를 사용 하는 Windows에서 데이터베이스를 복원할 수 없기 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] linux. 복원 하는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 메모리 내 OLTP를 사용 하는 데이터베이스에 데이터베이스를 먼저 업그레이드 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 하도록 이동 하기 전에 Windows에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업/복원 또는 분리/연결을 통해 Linux에서.

- 사용자 권한 **ADMINISTER BULK OPERATIONS** 지금은 Linux에서 지원 되지 않습니다.

#### <a name="networking"></a>네트워킹

다음 조건을 모두 충족 될 경우에 연결 된 서버 또는 가용성 그룹과 같은 sqlservr 프로세스에서 아웃 바운드 TCP 연결을 포함 하는 기능은 작동 하지 않을 수 있습니다.

1. 대상 서버 호스트 이름과 IP 주소가 아니라로 지정 됩니다.

1. 원본 인스턴스에 있는 커널을 사용 하지 않도록 설정 하는 IPv6에 있습니다. 시스템 IPv6 커널에서 사용 하도록 설정한 경우를 확인 하려면 다음 모든 테스트가 통과 해야 합니다.

   - `cat /proc/cmdline` 현재 커널 부팅 명령줄에 인쇄 됩니다. 출력 없어야 `ipv6.disable=1`합니다.
   - / Proc/sys/net/i p v 6/디렉터리가 있어야 합니다.
   - 호출 하는 C 프로그램 `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` 성공-syscall는 fd를 반환 해야 합니다! =-1 및 EAFNOSUPPORT 실패 하지 않습니다.

정확한 오류는 기능에 따라 달라 집니다. 연결 된 서버에 대 한이 로그인 제한 시간 오류로 매니페스트 합니다. 가용성 그룹에 대 한는 `ALTER AVAILABILITY GROUP JOIN` 다운로드 구성 제한 시간 오류를 5 분 후에 보조 데이터베이스에서 DDL는 실패 합니다.

이 문제를 해결 하려면 다음 중 하나를 수행 합니다.

1. TCP 연결의 대상을 지정 하려면 호스트 이름 대신 Ip를 사용 합니다.

1. 제거 하 여 커널에는 IPv6를 활성화 `ipv6.disable=1` 부팅 명령줄에서. 이 작업을 수행 하는 방법은 배포와 같은 grub 부팅 로더를 Linux 배포에 따라 달라 집니다. 사용 하지 않도록 설정할 IPv6 않으려면 비활성화할 수 있습니다 계속 설정 하 여 `net.ipv6.conf.all.disable_ipv6 = 1` 에 `sysctl` 구성 (예: `/etc/sysctl.conf`). 이 여전히 시스템의 네트워크 어댑터 IPv6 주소를 가져오는 없지만 sqlservr 기능만 작동 하도록 허용 합니다.

#### <a name="network-file-system-nfs"></a>네트워크 파일 시스템 (NFS)
사용 하는 경우 **네트워크 파일 시스템 (NFS)** 프로덕션 환경에서 원격 공유 다음 지원 요구 사항을 note 합니다.

- 사용 하 여 NFS 버전 **4.2 이상**합니다. 이전 버전의 NFS fallocate 및 스파스 파일 만들기, 최신 파일 시스템에 공통적으로 적용 등 필수 기능을 지원 하지 않습니다.
- 만 찾습니다 합니다 **/var/opt/mssql** NFS 탑재 디렉터리입니다. 와 같은 다른 파일을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 이진 파일을 사용할 수 없습니다.
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

- Mssql-conf를 실행 하는 경우의 영어 이외의 설치를 수행 하 고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 잘못 된 확장 된 문자 "구성 SQL Server..." 지역화 된 텍스트를 다음에 표시 됩니다. 비 라틴 기반된 설치에 대 한 문장 누락 될 수 있습니다 또는 완전히 합니다. 누락 된 문장에는 다음의 지역화 된 문자열을 표시 되어야 합니다. "라이선싱 PID가 성공적으로 처리 합니다. 새 버전은 [\<이름을\> 버전] "입니다. 이 문자열은 정보 제공 목적 으로만, 한 다음 출력 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 누적 업데이트는이 모든 언어에 대 한 주소입니다. 이 성공적으로 설치에는 영향을 주지 않습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 어떤 방식으로든에서 합니다. 

#### <a name="full-text-search"></a>전체 텍스트 검색

- 일부 필터는 Office 문서에 대 한 필터를 포함 하 여이 릴리스에서 사용할 수 있습니다. 지원 되는 필터의 목록을 참조 하세요 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)합니다.

#### <a id="ssis"></a> SSIS(SQL Server Integration Services)

- 합니다 **mssql server는** 패키지가이 릴리스에서 SUSE에 지원 되지 않습니다. Ubuntu 및 Red Hat Enterprise Linux (RHEL) 현재 지원 됩니다.

- 사용 하 여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Linux CTP 2.1 새로 고침 이상 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지는 Linux의 ODBC 연결을 사용할 수 있습니다. 이 기능을 사용 하 여 테스트를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 MySQL ODBC 드라이버와 이지만 ODBC 사양을 따르는 유니코드 ODBC 드라이버를 사용 하도 필요 합니다. 디자인 타임에 ODBC 데이터에 연결할 DSN 또는 연결 문자열을 제공할 수 있습니다. Windows 인증을 사용할 수도 있습니다. 자세한 내용은 참조는 [블로그 Linux의 ODBC 지원 발표 게시물](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

- Linux에서 SSIS 패키지를 실행할 때 다음과 같은 기능이이 릴리스에서 지원 되지 않습니다.
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그 데이터베이스
  - SQL 에이전트에서 예약 된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 규모 확장
  - Azure Feature Pack for SSIS
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

현재 지원 되지 않거나 제한 사항과 함께 지원 되는 기본 제공 SSIS 구성 요소 목록을 참조 하세요 [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md#components)합니다.

Linux에서 SSIS에 대 한 자세한 내용은 다음 문서를 참조 합니다.
-   [Linux에 대 한 SSIS 지원 블로그 게시물 발표](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)합니다.
-   [Linux의 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SSMS(SQL Server Management Studio)

다음 제한 사항이 적용 됩니다 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에 연결 하는 Windows에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux.

- 유지 관리 계획을 사용 하는 것이 없습니다.

- 관리 데이터 웨어하우스 (MDW) 및 데이터 수집기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 지원 되지 않습니다. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Windows 인증 또는 Windows 이벤트 로그 옵션 있는 UI 구성 요소는 Linux와 함께 작동 하지 않습니다. SQL 로그인 등의 다른 옵션을 사용 하 여 이러한 기능을 계속 사용할 수 있습니다. 

- 유지 하려면 로그 파일의 수를 수정할 수 없습니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작을 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

자주 묻는 질문에 대한 답변은, [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.
