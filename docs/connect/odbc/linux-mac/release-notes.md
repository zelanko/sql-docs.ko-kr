---
title: "릴리스 정보-Microsoft ODBC Driver for Linux와 macOS에서 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 84bb78e184f1bca9e683aeebf46b178e3a7dd61f
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Microsoft ODBC Driver for Linux와 macOS에서 SQL Server에 대 한 릴리스 정보
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 에 대 한 ODBC Driver 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux와 macOS에서  

에 대 한 ODBC Driver 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 상시 암호화와 Microsoft SQL Server 2016와 함께 사용 하는 경우 Azure Active Directory에 대 한 지원을 추가 합니다.

**지원 되는 새 배포**: OS X 10.11와 macOS 10.12 macOS에서 ODBC 드라이버의 첫 번째 릴리스에서 지원 됩니다. Ubuntu 16.10가 이제도 함께 지원 Red Hat 6, 7 및 SUSE 12입니다. 각 플랫폼에 플랫폼 관련 패키지 (RPM 또는 DEB)을 쉽게 설치 및 구성 합니다.  참조 [드라이버 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 설치 지침에 대 한 합니다.

**unixODBC 드라이버 관리자 2.3.1 지원 변경 사항을**: The ODBC 드라이버는 더 이상 unixODBC 드라이버 관리자에 대 한 사용자 지정 패키지에 따라 다릅니다 (RedHat 6에서 제외), 대신 UnixODBC 종속성을 확인할 배포 패키지 관리자 사용 분포의 리포지토리에서 합니다.

**BCP API 지원**: Linux와 macOS ODBC 드라이버는 이제 사용을 지원는 [BCP API 함수 (**bcp_init**등.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>새로운 기능에 대 한 Microsoft ODBC driver 13.0 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] linux  
Microsoft ODBC Driver for SQL Server 13.0, SQL Server 2014 및 SQL Server 2016 이제도 지원 됩니다.  

**지원 되는 새 배포**:

이제 Ubuntu가 Red Hat 및 SUSE와 함께 지원됩니다. 각 플랫폼에 플랫폼 관련 패키지 (RPM 또는 DEB)을 쉽게 설치 및 구성 합니다.  참조 [드라이버 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 설치 지침에 대 한 합니다.

**unixODBC 드라이버 관리자 2.3.1 지원**: 최신 드라이버 관리자를 외에도 이기도 쉽게 설치 및 구성 하는이 종속성이 설치에 대 한 패키지입니다.  

**투명 네트워크 IP 확인**: 투명 네트워크 IP 확인은 첫 번째 호스트의 IP 없는 해결 된 경우에서 드라이버의 연결 순서에 영향을 주는 기존 다중 서브넷 장애 조치 기능을 수정 버전 응답 하 고 호스트와 관련 된 여러 Ip 않습니다.

**TLS 1.2 지원**: SQL Server와의 보안 통신에 사용 되는 이제 Linux에서 SQL server의 Microsoft ODBC 드라이버 13.0 TLS 1.2 지원 합니다.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>새로운 기능에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] linux  
SUSE Linux(Preview)의 ODBC 드라이버는 64비트 SUSE Linux Enterprise 11 서비스 팩 2를 지원합니다. 자세한 내용은 참조 [시스템 요구 사항](../../../connect/odbc/linux-mac/system-requirements.md)합니다.  

Linux 기반 ODBC 드라이버 지원 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]합니다. 자세한 내용은 참조 [고가용성, 재해 복구에 대 한 Linux 지원이 ODBC 드라이버](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)합니다.  

Linux 기반 ODBC 드라이버는 Microsoft Azure SQL 데이터베이스에 대한 연결을 지원합니다. 자세한 내용은 [방법: ODBC를 사용하여 Microsoft Azure SQL 데이터베이스에 연결](http://msdn.microsoft.com/library/hh974312.aspx)을 참조하세요.  

`-l` 옵션 (로그인 시간 제한)에 추가 되었습니다 `bcp`합니다. 자세한 내용은 참조 [연결과 **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)합니다.

