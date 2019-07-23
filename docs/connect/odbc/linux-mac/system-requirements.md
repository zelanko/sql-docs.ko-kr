---
title: 시스템 요구 사항(ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 919a386af2ff0ceb714daf2c48ac199d2cbfb46d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008715"
---
# <a name="system-requirements"></a>시스템 요구 사항
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver를 사용하기 위한 요구 사항을 나열합니다.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>SQL Server용 Microsoft ODBC Driver 13, 13.1 및 17

Linux 및 macOS 드라이버는 다음 운영 체제의 64비트 버전에만 사용할 수 있습니다.

|운영 체제|지원되는 드라이버 버전|
|------------------------------------|--------------------------------|
|Apple OS X 10.11(El Capitan)|13, 13.1, 17|
|Apple macOS 10.12(Sierra)|13, 13.1, 17|
|Apple macOS 10.13(Sierra)|17| 
|Apple macOS 10.14(Mojave)|17| 
|Debian Linux 8|13, 13.1, 17|
|Debian Linux 9|17|
|RedHat Enterprise Linux 6|13, 13.1, 17|
|RedHat Enterprise Linux 7|13, 13.1, 17|
|SuSE Linux Enterprise Server 11|13, 13.1, 17 <br /><br /> **참고:** ODBC 드라이버 17은 SuSE Linux Enterprise Server 11 SP4만 지원합니다.|
|SuSE Linux Enterprise Server 12|13, 13.1, 17|
|SuSE Linux Enterprise Server 15|17|
|Ubuntu Linux 14.04|13, 13.1, 17|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17|
|Ubuntu Linux 16.10|13, 13.1|
|Ubuntu Linux 17.04|17| 
|Ubuntu Linux 17.10|17|
|Ubuntu Linux 18.04|17| 
|Ubuntu Linux 18.10|17| 

[드라이버 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)에서 설명한 대로 Linux 및 macOS 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC 드라이버 13, 13.1 및 17[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 설치 패키지는 사용자 배포의 패키지 관리 시스템을 사용하여 설치된 경우 드라이버의 종속성을 자동으로 해결합니다.

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   64비트 SQLLEN/SQLULEN용으로 빌드된 64비트 UnixODBC 2.3.0 드라이버 관리자입니다. 이후 버전의 64비트 UnixODBC 드라이버 관리자는 Linux 기반 ODBC 드라이버로 지원되지 않습니다. 자세한 내용은 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 을 참조하세요.  
  
-   ODBC Driver for **Red Hat Enterprise Linux 5(64비트)** 에는 다음 패키지가 필요하며 [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)에서 다운로드할 수 있습니다.  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   ODBC Driver for **Red Hat Enterprise Linux 6(64비트)** 에는 다음 패키지가 필요하며 [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)에서 다운로드할 수 있습니다.  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   ODBC Driver for **SUSE Linux Enterprise 11 서비스 팩 2(64비트)** 에는 다음 패키지가 필요하며 [Microsoft ODBC Driver 11 Preview for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)에서 다운로드할 수 있습니다.  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>참고 항목
[드라이버 관리자 설치](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
