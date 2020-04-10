---
title: 시스템 요구 사항(ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/18/2020
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
ms.openlocfilehash: 2459a9f57f3591db1107994d0b18770690f22724
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921174"
---
# <a name="system-requirements"></a>시스템 요구 사항

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver를 사용하기 위한 요구 사항을 나열합니다.

## <a name="sql-version-compatibility"></a>SQL 버전 호환성

Linux 및 macOS 드라이버 SQL 버전 호환성은 [Windows 드라이버 SQL 버전 호환성](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility)과 동일합니다.

## <a name="operating-system-support"></a>운영 체제 지원

Linux 및 macOS 드라이버 버전 17, 13.1 및 13은 다음 운영 체제의 64비트 버전에서 지원됩니다.

|지원되는 운영 체제     |17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|--|
|Apple OS X 10.11(El Capitan)  | |Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.12(Sierra)     | |Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.13(Sierra)|Y|Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.14(Mojave)     |Y|Y|Y| | | | | |
|Apple macOS 10.15(Catalina.properties)   |Y| | | | | | | |
|Alpine Linux 3.11              |Y| | | | | | | |
|Debian Linux 8                 | |Y|Y|Y|Y|Y|Y|Y|
|Debian Linux 9                 |Y|Y|Y|Y|Y|Y|Y|Y|
|Debian Linux 10                |Y|Y| | | | | | |
|Oracle Linux 8                 |Y| | | | | | | |
|RedHat Enterprise Linux 6      |Y|Y|Y|Y|Y|Y|Y|Y|
|RedHat Enterprise Linux 7      |Y|Y|Y|Y|Y|Y|Y|Y|
|RedHat Enterprise Linux 8      |Y|Y| | | | | | |
|SUSE Linux Enterprise Server 11<sup>1</sup>|Y|Y|Y|Y|Y|Y|Y|Y|
|SUSE Linux Enterprise Server 12|Y|Y|Y|Y|Y|Y|Y|Y|
|SUSE Linux Enterprise Server 15|Y|Y|Y| | | | | |
|Ubuntu Linux 14.04             | |Y|Y|Y|Y|Y|Y|Y|
|Ubuntu Linux 16.04             |Y|Y|Y|Y|Y|Y|Y|Y|
|Ubuntu Linux 18.04             |Y|Y|Y|Y| | | | |
|Ubuntu Linux 19.10             |Y| | | | | | | |

<sup>1</sup> ODBC Driver 17은 SUSE Linux Enterprise Server 11 SP4만 지원합니다.

[ODBC 드라이버 설치(Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) 및 [ODBC 드라이버 설치(macOS)](install-microsoft-odbc-driver-sql-server-macos.md)에서 설명한 대로, Linux 및 macOS 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1, 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 설치 패키지는 사용자 배포의 패키지 관리 시스템을 사용하여 설치된 경우 드라이버의 종속성을 자동으로 해결합니다.

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
* 64비트 SQLLEN/SQLULEN용으로 빌드된 64비트 UnixODBC 2.3.0 드라이버 관리자입니다. 이후 버전의 64비트 UnixODBC 드라이버 관리자는 Linux 기반 ODBC 드라이버로 지원되지 않습니다. 자세한 내용은 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 을 참조하세요.  
  
* ODBC Driver for **Red Hat Enterprise Linux 5(64비트)** 에는 다음 패키지가 필요하며 여기에서 다운로드할 수 있습니다. [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* ODBC Driver for  **Red Hat Enterprise Linux 6(64비트)** 에는 다음 패키지가 필요하며 여기에서 다운로드할 수 있습니다. [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* ODBC Driver for **SUSE Linux Enterprise 11 Service Pack 2(64비트)** 에는 다음 패키지가 필요하며 여기에서 다운로드할 수 있습니다. [Microsoft ODBC Driver 11 Preview for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
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
