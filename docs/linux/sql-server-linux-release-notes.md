---
title: SQL Server 2017 on Linux 릴리스 정보
description: 이 문서에는 Linux에서 실행되는 SQL Server 2017에 대한 릴리스 정보 및 지원되는 기능이 포함됩니다. 최신 릴리스 및 여러 이전 릴리스에 대한 릴리스 정보가 포함됩니다.
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 5b6fce0bdde7e320eea0371125a61627652de80d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68388407"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>SQL Server 2017 on Linux 릴리스 정보

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 릴리스 정보는 Linux에서 실행되는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]에 적용됩니다. 이 문서는 각 릴리스에 대한 섹션으로 나뉩니다. GA 릴리스에는 자세한 지원 가능성 및 알려진 문제가 나열되어 있습니다. 각 CU(누적 업데이트) 또는 GDR(일반 배포 릴리스)에는 CU 변경 내용을 설명하는 지원 문서 링크 및 Linux 패키지 다운로드 링크가 있습니다.

> [!TIP]
> 이 릴리스 정보는 특히 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 릴리스에 해당합니다. 새 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에 대한 자세한 내용은 [Linux의 SQL Server 2019 미리 보기 릴리스 정보](sql-server-linux-release-notes-2019.md?view=sql-server-ver15)를 참조하세요.

## <a name="supported-platforms"></a>지원 플랫폼

| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 또는 7.6 서버 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 또는 EXT4 | [설치 가이드](quickstart-install-connect-ubuntu.md) | 
| Windows, Mac 또는 Linux의 Docker Engine 1.8 이상 | 해당 사항 없음 | [설치 가이드](quickstart-install-connect-docker.md) | 

