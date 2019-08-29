---
title: SQL Server 2019 on Linux 릴리스 정보
description: 이 문서에는 Linux에서 실행되는 SQL Server 2019에 대한 릴리스 정보 및 지원되는 기능이 포함됩니다. 최신 릴리스 및 여러 이전 릴리스에 대한 릴리스 정보가 포함됩니다.
author: VanMSFT
ms.author: vanto
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: af3b6f82e3b76e2dd2b11403bccf4b3e0885912e
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890898"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>SQL Server 2019 on Linux 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

다음 릴리스 정보는 Linux에서 실행되는 SQL Server 2019에 적용됩니다. 이 문서는 각 릴리스에 대한 섹션으로 나뉩니다. 각 릴리스에는 CU 변경 내용을 설명하는 지원 문서 링크와 Linux 패키지 다운로드용 링크가 있습니다.

> [!TIP]
> SQL Server 2019의 새로운 Linux 기능에 대해 알아보려면 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)을 참조하세요.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 또는 7.6 서버 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Windows, Mac 또는 Linux의 Docker Engine 1.8 이상 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 Linux의 SQL Server에 대한 [시스템 요구 사항](sql-server-linux-setup.md#system)을 검토하세요. SQL Server 2017에 대 한 최신 지원 정책은 [Microsoft SQL Server의 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)을 참조하세요.

## <a name="tools"></a>도구

SQL Server를 대상으로 하는 대부분의 기존 클라이언트 도구는 Linux에서 실행되는 SQL Server에서 원활하게 사용할 수 있습니다. 일부 도구에는 Linux에서 잘 작동하는 특정 버전 요구 사항이 있을 수 있습니다. SQL Server 도구의 전체 목록은 [SQL Server용 SQL 도구 및 유틸리티](../tools/overview-sql-tools.md)를 참조하세요.

## <a name="release-history"></a>릴리스 기록

다음 표에는 SQL Server 2019 미리 보기 릴리스의 릴리스 기록이 나와 있습니다.

| 릴리스                   | 버전 옵션       | 릴리스 날짜 |
|---------------------------|---------------|--------------|
| [릴리스 후보](#rc)  | 15.0.1900.25  | 2019-8-21    |
| [CTP 3.2](#CTP32)         | 15.0.1800.32  | 2019-7-24    |
| [CTP 3.1](#CTP31)         | 15.0.1700.37  | 2019-6-26    |
| [CTP 3.0](#CTP30)         | 15.0.1600.8   | 2019-5-22    |
| [CTP 2.5](#CTP25)         | 15.0.1500.28  | 2019-4-24    |
| [CTP 2.4](#CTP24)         | 15.0.1400.75  | 2019-3-27    |
| [CTP 2.3](#CTP23)         | 15.0.1300.359 | 2019-3-01    |
| [CTP 2.2](#CTP22)         | 15.0.1200.24  | 2018-12-11   |
| [CTP 2.1](#CTP21)         | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)         | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> 업데이트 설치 방법

미리 보기 리포지토리(**mssql-server-preview**)를 구성한 경우에는 새 설치를 수행할 때 최신 SQL Server CTP 패키지가 제공됩니다. Docker 컨테이너 이미지가 필요한 경우 [Docker 엔진용 Microsoft SQL Server on Linux](https://hub.docker.com/r/microsoft/mssql-server/)의 공식 이미지를 참조하세요. 리포지토리 구성에 대한 자세한 내용은 [Linux에서 SQL Server용 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하세요.

기존 SQL Server 패키지를 업데이트하는 경우에는 각 패키지에 대해 적절한 업데이트 명령을 실행하여 최신 CU를 가져옵니다. 각 패키지의 특정 업데이트 지침은 다음 설치 가이드를 참조하세요.

- [SQL Server 패키지 설치](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [Linux에서 SQL Server 2019 미리 보기 Machine Learning Services R 및 Python 지원 설치](sql-server-linux-setup-machine-learning.md)
- [PolyBase 패키지 설치](../relational-databases/polybase/polybase-linux-setup.md)
- [SQL Server 에이전트 사용](sql-server-linux-setup-sql-agent.md)

## <a id="rc"></a> 릴리스 후보(2019년 8월)

다음 섹션에서는 릴리스 후보의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1900.25-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1900.25-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1900.25-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1900.25-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a id="CTP32"></a>CTP 3.2(2019년 7월)

다음 섹션에서는 CTP 3.2 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1800.32-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1800.32-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1800.32-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1800.32-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1800.32-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1800.32-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1800.32-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1800.32-1_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1800.32-1_amd64.deb)|

## <a id="CTP31"></a> CTP 3.1(2019년 6월)

다음 섹션에서는 CTP 3.1 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1700.37-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1700.37-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1700.37-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0(2019년 5월)

다음 섹션에서는 CTP 3.0 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1600.8-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1600.8-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1600.8-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a id="CTP25"></a> CTP 2.5(2019년 4월)

다음 섹션에서는 CTP 2.5 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1500.28-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1500.28-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1500.28-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a id="CTP24"></a> CTP 2.4(2019년 3월)

다음 섹션에서는 CTP 2.4 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1400.75-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1400.75-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1400.75-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a id="CTP23"></a> CTP 2.3(2019년 2월)

다음 섹션에서는 CTP 2.3 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1300.359-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1300.359-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1300.359-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a id="CTP22"></a> CTP 2.2(2018년 12월)

다음 섹션에서는 CTP 2.2 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1200.24-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1200.24-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1200.24-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a id="CTP21"></a> CTP 2.1(2018년 11월)

다음 섹션에서는 CTP 2.1 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1100.94-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1100.94-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1100.94-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a id="CTP20"></a> CTP 2.0(2018년 9월)

다음 섹션에서는 CTP 2.0 릴리스의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1000.34-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1000.34-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1000.34-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>알려진 문제

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft Distributed Transaction Coordinator

현재 MSDTC에는 인증되지 않은 트랜잭션이 필요합니다. 예를 들어 Windows의 SQL Server에서 Linux의 SQL Server로 연결된 서버를 사용하거나 Windows 클라이언트 애플리케이션을 사용하여 Linux의 SQL Server에 대해 분산 트랜잭션을 시작하는 경우 Windows 서버/클라이언트의 MSDTC는 "인증 필요 없음" 옵션을 사용해야 합니다.

## <a name="next-steps"></a>다음 단계

시작하려면 다음 빠른 시작을 참조하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.
