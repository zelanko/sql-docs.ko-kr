---
title: "Microsoft ODBC Driver for SQL Server의 기능 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
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
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3916b53dcccf77cea96b5d12ce61273569b33dc3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 기반 Microsoft ODBC Driver for SQL Server의 기능
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server

ODBC Driver 13.1 for SQL Server 이전 버전 (11)의 모든 기능을 포함 하 고 Microsoft SQL Server 2016와 함께 사용 하는 경우 상시 암호화와 Azure Active Directory 인증에 대 한 지원을 추가 합니다.  
  
상시 암호화를 사용하면 클라이언트가 클라이언트 응용 프로그램의 중요한 데이터를 암호화하고 암호화 키를 SQL Server에 표시하지 않을 수 있습니다. 클라이언트 컴퓨터에 설치된 상시 암호화 지원 드라이버가 SQL Server 클라이언트 응용 프로그램의 중요한 데이터를 자동으로 암호화하고 암호 해독합니다. 드라이버는 데이터를 SQL Server로 전달하기 전에 중요한 열의 데이터를 암호화하고 응용 프로그램에 대한 의미 체계가 유지되도록 자동으로 쿼리를 다시 작성합니다. 마찬가지로, 드라이버는 쿼리 결과에 포함되고 암호화된 데이터베이스 열에 저장된 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 참조 [ODBC 드라이버를 사용 하 여 항상 암호화를 사용 하 여](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)합니다.
 
Azure Active Directory 사용자, DBA, 및 응용 프로그램 프로그래머의 Azure Active Directory (Azure AD에서에서 id를 사용 하 여 Microsoft SQL Server 2016 및 Microsoft Azure SQL 데이터베이스에 연결 하는 메커니즘으로 Azure Active Directory 인증을 사용 하도록 허용 ). 자세한 내용은 참조 [를 사용 하 여 Azure Active Directory와 ODBC 드라이버](../../../connect/odbc/using-azure-active-directory.md), 및 [SQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여 연결할](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/)합니다.   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Windows의 Microsoft ODBC Driver 11 for SQL Server  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 에서 제공되는 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]Native Client ODBC 드라이버에 대한 모든 기능이 포함되어 있습니다. 자세한 내용은 [SQL Server Native Client 프로그래밍](http://msdn.microsoft.com/library/ms130892.aspx)을 참조하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ODBC 드라이버는 Windows 운영 체제에서 제공되는 ODBC 드라이버를 기반으로 합니다. 자세한 내용은 [Windows Data Access Components SDK](http://msdn.microsoft.com/library/aa968814(VS.85).aspx)를 참조하세요.  
  
이 릴리스의 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 에는 다음 새 기능이 포함되어 있습니다.  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>로그인 제한 시간을 지정 하기 위한 – l 옵션이 bcp.exe
 
초를 대기한 수를 지정 하는 – l 옵션은 `bcp.exe` 로그인을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 서버에 연결 하려고 하면 제한 시간입니다. 기본 로그인 제한 시간은 15 초입니다. 로그인 제한 시간을 0에서 65534 사이의 숫자 여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 `bcp.exe`는 오류 메시지를 생성합니다. 값이 0에는 무한 시간 제한을 지정합니다. 약 10 초 미만의 로그인 시간 제한은 안정적있지 않습니다.  
  
### <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 지원 [드라이버 인식 연결 풀링](http://msdn.microsoft.com/library/hh405031(VS.85).aspx)합니다. 자세한 내용은 [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)을 참조하세요.  
  
### <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 지원 [비동기 실행 (알림 방법)](http://msdn.microsoft.com/library/hh405038(VS.85).aspx)합니다. 사용 예제를 참조 하세요. [비동기 실행 &#40; 알림 방법 &#41; 샘플](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)합니다.  
  
### <a name="connection-resiliency"></a>연결 복원력
응용 프로그램이 Microsoft Azure SQL 데이터베이스에 연결되어 있는지 확인하려면 Windows 기반 ODBC 드라이버가 유휴 연결을 복원하면 됩니다. 자세한 내용은 [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)을 참조하세요.  
  
## <a name="behavior-changes"></a>동작 변경 내용

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client는 `-y0` 옵션에 대 한 `sqlcmd.exe` 출력이 디스플레이 width가 0 경우 1MB에서 잘립니다.
  
ODBC Driver 11 for부터 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], 단일 열에 검색할 수 있는 데이터의 양에 제한이 없는 때 `–y0` 지정 합니다. `sqlcmd.exe`이제 2GB 정도의 열 스트림 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식 최대).  
  
또 다른 차이점은 해당 둘 다 지정 하면 `-h` 및 `-y0` 이제에서 옵션이 호환 되지 않습니다 보고 오류를 생성 합니다. `-h`열 머리글 사이 출력할 행 수를 지정 하 고 호환 되지 `-y0`, 머리글이 인쇄 되지 않지만 무시 되었습니다.
  
`-y0` 서버와 반환 된 데이터의 크기에 따라 네트워크 모두에서 성능 문제를 일으킬 수 있습니다.

## <a name="see-also"></a>관련 항목:  
[Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  

