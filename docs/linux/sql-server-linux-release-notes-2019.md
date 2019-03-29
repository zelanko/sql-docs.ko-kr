---
title: Linux에서 SQL Server 2019 미리 보기 릴리스 정보 | Microsoft Docs
description: 이 문서에서는 Linux에서 실행 되는 SQL Server 2019 미리 보기에 대 한 지원 되는 기능과 릴리스 정보를 포함 합니다. 릴리스 정보는 가장 최신 릴리스 및 몇 가지 이전 릴리스를 포함합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 9c3ee750afe0af5971f571a2a0352397ed8c4f40
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2019
ms.locfileid: "58566572"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>Linux에서 SQL Server 2019 미리 보기에 대 한 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

다음 릴리스 정보는 Linux에서 실행 되는 SQL Server 2019 미리 보기에 적용 합니다. 이 문서는 각 릴리스에 대 한 섹션으로 구분 됩니다. 각 릴리스에 CU 변경 뿐만 아니라 Linux 패키지 다운로드에 대 한 링크를 설명 하는 기술 지원 문서에 대 한 링크가 있습니다.

> [!TIP]
> SQL Server 2019의 새로운 Linux 기능을 알아보려면 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sqllinux)합니다.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 또는 7.6 Server | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8 + Windows, Mac 또는 Linux에서 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 다음을 검토 합니다 [시스템 요구 사항](sql-server-linux-setup.md#system) Linux의 SQL Server에 대 한 합니다. SQL Server 2017에 대 한 최신 지원 정책을 참조 합니다 [Microsoft SQL Server에 대 한 기술 지원 정책을](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)합니다.

## <a name="tools"></a>Tools

SQL Server를 대상으로 하는 대부분의 기존 클라이언트 도구는 Linux에서 실행 중인 SQL Server를 대상 원활 하 게 수 있습니다. 일부 도구는 Linux에서 작동 하도록 특정 버전 요구 사항이 있을 수 있습니다. SQL Server 도구의 전체 목록을 참조 하세요 [SQL Tools 및 SQL Server 유틸리티](../tools/overview-sql-tools.md)합니다.

## <a name="release-history"></a>릴리스 기록

다음 표에서 CTP 릴리스의 SQL Server 2019 미리 보기 릴리스 기록을 나열 합니다.

| 릴리스               | 버전       | 릴리스 날짜 |
|-----------------------|---------------|--------------|
| [CTP 2.4](#CTP24)     | 15.0.1400.75  | 2019-3-27    |
| [CTP 2.3](#CTP23)     | 15.0.1300.359 | 2019-3-01    |
| [CTP 2.2](#CTP22)     | 15.0.1200.24  | 2018-12-11   |
| [CTP 2.1](#CTP21)     | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)     | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> 업데이트를 설치 하는 방법

미리 보기 리포지토리를 구성한 경우 (**mssql-서버-미리 보기**), 새 설치를 수행 하는 경우에 최신 SQL Server CTP 패키지를 갖게 됩니다. Docker 컨테이너 이미지에 필요한 경우에 대 한 공식 이미지를 참조 하세요 [Docker 엔진에 대 한 Linux의 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server/)합니다. 리포지토리 구성에 대 한 자세한 내용은 참조 하세요. [Linux의 SQL Server에 대 한 리포지토리를 구성](sql-server-linux-change-repo.md)합니다.

기존 SQL Server 패키지를 업데이트 하는 경우에 최신 CU를 가져오려는 각 패키지에 대 한 적절 한 업데이트 명령을 실행 합니다. 각 패키지에 대 한 특정 업데이트 지침은 다음 설치 가이드를 참조 합니다.

- [SQL Server 패키지를 설치 합니다.](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지를 설치 합니다.](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [Linux에서 SQL Server 2019 미리 보기 Machine Learning Services R 및 Python 지원 설치](sql-server-linux-setup-machine-learning.md)
- [SQL Server 에이전트를 사용 하도록 설정](sql-server-linux-setup-sql-agent.md)

## <a id="CTP24"></a> CTP 2.4 (2019 년 3 월)

CTP 2.4의 알려진된 문제 릴리스 및 다음 섹션에서는 패키지 위치를 제공 합니다. 새 기능에 대 한 자세한 내용은 SQL Server 2019에 Linux에 대 한 자세한 참조를 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1400.75-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1400.75-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1400.75-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재, MSDTC 트랜잭션을 인증 되지 않은 것에 필요 합니다. 예를 들어, Linux의 SQL Server를 Windows에서 SQL Server에서 연결 된 서버를 사용 하거나 Windows 클라이언트 응용 프로그램을 Linux의 SQL Server에 대 한 분산된 트랜잭션을 시작 하는 데 Windows server/client MSDTC 경우 "No 옵션을 사용 하는 데 필요한 인증 필요 "입니다.

## <a id="CTP23"></a> CTP 2.3 (2019 년 2 월)

다음 섹션에서는 패키지 위치를 제공 하 고 릴리스의 알려진된 문제는 CTP 2.3에 대 한 키를 누릅니다. 새 기능에 대 한 자세한 내용은 SQL Server 2019에 Linux에 대 한 자세한 참조를 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1300.359-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1300.359-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1300.359-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재, MSDTC 트랜잭션을 인증 되지 않은 것에 필요 합니다. 예를 들어, Linux의 SQL Server를 Windows에서 SQL Server에서 연결 된 서버를 사용 하거나 Windows 클라이언트 응용 프로그램을 Linux의 SQL Server에 대 한 분산된 트랜잭션을 시작 하는 데 Windows server/client MSDTC 경우 "No 옵션을 사용 하는 데 필요한 인증 필요 "입니다.

## <a id="CTP22"></a> CTP 2.2 (2018 년 12 월)

CTP 2.2의 알려진된 문제 릴리스 및 다음 섹션에서는 패키지 위치를 제공 합니다. 새 기능에 대 한 자세한 내용은 SQL Server 2019에 Linux에 대 한 자세한 참조를 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1200.24-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1200.24-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1200.24-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재, MSDTC 트랜잭션을 인증 되지 않은 것에 필요 합니다. 예를 들어, Linux의 SQL Server를 Windows에서 SQL Server에서 연결 된 서버를 사용 하거나 Windows 클라이언트 응용 프로그램을 Linux의 SQL Server에 대 한 분산된 트랜잭션을 시작 하는 데 Windows server/client MSDTC 경우 "No 옵션을 사용 하는 데 필요한 인증 필요 "입니다.

## <a id="CTP21"></a> CTP 2.1 (2018 년 11 월)

다음 섹션에서는 패키지 위치를 제공 하 고 릴리스의 알려진된 문제는 CTP 2.1에 대 한 키를 누릅니다. 새 기능에 대 한 자세한 내용은 SQL Server 2019에 Linux에 대 한 자세한 참조를 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1100.94-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1100.94-1 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1100.94-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft Distributed Transaction Coordinator

현재, MSDTC 트랜잭션을 인증 되지 않은 것에 필요 합니다. 예를 들어, Linux의 SQL Server를 Windows에서 SQL Server에서 연결 된 서버를 사용 하거나 Windows 클라이언트 응용 프로그램을 Linux의 SQL Server에 대 한 분산된 트랜잭션을 시작 하는 데 Windows server/client MSDTC 경우 "No 옵션을 사용 하는 데 필요한 인증 필요 "입니다.

## <a id="CTP20"></a> CTP 2.0 (9 월 2018)

다음 섹션에서는 패키지 위치를 제공 하 고 릴리스의 알려진된 문제는 CTP 2.0에 대 한 키를 누릅니다. 새 기능에 대 한 자세한 내용은 SQL Server 2019에 Linux에 대 한 자세한 참조를 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)합니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 Debian 및 RPM 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1000.34-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1000.34-2 | [mssql server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1000.34-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[높은 가용성의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[전체 텍스트 검색의 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft Distributed Transaction Coordinator

현재, MSDTC 트랜잭션을 인증 되지 않은 것에 필요 합니다. 예를 들어, Linux의 SQL Server를 Windows에서 SQL Server에서 연결 된 서버를 사용 하거나 Windows 클라이언트 응용 프로그램을 Linux의 SQL Server에 대 한 분산된 트랜잭션을 시작 하는 데 Windows server/client MSDTC 경우 "No 옵션을 사용 하는 데 필요한 인증 필요 "입니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작을 참조 하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

자주 묻는 질문에 대한 답변은, [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.
