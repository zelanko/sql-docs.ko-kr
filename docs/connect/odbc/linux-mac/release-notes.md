---
title: 릴리스 정보 - Linux 및 macOS 기반 Microsoft ODBC Driver for SQL Server on Linux 및 macOS | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: a12475a1f759be12949d5642e5af865b10e4af99
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786028"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Linux 및 macOS 기반 Microsoft ODBC Driver for SQL Server에 대한 릴리스 정보
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2의 새로운 기능

**지원 되는 새 배포**: Ubuntu 18.04

**추가 기능**:

자세한 내용은 SQL Server 및 Azure SQL Database에 대 한 데이터 분류 참조 [데이터 분류](../data-classification.md)

SQLBrowseConnect

에 대 한 동적 종속성 `libcurl`:
- 이 버전부터는 `libcurl` 패키지는 명시적 종속성을 하지 않습니다. `libcurl` OpenSSL 또는 NSS 반드시 Azure Key Vault 또는 Azure Active Directory 인증을 사용 하는 경우에 대 한 패키지 있습니다. 오류가 발생 하는 경우와 관련 하 여 `libcurl`, 설치 되어 있는지 확인 합니다.

ConnectRetryCount 및 ConnectRetryInterval 연결 문자열 키워드를 사용 하 여 연결 복원 력 유휴 (자세한 내용은 [Windows ODBC 드라이버의 연결 복원 력](../windows/connection-resiliency-in-the-windows-odbc-driver.md)):
- 사용 하 여 `SQL_COPT_SS_CONNECT_RETRY_COUNT`(읽기 전용)에 연결 다시 시도 횟수를 검색 합니다.
- 사용 하 여 `SQL_COPT_SS_CONNECT_RETRY_INTERVAL`(읽기 전용) 연결 다시 시도 간격의 길이 검색 하도록 합니다.
- 연결은 기본적으로 한 번 다시 시도 됩니다.


