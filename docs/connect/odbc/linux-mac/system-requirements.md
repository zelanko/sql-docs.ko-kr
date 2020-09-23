---
title: 시스템 요구 사항(ODBC Driver for SQL Server)
description: Linux 및 macOS 운영 체제 기반 ODBC Driver for SQL Server의 시스템 요구 사항을 나열합니다.
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 74b7bf1680dd956dfca85917939ad24a3559d7de
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934462"
---
# <a name="system-requirements-linux-and-macos"></a>시스템 요구 사항(Linux 및 macOS)

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver를 사용하기 위한 요구 사항을 나열합니다.

## <a name="sql-version-compatibility"></a>SQL 버전 호환성

Linux 및 macOS 드라이버 SQL 버전 호환성은 [Windows 드라이버 SQL 버전 호환성](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility)과 동일합니다.

## <a name="operating-system-support"></a>운영 체제 지원

Linux 및 macOS 드라이버 버전 17, 13.1 및 13은 다음 운영 체제의 x64 아키텍처에서 지원됩니다.

|드라이버 버전&nbsp;&#8594;<br />&#8595; 운영 체제     |17.6|17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|----|---|
|Apple OS X 10.11(El Capitan)  |    |    |예 |예 |예 |예 |예 |예 |예|
|Apple macOS 10.12(Sierra)     |    |    |예 |예 |예 |예 |예 |예 |예|
|Apple macOS 10.13(Sierra)|예 |예 |예 |예 |예 |예 |예 |예 |예|
|Apple macOS 10.14(Mojave)     |예 |예 |예 |예 |    |    |    |    |   |
|Apple macOS 10.15(Catalina.properties)   |예 |예 |    |    |    |    |    |    |   |
|Alpine Linux 3.11              |예 |예 |    |    |    |    |    |    |   |
|Debian Linux 8                 |예 |예 |예 |예 |예 |예 |예 |예 |예|
|Debian Linux 9                 |예 |예 |예 |예 |예 |예 |예 |예 |예|
|Debian Linux 10                |예 |예 |예 |    |    |    |    |    |   |
|Oracle Linux 8                 |예 |예 |    |    |    |    |    |    |   |
|RedHat Enterprise Linux 6      |예 |예 |예 |예 |예 |예 |예 |예 |예|
|RedHat Enterprise Linux 7      |예 |예 |예 |예 |예 |예 |예 |예 |예|
|RedHat Enterprise Linux 8      |예 |예 |예 |    |    |    |    |    |   |
|SUSE Linux Enterprise Server 11<sup>1</sup>|예 |예 |예 |예 |예 |예 |예 |예 |예|
|SUSE Linux Enterprise Server 12|예 |예 |예 |예 |예 |예 |예 |예 |예|
|SUSE Linux Enterprise Server 15|예 |예 |예 |예 |    |    |    |    |   |
|Ubuntu Linux 14.04             |    |    |예 |예 |예 |예 |예 |예 |예|
|Ubuntu Linux 16.04             |예 |예 |예 |예 |예 |예 |예 |예 |예|
|Ubuntu Linux 18.04             |예 |예 |예 |예 |예 |    |    |    |   |
|Ubuntu Linux 20.04             |예 |    |    |    |    |    |    |    |   |

<sup>1</sup> ODBC Driver 17은 SUSE Linux Enterprise Server 11 SP4만 지원합니다.

[ODBC 드라이버 설치(Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) 및 [ODBC 드라이버 설치(macOS)](install-microsoft-odbc-driver-sql-server-macos.md)에서 설명한 대로, Linux 및 macOS 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1, 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 설치 패키지는 사용자 배포의 패키지 관리 시스템을 사용하여 설치된 경우 드라이버의 종속성을 자동으로 해결합니다.

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
* 64비트 SQLLEN/SQLULEN용으로 빌드된 64비트 UnixODBC 2.3.0 드라이버 관리자입니다. 이후 버전의 64비트 UnixODBC 드라이버 관리자는 Linux 기반 ODBC 드라이버로 지원되지 않습니다. 자세한 내용은 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 을 참조하세요.  
  
* ODBC Driver for **Red Hat Enterprise Linux 5(64비트)** 에는 다음 패키지가 필요하며 [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)에서 다운로드할 수 있습니다.  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* ODBC Driver for **Red Hat Enterprise Linux 6(64비트)** 에는 다음 패키지가 필요하며 [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)에서 다운로드할 수 있습니다.  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* ODBC Driver for **SUSE Linux Enterprise 11 서비스 팩 2(64비트)** 에는 다음 패키지가 필요하며 [Microsoft ODBC Driver 11 Preview for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)에서 다운로드할 수 있습니다.  
  * `glibc`  
  * `libstdc++46`  
  * `libgcc46`  
  * `libuuid1`  
  * `krb5`  
  * `libopenssl0_9_8`  
  
## <a name="see-also"></a>참고 항목

[드라이버 관리자 설치](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)  
[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  
[릴리스 정보](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
