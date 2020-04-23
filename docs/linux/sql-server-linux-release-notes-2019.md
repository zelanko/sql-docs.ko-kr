---
title: SQL Server 2019 on Linux 릴리스 정보
description: 이 문서에는 Linux에서 실행되는 SQL Server 2019에 대한 릴리스 정보 및 지원되는 기능이 포함됩니다. 최신 릴리스 및 여러 이전 릴리스에 대한 릴리스 정보가 포함됩니다.
author: VanMSFT
ms.author: vanto
ms.date: 03/31/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7782806a1ba44c4f18c4005dfa592998cc9f026b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301725"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>SQL Server 2019 on Linux 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

다음 릴리스 정보는 Linux에서 실행되는 SQL Server 2019에 적용됩니다. 이 문서는 각 릴리스에 대한 섹션으로 나뉩니다. 각 릴리스에는 CU 변경 내용을 설명하는 지원 문서 링크와 Linux 패키지 다운로드용 링크가 있습니다.

> [!TIP]
> SQL Server 2019의 새로운 Linux 기능에 대해 알아보려면 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)을 참조하세요.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5, 7.6 또는 8 서버 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2, SP3, SP4 또는 SP5 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS, 18.04 LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Windows, Mac 또는 Linux의 Docker Engine 1.8 이상 | 해당 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 Linux의 SQL Server에 대한 [시스템 요구 사항](sql-server-linux-setup.md#system)을 검토하세요. SQL Server 2017에 대 한 최신 지원 정책은 [Microsoft SQL Server의 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)을 참조하세요.

## <a name="tools"></a>도구

SQL Server를 대상으로 하는 대부분의 기존 클라이언트 도구는 Linux에서 실행되는 SQL Server에서 원활하게 사용할 수 있습니다. 일부 도구에는 Linux에서 잘 작동하는 특정 버전 요구 사항이 있을 수 있습니다. SQL Server 도구의 전체 목록은 [SQL Server용 SQL 도구 및 유틸리티](../tools/overview-sql-tools.md)를 참조하세요.

## <a name="release-history"></a>릴리스 기록

다음 표에는 SQL Server 2019 릴리스의 릴리스 기록이 나와 있습니다.

| 해제                   | 버전       | 릴리스 날짜 |
|---------------------------|---------------|--------------|
| [CU4](#cu4)               | 15.0.4033.1   | 2020-03-31   |
| [CU3](#cu3)               | 15.0.4023.6   | 2020-03-12   |
| [CU2](#cu2)               | 15.0.4013.40  | 2020-02-13   |
| [CU1](#cu1)               | 15.0.4003.23  | 2020-01-07   |
| [GA](#ga)                 | 15.0.2000.5   | 2019-11-04   |
| [릴리스 후보](#rc)  | 15.0.1900.25  | 2019-08-21   |

## <a name="how-to-install-updates"></a><a id="cuinstall"></a> 업데이트 설치 방법

CU 리포지토리(mssql-server-2019)를 구성한 경우에는 새 설치를 수행할 때 SQL Server 패키지의 최신 CU가 제공됩니다. Docker 컨테이너 이미지가 필요한 경우 [Docker 엔진용 Microsoft SQL Server on Linux](https://hub.docker.com/r/microsoft/mssql-server/)의 공식 이미지를 참조하세요. 리포지토리 구성에 대한 자세한 내용은 [SQL Server on Linux용 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하세요.

기존 SQL Server 패키지를 업데이트하는 경우에는 각 패키지에 대해 적절한 업데이트 명령을 실행하여 최신 CU를 가져옵니다. 각 패키지의 특정 업데이트 지침은 다음 설치 가이드를 참조하세요.

- [SQL Server 패키지 설치](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [Linux에서 SQL Server 2019 Machine Learning Services R 및 Python 지원 설치](sql-server-linux-setup-machine-learning.md)
- [PolyBase 패키지 설치](../relational-databases/polybase/polybase-linux-setup.md)
- [SQL Server 에이전트 사용](sql-server-linux-setup-sql-agent.md)

## <a name="cu4-april-2020"></a><a id="cu4"></a> CU4(2020년 4월)

SQL Server 2019(15.x)의 CU4(누적 업데이트 4) 릴리스입니다. 이 릴리스의 SQL Server 데이터베이스 엔진 버전은 15.0.4033.1입니다. 수정 사항 및 개선 사항에 대한 자세한 내용은 <https://support.microsoft.com/help/4548597>를 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU1부터 Red Hat의 오프라인 패키지 설치 링크는 RHEL 8 패키지를 가리킵니다. RHEL 7 패키지를 찾고 있는 경우 다운로드 경로 <https://packages.microsoft.com/rhel/7/mssql-server-2019/>를 참조하세요.
>
> **Ubuntu 18.04**는 CU3부터 SQL Server 2019에서 지원됩니다. Ubuntu의 오프라인 패키지 설치 링크는 Ubuntu 18.04 패키지를 가리킵니다. Ubuntu 16.04 패키지를 찾고 있는 경우 다운로드 경로 <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/>을 참조하세요.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.4033.1-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4033.1-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4033.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4033.1-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4033.1-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4033.1-2.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4033.1-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.4033.1-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4033.1-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4033.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4033.1-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4033.1-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4033.1-2.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4033.1-2.x86_64.rpm)|
| Ubuntu 18.04 Debian 패키지 | 15.0.4033.1-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4033.1-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4033.1-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4033.1-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4033.1-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4033.1-2_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4033.1-2_amd64.deb)|

## <a name="cu3-march-2020"></a><a id="cu3"></a> CU3(2020년 3월)

SQL Server 2019(15.x)의 CU3(누적 업데이트 3) 릴리스입니다. 이 릴리스의 SQL Server 데이터베이스 엔진 버전은 15.0.4023.6입니다. 수정 사항 및 개선 사항에 대한 자세한 내용은 <https://support.microsoft.com/help/4538853>를 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU1부터 Red Hat의 오프라인 패키지 설치 링크는 RHEL 8 패키지를 가리킵니다. RHEL 7 패키지를 찾고 있는 경우 다운로드 경로 <https://packages.microsoft.com/rhel/7/mssql-server-2019/>를 참조하세요.
>
> **Ubuntu 18.04**는 CU3부터 SQL Server 2019에서 지원됩니다. Ubuntu의 오프라인 패키지 설치 링크는 Ubuntu 18.04 패키지를 가리킵니다. Ubuntu 16.04 패키지를 찾고 있는 경우 다운로드 경로 <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/>을 참조하세요.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.4023.6-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4023.6-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4023.6-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4023.6-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4023.6-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4023.6-2.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4023.6-2.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.4023.6-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4023.6-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4023.6-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4023.6-2.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4023.6-2.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4023.6-2.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4023.6-2.x86_64.rpm)|
| Ubuntu 18.04 Debian 패키지 | 15.0.4023.6-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4023.6-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4023.6-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4023.6-2_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4023.6-2_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4023.6-2_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4023.6-2_amd64.deb)|

## <a name="cu2-february-2020"></a><a id="cu2"></a> CU2(2020년 2월)

이것은 SQL Server 2019(15.x)의 CU2(누적 업데이트 2) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.4013.40입니다. 수정 사항 및 개선 사항에 대한 자세한 내용은 <https://support.microsoft.com/help/4536075>를 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU1부터 Red Hat의 오프라인 패키지 설치 링크는 RHEL 8 패키지를 가리킵니다. RHEL 7 패키지를 찾고 있는 경우 다운로드 경로 <https://packages.microsoft.com/rhel/7/mssql-server-2019/>를 참조하세요.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.4013.40-8 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4013.40-8.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4013.40-8.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4013.40-8.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4013.40-8.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4013.40-8.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4013.40-8.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.4013.40-8 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4013.40-8.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4013.40-8.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4013.40-8.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4013.40-8.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4013.40-8.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4013.40-8.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.4013.40-8 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4013.40-8_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4013.40-8_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4013.40-8_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4013.40-8_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4013.40-8_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4013.40-8_amd64.deb)|

## <a name="cu1-january-2020"></a><a id="cu1"></a> CU1(2020년 1월)

이것은 SQL Server 2019(15.x)의 CU1(누적 업데이트 1) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.4003.23입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 <https://support.microsoft.com/en-us/help/4527376>을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU1부터 Red Hat의 오프라인 패키지 설치 링크는 RHEL 8 패키지를 가리킵니다. RHEL 7 패키지를 찾고 있는 경우 다운로드 경로 <https://packages.microsoft.com/rhel/7/mssql-server-2019/>를 참조하세요.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.4003.23-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4003.23-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4003.23-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4003.23-3.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4003.23-3.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4003.23-3.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4003.23-3.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.4003.23-3 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4003.23-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4003.23-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4003.23-3.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4003.23-3.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4003.23-3.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4003.23-3.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.4003.23-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4003.23-3_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4003.23-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4003.23-3_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4003.23-3_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4003.23-3_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4003.23-3_amd64.deb)|

## <a name="ga-november-2019"></a><a id="ga"></a> GA(2019년 11월)

이것은 SQL Server 2019(15.x)의 GA(일반 공급) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.2000.5입니다.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.2000.5-5 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.2000.5-5 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.2000.5-5 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.2000.5-5_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.2000.5-5_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.2000.5-5_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.2000.5-5_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.2000.5-5_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.2000.5-5_amd64.deb)|

## <a name="release-candidate-august-2019"></a><a id="rc"></a> 릴리스 후보(2019년 8월)

다음 섹션에서는 릴리스 후보의 패키지 위치 및 알려진 문제를 제공합니다. SQL Server 2019의 Linux용 새 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 15.0.1900.25-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| SLES RPM 패키지 | 15.0.1900.25-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 확장성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 패키지 | 15.0.1900.25-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Java 확장성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[PolyBase RPM 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a name="known-issues"></a>알려진 문제

다음 섹션에서는 SQL Server 2019(15.x) on Linux의 GA(일반 공급) 릴리스에 관련된 알려진 문제를 설명합니다.

### <a name="general"></a>일반

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 설치된 호스트 이름의 길이는 15자 이하여야 합니다. 

    - **해결 방법**: /etc/hostname에 있는 이름을 15자 이하의 이름으로 변경합니다.

- 시스템 시간을 역방향으로 수동으로 설정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 내의 내부 시스템 시간 업데이트를 중지합니다.

    - **해결 방법**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다시 시작합니다.

- 단일 인스턴스 설치만 지원됩니다.

    - **해결 방법**: 지정된 호스트에 둘 이상의 인스턴스를 포함하려면 VM 또는 Docker 컨테이너를 사용하는 것이 좋습니다. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에 연결할 수 없습니다.

- **sa** 로그인의 기본 언어는 영어입니다.

    - **해결 방법**: **ALTER LOGIN** 문을 사용하여 **sa** 로그인의 언어를 변경합니다.

- OLEDB 공급자는 다음 경고를 기록합니다. `Failed to verify the Authenticode signature of 'C:\binn\msoledbsql.dll'. Signature verification of SQL Server DLLs will be skipped. Genuine copies of SQL Server are signed. Failure to verify the Authenticode signature might indicate that this is not an authentic release of SQL Server. Install a genuine copy of SQL Server or contact customer support.`

   - **해결 방법**: 사용자가 조치할 필요는 없습니다. OLEDB 공급자는 SHA256을 사용하여 서명됩니다. SQL Server 데이터베이스 엔진은 서명된 .dll의 유효성을 올바르게 검사하지 않습니다.

### <a name="databases"></a>데이터베이스

- master 데이터베이스는 mssql-conf 유틸리티를 사용하여 이동할 수 없습니다. 다른 시스템 데이터베이스는 mssql-conf를 통해 이동할 수 있습니다.

- Windows의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 백업된 데이터베이스를 복원할 때 Transact-SQL 문에서 **WITH MOVE** 절을 사용해야 합니다.

- TLS(전송 계층 보안)에 대한 특정 알고리즘(암호 도구 모음)은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에서 제대로 작동하지 않습니다. 이로 인해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결을 시도할 때 연결 오류가 발생하며 고가용성 그룹의 복제본 간에 연결을 설정하는 데 문제가 발생합니다.

   - **해결 방법**: 다음을 수행하여 문제가 있는 암호 도구 모음을 사용하지 않도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux의 **mssql.conf** 구성 스크립트를 수정합니다.

      1. /var/opt/mssql/mssql.conf에 다음을 추가합니다.

          ```
          [network]
          tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
          ```

         > [!NOTE]
         > 위의 코드에서 `!`는 식을 부정합니다. 이는 OpenSSL에 다음 암호화 그룹을 사용하지 않도록 지시합니다.  

      1. 다음 명령을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다시 시작합니다.

          ```bash
          sudo systemctl restart mssql-server
          ```

- 메모리 내 OLTP를 사용하는 Windows의 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 데이터베이스는 SQL Server 2019(15.x) on Linux에서 복원할 수 없습니다. 메모리 내 OLTP를 사용하는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 데이터베이스를 복원하려면 먼저 백업/복원 또는 분리/연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux로 이동하기 전에 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], SQL Server 2017 또는 SQL Server 2019 on Windows로 데이터베이스를 업그레이드합니다.

- 현재 사용자 권한 **ADMINISTER BULK OPERATIONS**는 Linux에서 지원되지 않습니다.

### <a name="networking"></a>네트워킹

다음 조건이 둘 다 충족되는 경우 연결된 서버 또는 가용성 그룹과 같은 sqlservr 프로세스의 아웃바운드 TCP 연결에 관련된 기능이 작동하지 않을 수 있습니다.

1. 대상 서버는 IP 주소가 아닌 호스트 이름으로 지정됩니다.

1. 원본 인스턴스의 IPv6는 커널에서 사용하지 않도록 설정되어 있습니다. 커널에서 시스템의 IPv6이 사용하도록 설정되어 있는지 확인하려면 다음 테스트를 모두 통과해야 합니다.

   - `cat /proc/cmdline`은 현재 커널의 부팅 명령줄을 인쇄합니다. 출력에는 `ipv6.disable=1`이 포함되지 않아야 합니다.
   - /proc/sys/net/ipv6/ 디렉터리가 있어야 합니다.
   - `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`을 호출하는 C 프로그램이 성공해야 합니다. syscall은 fd != -1을 반환해야 하며 EAFNOSUPPORT와 함께 실패하지 않아야 합니다.

정확한 오류는 기능에 따라 달라집니다. 연결된 서버의 경우 이 오류는 로그인 시간 제한 오류로 매니페스트됩니다. 가용성 그룹의 경우 보조의 `ALTER AVAILABILITY GROUP JOIN` DDL이 5분 후에 다운로드 구성 시간 제한 오류와 함께 실패합니다.

이 문제를 해결하려면 다음 중 하나를 수행합니다.

1. 호스트 이름 대신 IP를 사용하여 TCP 연결의 대상을 지정합니다.

1. 부팅 명령줄에서 `ipv6.disable=1`을 제거하여 커널에서 IPv6을 사용하도록 설정합니다. 이 작업을 수행하는 방법은 grub와 같은 Linux 배포 및 부팅 로더에 따라 다릅니다. IPv6을 사용하지 않도록 설정하려면 `sysctl` 구성(예: `/etc/sysctl.conf`)에서 `net.ipv6.conf.all.disable_ipv6 = 1`을 설정하여 사용하지 않도록 설정할 수도 있습니다. 이렇게 하면 시스템의 네트워크 어댑터가 IPv6 주소를 가져올 수 없지만 sqlservr 기능이 작동할 수 있습니다.

#### <a name="network-file-system-nfs"></a>NFS(네트워크 파일 시스템)
프로덕션에서 **NFS(네트워크 파일 시스템)** 원격 공유를 사용하는 경우 다음과 같은 지원 요구 사항을 확인합니다.

- NFS 버전 **4.2 이상**을 사용합니다. 이전 버전의 NFS는 최신 파일 시스템에서 일반적으로 필요한 기능(예: `fallocate` 및 스파스 파일 만들기)을 지원하지 않습니다.
- NFS 탑재에 **/var/opt/mssql** 디렉터리만 배치합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 이진 파일 등의 다른 파일은 지원되지 않습니다.
- NFS 클라이언트가 원격 공유를 탑재할 때 `nolock` 옵션을 사용하는지 확인합니다.

### <a name="localization"></a>지역화

- 설치하는 동안 로캘이 영어(en_us)가 아닌 경우 bash 세션/터미널에서 UTF-8 인코딩을 사용해야 합니다. ASCII 인코딩을 사용하는 경우 다음과 유사한 오류가 표시될 수 있습니다.

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   UTF-8 인코딩을 사용할 수 없는 경우 MSSQL_LCID 환경 변수를 사용하여 설치 프로그램을 실행하고 원하는 언어를 지정합니다.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- mssql-conf 설치 프로그램을 실행하고 영어 이외의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치를 수행할 때 잘못된 확장 문자가 지역화된 텍스트 “SQL Server를 구성하는 중...” 뒤에 표시됩니다. 또는 라틴어 이외 설치의 경우 문장이 완전히 누락될 수 있습니다. 누락된 문장에는 다음 지역화된 문자열이 표시되어야 합니다. “라이선싱 PID가 처리되었습니다. 새 버전은 [\<Name\> edition]입니다.” 이 문자열은 정보를 제공하기 위한 출력일 뿐이며 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 누적 업데이트에서 모든 언어에 대해 이 문제를 해결할 예정입니다. 이 문제는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 성공적인 설치에 영향을 주지 않습니다. 

#### <a name="full-text-search"></a>전체 텍스트 검색

- 이 릴리스에서는 Office 문서용 필터를 비롯한 일부 필터를 사용할 수 없습니다. 지원되는 필터 목록은 [Linux에서 SQL Server 전체 텍스트 검색 설치](sql-server-linux-setup-full-text-search.md#filters)를 참조하세요.

### <a name="sql-server-integration-services-ssis"></a><a id="ssis"></a> SSIS(SQL Server Integration Services)

- **mssql-server-is** 패키지는 이 릴리스의 SUSE에서 지원되지 않습니다. 현재 Ubuntu 및 RHEL(Red Hat Enterprise Linux)에서는 지원됩니다.

- Linux CTP 2.1 새로 고침 이상에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 사용하는 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지는 Linux에서 ODBC 연결을 사용할 수 있습니다. 이 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 MySQL ODBC 드라이버로 테스트되었지만 ODBC 사양을 준수하는 모든 유니코드 ODBC 드라이버에서도 작동할 것으로 예상됩니다. 디자인 타임에 ODBC 데이터에 연결하기 위한 DSN 또는 연결 문자열을 제공할 수 있습니다. Windows 인증을 사용할 수도 있습니다. 자세한 내용은 [Linux의 ODBC 지원을 알리는 블로그 게시물](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)을 참조하세요.

- Linux에서 SSIS 패키지를 실행할 경우 이번 릴리스에서는 다음 기능이 지원되지 않습니다.
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그 데이터베이스
  - SQL 에이전트에서 예약된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out
  - SSIS용 Azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

현재 지원되지 않거나 제한적으로 지원되는 기본 제공 SSIS 구성 요소 목록은 [Linux의 SSIS에 대한 제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md#components)를 참조하세요.

Linux SSIS에 대한 자세한 내용은 다음 문서를 참조하세요.
-   [Linux에 대한 SSIS 지원을 알리는 블로그 게시물](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Linux에서 SSIS(SQL Server Integration Services) 설치](sql-server-linux-setup-ssis.md)
-   [SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)

### <a name="sql-server-management-studio-ssms"></a><a id="ssms"></a> SSMS(SQL Server Management Studio)

다음 제한 사항은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에 연결된 Windows의 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 적용됩니다.

- 유지 관리 계획은 지원되지 않습니다.

- MDW(관리 데이터 웨어하우스) 및 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 데이터 수집기는 지원되지 않습니다. 

- Windows 인증 또는 Windows 이벤트 로그 옵션을 포함하는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 구성 요소는 Linux에서 작동하지 않습니다. SQL 로그인과 같은 다른 옵션과 함께 이 기능을 계속 사용할 수 있습니다. 

- 보존할 로그 파일 수는 수정할 수 없습니다.

## <a name="next-steps"></a>다음 단계

시작하려면 다음 빠른 시작을 참조하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [실행 및 연결 - 클라우드](quickstart-install-connect-clouds.md)

질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요.
