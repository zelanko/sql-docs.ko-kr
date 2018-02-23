---
title: "드라이버 관리자 (ODBC Driver for SQL Server) 설치 | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 36f432e883b56759d46304239715a00c06334d3a
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="installing-the-driver-manager"></a>드라이버 관리자 설치
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서는 Linux와 macOS에서 SQL Server에 대 한 모든 버전의 Microsoft ODBC 드라이버와 사용 하기 위해 unixODBC 드라이버 관리자를 설치 하는 지침을 포함 합니다.  

> [!IMPORTANT]  
> unixODBC 드라이버 관리자를 설치하기 전에 컴퓨터에 설치된 드라이버 관리자 패키지를 삭제합니다. unixODBC 드라이버 관리자를 설치하면 기존 드라이버 관리자에 오류가 발생할 수 있습니다.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Microsoft ODBC Driver 13, 13.1, 및 17 용 드라이버 관리자 설치
드라이버 관리자 종속성이 자동으로 해결 패키지 관리 시스템에서 Microsoft ODBC Driver 13, 13.1, 또는 17 Linux 또는 macOS에서 SQL Server에 대 한 지침에 따라 설치할 때 [Microsoft ODBC 드라이버 설치 Linux 또는 macOS에서 SQL Server에 대 한](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다. 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server용 드라이버 관리자 설치  

(SUSE와 Red Hat Linux만)

**설치 스크립트를 사용 하 여**  
  
> [!IMPORTANT]  
> 이러한 지침은를 참조 `msodbcsql-11.0.2270.0.tar.gz`, Red Hat Linux에 대 한 설치 파일인 합니다. SUSE Linux 용 Preview를 설치 하는 경우 파일 이름이 `msodbcsql-11.0.2260.0.tar.gz`합니다.  

드라이버 관리자를 설치하려면  
  
1.  루트 권한이 있는지 확인합니다.  
  
2.  디렉터리로 이동 위치는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ODBC 드라이버 다운로드가 라는 파일을 배치한 `msodbcsql-11.0.2270.0.tar.gz`합니다. Linux 버전과 일치하는 \*.tar.gz 파일이 있는지 확인합니다. 파일을 추출 하려면 다음 명령을 실행: **tar xvzf msodbcsql-11.0.2270.0.tar.gz**합니다.  

3.  변경 된 `msodbcsql-11.0.2270.0` 디렉터리 라는 파일을 있습니다 표시 되어야 `build_dm.sh`합니다. 실행할 수 있습니다 `build_dm.sh` unixODBC 드라이버 관리자를 설치 합니다.

4.  사용 가능한 옵션 목록을 보려면 다음 명령을 실행: **./build_dm.sh-도움말**합니다.  
  
5.  다음 명령을 실행 하는 경우를 설치할 준비가 되었습니다. 하 고 컴퓨터가 FTP 통해 외부 사이트에 액세스할 수 있습니다: **./build_dm.sh**합니다.

컴퓨터가 FTP 통해 외부 사이트에 액세스할 수 없는 경우 get `unixODBC-2.3.0.tar.gz`합니다. 가져올 수 있습니다 `unixODBC-2.3.0.tar.gz` 에서 [http://www.unixodbc.org](http://www.unixodbc.org/)합니다. 클릭는 **다운로드** 다운로드 페이지로 이동 하는 페이지의 왼쪽에 링크 합니다. 그런 다음 적절한 링크를 클릭하여 unixODBC-2.3.0(unixODBC-2.3.1 아님)을 다운로드합니다. UnixODBC 2.3.1은이 버전의 지원 되지 않습니다는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. UnixODBC 드라이버 관리자 설치를 시작 하려면 다음 명령을 실행: **./build_dm.sh-다운로드 url file://unixODBC-2.3.0.tar.gz =**합니다.  

6.  형식 **예** 파일의 압축 해제를 진행할 수 있습니다. 이 부분의 프로세스를 완료 하려면 최대 5 분까지 걸릴 수 있습니다.  

7.  스크립트가 실행을 중지한 후 화면의 지침을 따라 unixODBC 드라이버 관리자를 설치합니다.

이제 드라이버를 설치할 준비가 되었습니다. 자세한 내용은 참조 [Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.  

수동 설치

설치 스크립트가 완료할 수 없는 경우 적절한 드라이버 관리자를 직접 구성하고 빌드합니다.

1.  이전에 설치된 unixODBC 버전(예: unixODBC 2.2.11)을 제거합니다. Red Hat Enterprise Linux 5 또는 6에서 다음 명령을 실행: **yum 제거 unixODBC**합니다. SUSE Linux enterprise **zypper 제거 unixODBC**합니다.  
  
2.  로 이동 [http://www.unixodbc.org](http://www.unixodbc.org/)합니다. 클릭는 **다운로드** 다운로드 페이지로 이동 하는 페이지의 왼쪽에 링크 합니다. 그런 다음 적절한 링크를 클릭하여 unixODBC-2.3.0.tar.gz 파일을 컴퓨터에 저장합니다. UnixODBC 2.3.1은이 버전의 지원 되지 않습니다는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
3.  Linux 컴퓨터에서 명령을 실행: **tar xvzf unixodbc-2.3.0.tar.gz**합니다.  
  
4.  unixODBC-2.3.0 디렉터리로 변경합니다.  
  
5.  명령 프롬프트에서 명령을 실행: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8"**합니다.  
  
6.  명령 프롬프트에서 명령을 실행: **CPPFLAGS 내보내기**합니다.  
  
7.  명령 프롬프트에서 명령을 실행: **". / 구성-= / usr-libdir = / usr/lib64-sysconfdir = / 등-enable gui 접두사 = 아니요-enable 드라이버 = 아니요-enable iconv-와 iconv-char-enc UTF8-와 iconv-ucode-enc = UTF16LE ="**.  
  
8.  명령 프롬프트 (루트로 로그인)에서 명령을 실행: **확인**합니다.  
  
9. 명령 프롬프트 (루트로 로그인)에서 명령을 실행: **설치 확인**합니다.  

이제 드라이버를 설치할 준비가 되었습니다. 자세한 내용은 참조 [Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목:
[Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)