> [!TIP]
> 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에 대한 [시스템 요구 사항](sql-server-linux-setup.md#system)을 검토하세요. [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]에 대한 최신 지원 정책은 [Microsoft SQL Server의 기술 지원 정책](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)을 참조하세요.

## <a name="tools"></a>도구

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 대상으로 하는 대부분의 기존 클라이언트 도구는 Linux에서 실행되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 원활하게 사용할 수 있습니다. 일부 도구에는 Linux에서 잘 작동하는 특정 버전 요구 사항이 있을 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구의 전체 목록은 [SQL Server용 SQL 도구 및 유틸리티](../tools/overview-sql-tools.md)를 참조하세요.

## <a name="release-history"></a>릴리스 기록

다음 표에는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 릴리스 기록이 나와 있습니다.

| 릴리스               | 버전 옵션       | 릴리스 날짜 |
|-----------------------|---------------|--------------|
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
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

## <a id="cuinstall"></a> 업데이트 설치 방법

CU 리포지토리(**mssql-server-2017**)를 구성한 경우에는 새 설치를 수행할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 패키지의 최신 CU가 제공됩니다. CU 리포지토리는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에 대한 모든 패키지 설치 문서의 기본값입니다. GDR 리포지토리(**mssql-server-2017-gdr**)를 구성한 경우 GA 이후 릴리스된 중요 보안 업데이트만 제공됩니다. Docker 컨테이너 CU 또는 GDR 업데이트가 필요한 경우 [Docker 엔진용 Microsoft SQL Server on Linux](https://hub.docker.com/r/microsoft/mssql-server)의 공식 이미지를 참조하세요. 리포지토리 구성에 대한 자세한 내용은 [SQL Server on Linux용 리포지토리 구성](sql-server-linux-change-repo.md)을 참조하세요.

기존 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 패키지를 업데이트하는 경우에는 각 패키지에 대해 적절한 업데이트 명령을 실행하여 최신 CU를 가져옵니다. 각 패키지의 특정 업데이트 지침은 다음 설치 가이드를 참조하세요.

- [SQL Server 패키지 설치](sql-server-linux-setup.md#upgrade)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)
- [SQL Server 에이전트 사용](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a> CU15(2019년 5월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU15(누적 업데이트 15) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3162.1입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3162.1-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3162.1-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3162.1-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a> CU14(2019년 3월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU14(누적 업데이트 14) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3076.1입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3076.1-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3076.1-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3076.1-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a> CU13(2018년 12월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU13(누적 업데이트 13) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3048.4입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3048.4-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3048.4-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3048.4-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12(2018년 10월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU12(누적 업데이트 12) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3045.24입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3045.24-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3045.24-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3045.24-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11(2018년 9월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU11(누적 업데이트 11) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3038.14입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3038.14-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3038.14-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3038.14-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10(2018년 8월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU10(누적 업데이트 10) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3037.1입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3037.1-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3037.1-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3037.1-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9-GDR2(2018년 8월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 이전 릴리스 CU(CU9)가 포함된 보안 업데이트합니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3035.2입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3035.2-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM 패키지 | 14.0.3035.2-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3035.2-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2(2018년 8월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 GDR2 및 GDR1 보안 수정 사항만 포함된 보안 업데이트합니다.  이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.2002.14입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.2002.14-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.2002.14-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.2002.14-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9(2018년 7월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU9(누적 업데이트 9) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3030.27입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3030.27-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3030.27-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3030.27-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8(2018년 6월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU8(누적 업데이트 8) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3029.16입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3029.16-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3029.16-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3029.16-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7(2018년 5월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU7(누적 업데이트 7) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3026.27입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3026.27-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3026.27-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3026.27-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6(2018년 4월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU6(누적 업데이트 6) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3025.34입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3025.34-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3025.34-3 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3025.34-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5(2018년 3월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU5(누적 업데이트 5) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3023.8입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643) 항목을 참조하세요.

### <a name="known-upgrade-issue"></a>알려진 업그레이드 문제

이전 릴리스에서 CU5로 업그레이드하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 다음 오류와 함께 시작하지 못할 수 있습니다.

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

이 오류를 해결하려면 SQL Server 에이전트를 사용하도록 설정하고 다음 명령을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다시 시작합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3023.8-5 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3023.8-5 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3023.8-5 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4(2018년 2월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU4(누적 업데이트 4) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3022.28입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

> [!NOTE]
> CU4부터 SQL Server 에이전트는 더 이상 별도의 패키지로 설치되지 않습니다. 엔진 패키지와 함께 설치되며 사용하도록 설정되어야 합니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3022.28-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3022.28-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3022.28-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1(2018년 1월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 GDR1 보안 수정 사항만 포함된 보안 업데이트합니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.2000.63입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.2000.63-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.2000.63-3 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.2000.63-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3(2018년 1월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU3(누적 업데이트 3) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3015.40입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3015.40-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3015.40-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3015.40-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2(2017년 11월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU2(누적 업데이트 2) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3008.27입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3008.27-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3008.27-1 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3008.27-1 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1(2017년 10월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 CU1(누적 업데이트 1) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.3006.16입니다. 이 릴리스의 수정 사항 및 향상된 기능에 대한 자세한 내용은 [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634) 항목을 참조하세요.

### <a name="package-details"></a>패키지 세부 정보

수동 또는 오프라인 패키지 설치의 경우 다음 표의 정보를 사용하여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3006.16-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.3006.16-3 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.3006.16-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA(2017년 10월)

이것은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]의 GA(일반 공급) 릴리스입니다. 이 릴리스의 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 버전은 14.0.1000.169입니다.

### <a name="package-details"></a>패키지 세부 정보

다음 표에는 RPM 및 Debian 패키지에 대한 패키지 세부 정보 및 다운로드 위치가 나와 있습니다. 다음 설치 가이드의 단계를 사용하는 경우 이 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지 설치](sql-server-linux-setup.md)
- [전체 텍스트 검색 패키지 설치](sql-server-linux-setup-full-text-search.md)
- [SQL Server 에이전트 패키지 설치](sql-server-linux-setup-sql-agent.md)
- [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.1000.169-2 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 패키지 | 14.0.1000.169-2 | [mssql-server 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[고가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 패키지 | 14.0.1000.169-2 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[고가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 에이전트 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> 지원되지 않는 기능 및 서비스

다음 기능 및 서비스는 GA 릴리스 시 Linux에서 사용할 수 없습니다. 이 기능에 대한 지원은 시간이 지나면서 점점 더 활성화됩니다.

| 영역 | 지원되지 않는 기능 또는 서비스 |
|-----|-----|
| **데이터베이스 엔진** | 트랜잭션 복제 |
| &nbsp; | 병합 복제 |
| &nbsp; | 변경 데이터 캡처(SQL Server 에이전트 참조) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | 타사 연결을 사용하는 분산 쿼리 |
| &nbsp; | [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이외의 데이터 원본에 연결된 서버  |
| &nbsp; | 시스템 확장 저장 프로시저(XP_CMDSHELL 등) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | EXTERNAL_ACCESS 또는 UNSAFE 권한 세트가 있는 CLR 어셈블리 |
| &nbsp; | Buffer Pool Extension |
| **SQL Server 에이전트** |  하위 시스템: CmdExec, PowerShell, Queue Reader, SSIS, SSAS, SSRS |
| &nbsp; | , |
| &nbsp; | 로그 판독기 에이전트 |
| &nbsp; | CDC(변경 데이터 캡처) |
| &nbsp; | Managed Backup |
| **고가용성** | 데이터베이스 미러링  |
| **보안** | 확장 가능 키 관리 |
| &nbsp; | 연결된 서버의 AD 인증 | 
| &nbsp; | AG(가용성 그룹)의 AD 인증 | 
| &nbsp; | 타사 AD 도구(Centrify, Vintela, Powerbroker) | 
| **Services** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | 데이터베이스 엔진 서비스 |
| &nbsp; | Master  Data  Services |
| &nbsp; | DTC(Distributed Transaction Coordinator) |

## <a name="known-issues"></a>알려진 문제

다음 섹션에서는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] on Linux의 GA(일반 공급) 릴리스에 관련된 알려진 문제를 설명합니다.

#### <a name="general"></a>일반

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 설치된 호스트 이름의 길이는 15자 이하여야 합니다. 

    - **해결 방법**: /etc/hostname에 있는 이름을 15자 이하의 이름으로 변경합니다.

- 시스템 시간을 역방향으로 수동으로 설정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 내의 내부 시스템 시간 업데이트를 중지합니다.

    - **해결 방법**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다시 시작합니다.

- 단일 인스턴스 설치만 지원됩니다.

    - **해결 방법**: 지정된 호스트에 둘 이상의 인스턴스를 포함하려면 VM 또는 Docker 컨테이너를 사용하는 것이 좋습니다. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에 연결할 수 없습니다.

- **sa** 로그인의 기본 언어는 영어입니다.

    - **해결 방법**: **ALTER LOGIN** 문을 사용하여 **sa** 로그인의 언어를 변경합니다.

#### <a name="databases"></a>데이터베이스

- master 데이터베이스는 mssql 유틸리티를 사용하여 이동할 수 없습니다. 다른 시스템 데이터베이스는 mssql-conf를 통해 이동할 수 있습니다.

- Windows의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 백업된 데이터베이스를 복원할 때 Transact-SQL 문에서 **WITH MOVE** 절을 사용해야 합니다.

- Microsoft DTC(Distributed Transaction Coordinator) 서비스가 필요한 분산 트랜잭션은 Linux에서 실행되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지 않습니다. DTC가 포함되지 않은 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결된 서버에 대한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 지원됩니다. 자세한 내용은 [Microsoft DTC(Distributed Transaction Coordinator) 서비스가 필요한 분산 트랜잭션은 Linux에서 실행되는 SQL Server에서 지원되지 않음](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)을 참조하세요.

- TLS(전송 계층 보안)에 대한 특정 알고리즘(암호 도구 모음)은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에서 제대로 작동하지 않습니다. 이로 인해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결을 시도할 때 연결 오류가 발생하며 고가용성 그룹의 복제본 간에 연결을 설정하는 데 문제가 발생합니다.

   - **해결 방법**: 다음을 수행하여 문제가 있는 암호 도구 모음을 사용하지 않도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux의 **mssql.conf** 구성 스크립트를 수정합니다.

      1. /var/opt/mssql/mssql.conf에 다음을 추가합니다.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 다음 명령을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다시 시작합니다.

      ```bash
      sudo systemctl restart mssql-server
      ```

- 메모리 내 OLTP를 사용하는 Windows의 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 데이터베이스는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] on Linux에서 복원할 수 없습니다. 메모리 내 OLTP를 사용하는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 데이터베이스를 복원하려면 먼저 백업/복원 또는 분리/연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux로 이동하기 전에 Windows의 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 또는 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]로 데이터베이스를 업그레이드합니다.

- 현재 사용자 권한 **ADMINISTER BULK OPERATIONS**는 Linux에서 지원되지 않습니다.

#### <a name="networking"></a>네트워킹

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

- NFS 버전 **4.2 이상**을 사용합니다. 이전 버전의 NFS는 최신 파일 시스템에서 일반적으로 필요한 기능(예: fallocate, 스파스 파일 만들기)을 지원하지 않습니다.
- NFS 탑재에 **/var/opt/mssql** 디렉터리만 배치합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 이진 파일 등의 다른 파일은 지원되지 않습니다.
- NFS 클라이언트가 원격 공유를 탑재할 때 ‘nolock’ 옵션을 사용하는지 확인합니다.

#### <a name="localization"></a>지역화

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

#### <a id="ssis"></a> SSIS(SQL Server Integration Services)

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

#### <a id="ssms"></a> SSMS(SQL Server Management Studio)

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