[버그 수정](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1의 새로운 기능

**추가 기능**:

에 대 한 지원 `SQL_COPT_SS_CEKCACHETTL` 하 고 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성 (자세한 내용은 참조 하십시오 [ODBC Driver for SQL Server를 사용 하 여 상시 암호화를 사용 하 여](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 열 암호화 키의 로컬 캐시에 존재 하는 시간을 제어 뿐만 아니라이 플러시 수 있습니다.
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 만 목록을 사용합니다 하 여 지정 된 열 마스터 키의 AE 작업을 제한 하는 응용 프로그램 사용



로드에 대 한 지원 합니다 `.rll` 기본 위치에서 (자세한 내용은 참조 하십시오 [설치 문서에서 ' 리소스 파일 로드 ' 섹션](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[버그 수정](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17의 새로운 기능

**지원 되는 새 배포**: macOS High Sierra 및 Ubuntu 17.10 

**성능 향상**: 드라이버 u t F-8 월 16에서 변환 하는 경우 성능 향상 x 10 보다 큽니다.

**추가 기능**:

BCP API에 대 한 always Encrypted 지원

새 연결 문자열 특성 UseFMTOnly 드라이버를 임시 테이블을 요구 하는 특별 한 경우에서 레거시 메타 데이터를 사용 하면 됩니다.

Azure SQL 관리 되는 인스턴스 (확장 된 비공개 미리 보기)를 지원 합니다. 
> [!NOTE]
> 관리 되는 인스턴스를 사용 하는 경우 몇 가지 차이점이 가지:
> -   FILESTREAM 지원 되지 않습니다. 
> -   로컬 파일 시스템 액세스는 지원 되지 않지만 tracefiles 등을 위해 필요 하지 않습니다. 
> -   로컬에서 UDT를 만들 경로가 지원 되지 않습니다 
> -   Windows 통합 인증이 지원 되지 않습니다. 
> -   DTC는 지원되지 않습니다. 
> -   'sa' 계정 없는 (기본 계정 이라고 'cloudSA')
> -   잘못 된 서버 이름을 반환 하는 TDS 토큰 오류 (0xAA)
> -   데이터베이스 이름에 특수 문자는 지원 되지 않습니다. 
> -   [Dbname1] ALTER DATABASE MODIFY NAME = [dbname2] 지원 되지 않습니다
> -   오류 메시지는 항상 언어에 관계 없이 영어로 표시 됩니다 (Azure와 동일) 설정 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1의 새로운 기능  

ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 상시 암호화 및 Microsoft SQL Server 2016과 함께 사용 하는 경우 Azure Active Directory에 대 한 지원이 추가 되었습니다.

**지원 되는 새 배포**: OS X 10.11 및 macOS 10.12 macOS에서 ODBC 드라이버의 첫 번째 릴리스에서 지원 됩니다. Ubuntu 16.10 이제도 함께 지원 됩니다 Red Hat 6, 7 및 SUSE 12입니다. 각 플랫폼에 플랫폼 관련 패키지 RPM 또는 DEB 손쉬운 설치 및 구성 합니다.  참조 [드라이버를 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 설치 지침에 대 한 합니다.

**unixODBC 드라이버 관리자 2.3.1 지원 변경**: The ODBC 드라이버 이상 unixODBC 드라이버 관리자에 대 한 사용자 지정 패키지에 따라 달라 집니다 (RedHat 6에서 제외), UnixODBC 종속성을 해결 하려면 배포 패키지 관리자를 대신 사용 분포의 리포지토리에서 합니다.

**BCP API 지원을**: Linux 및 macOS의 ODBC 드라이버는 이제 사용을 지원 합니다 [BCP API 함수 (**bcp_init**등.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Microsoft ODBC Driver 13.0 for의 새로운 기능 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] linux  
Microsoft ODBC Driver 13.0 for SQL Server를 사용 하 여 SQL Server 2014 및 SQL Server 2016 이제 지원 됩니다.  

**지원 되는 새 배포**:

이제 Ubuntu가 Red Hat 및 SUSE와 함께 지원됩니다. 각 플랫폼에 플랫폼 관련 패키지 RPM 또는 DEB 손쉬운 설치 및 구성 합니다.  참조 [드라이버를 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 설치 지침에 대 한 합니다.

**unixODBC 드라이버 관리자 2.3.1 지원**: 최신 드라이버 관리자를 외에도 이기도 패키지를 설치 및 구성을 용이 하 게 하는이 종속성을 설치 합니다.  

**Transparent Network IP Resolution**: Transparent Network IP Resolution은 첫 번째 호스트 이름의 IP 않습니다 해결 된 경우에서 드라이버의 연결 순서에 영향을 주는 기존 다중 서브넷 장애 조치 기능의 수정 버전 응답 되며 호스트와 연결 된 여러 Ip입니다.

**TLS 1.2 지원**: SQL Server를 사용 하 여 보안 통신을 사용 하는 경우 이제는 Microsoft ODBC Driver 13.0 for SQL Server Linux TLS 1.2 지원 합니다.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Linux 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11의 새로운 기능  
SUSE Linux(Preview)의 ODBC 드라이버는 64비트 SUSE Linux Enterprise 11 서비스 팩 2를 지원합니다. 자세한 내용은 [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md)을 참조하세요.  

Linux 기반 ODBC 드라이버는 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]을 지원합니다. 자세한 내용은 [Linux Support for High Availability, Disaster Recovery 기반 ODBC 드라이버](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)합니다.  

Linux 기반 ODBC 드라이버는 Microsoft Azure SQL 데이터베이스에 대한 연결을 지원합니다. 자세한 내용은 [방법: ODBC를 사용하여 Microsoft Azure SQL 데이터베이스에 연결](http://msdn.microsoft.com/library/hh974312.aspx)을 참조하세요.  

합니다 `-l` (로그인 시간 제한) 옵션에 추가 되었습니다 `bcp`합니다. 자세한 내용은 [Connecting with **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)을 참조하세요.
