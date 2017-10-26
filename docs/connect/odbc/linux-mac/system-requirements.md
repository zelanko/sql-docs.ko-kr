---
title: "시스템 요구 사항 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 75c8c9daea3f26dc694ae66597649f399a986456
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="system-requirements"></a>시스템 요구 사항
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 요구 사항을 사용 하는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux와 macOS에서 합니다.

## <a name="microsoft-odbc-driver-13-and-131-for-sql-server"></a>Microsoft ODBC Driver 13 및 13.1 for SQL Server

Linux와 macOS 드라이버는 다음 운영 체제의 64 비트 버전에 대해서만 사용할 수 있습니다.

- Apple macOS 10.12 (시에라)
- Apple OS X 10.11 (El Capitan)
- Debian Linux 8
- RedHat Enterprise Linux 6
- RedHat Enterprise Linux 7
- SuSE Linux Enterprise Server 11
- SuSE Linux Enterprise Server 12
- Ubuntu 14.04 Linux
- Ubuntu Linux 15.10
- Ubuntu Linux 16.04
- Ubuntu Linux 16.10

설치 패키지로 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 및에 대 한 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux와 macOS에서 드라이버의 종속성 에설명된대로패키지관리시스템의분포를사용하여을설치할때자동으로해결[드라이버 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   64비트 SQLLEN/SQLULEN용으로 빌드된 64비트 UnixODBC 2.3.0 드라이버 관리자입니다. 이후 버전의 64비트 UnixODBC 드라이버 관리자는 Linux 기반 ODBC 드라이버로 지원되지 않습니다. 자세한 내용은 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 을 참조하세요.  
  
-   에 대 한 ODBC 드라이버 **Red Hat Enterprise Linux 5 (64 비트)** 는 다음 패키지가 필요 하며 여기에 다운로드할 수 있습니다: [Microsoft ODBC Driver 11 for SQL Server-Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   e2fsprogs-libs  
    -   krb5-libs  
    -   openssl  
  
-   에 대 한 ODBC 드라이버 **Red Hat Enterprise Linux 6 (64 비트)** 는 다음 패키지가 필요 하며 여기에 다운로드할 수 있습니다: [Microsoft ODBC Driver 11 for SQL Server-Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   libuuid  
    -   krb5-libs  
    -   openssl  
  
-   에 대 한 ODBC 드라이버 **SUSE Linux Enterprise 11 서비스 팩 2 (64 비트)** 는 다음 패키지가 필요 하며 여기에 다운로드할 수 있습니다: [Microsoft ODBC Driver 11 for SQL Server-SUSE Linux Preview](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   glibc  
    -   libstdc++46  
    -   libgcc46  
    -   libuuid1  
    -   krb5  
    -   libopenssl0_9_8  
  
## <a name="see-also"></a>관련 항목:
[드라이버 관리자 설치](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)  

