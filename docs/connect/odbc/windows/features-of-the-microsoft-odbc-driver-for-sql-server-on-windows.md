---
title: Windows 기반 Microsoft ODBC Driver for SQL Server의 기능 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: v-makouz
ms.author: v-daenge
ms.openlocfilehash: 2143be3396e16eb61fd36ac5956c11626363bcf5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928266"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 기반 Microsoft ODBC Driver for SQL Server의 기능
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Windows의 Microsoft ODBC Driver 17.4 for SQL Server

ODBC 드라이버 17.4에는 TCP 연결 유지 설정을 조정하는 기능이 포함되어 있습니다. 이 설정은 드라이버 또는 DSN 레지스트리 키에 값을 추가하여 수정할 수 있습니다. 키는 시스템 데이터 원본의 경우 `HKEY_LOCAL_MACHINE\Software\ODBC\`에 있고, 사용자 데이터 원본의 경우 `HKEY_CURRENT_USER\Software\ODBC\`에 있습니다. DSN의 경우 `...\Software\ODBC\ODBC.INI\<DSN Name>`에 값을 추가하고, 드라이버의 경우 `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`에 값을 추가해야 합니다.

자세한 내용은 [ODBC 구성 요소 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-odbc-components.md)을 참조하세요.

값은`REG_SZ`이며 다음과 같습니다.

- `KeepAlive`는 연결을 유지하기 위해 TCP에서 연결 유지 패킷을 보내는 빈도를 제어합니다. 기본값은 30초입니다.

- `KeepAliveInterval`은 응답이 수신될 때까지 연결 유지 재전송을 구분하는 간격을 결정합니다. 기본값은 1초입니다.



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Windows 기반 Microsoft ODBC Driver 13.1 for SQL Server

ODBC Driver 13.1 for SQL Server에는 이전 버전(11)의 모든 기능이 포함되어 있으며 Microsoft SQL Server 2016과 함께 사용하는 경우 Always Encrypted 및 Azure Active Directory 인증에 대한 지원이 추가되었습니다.  
  
상시 암호화를 사용하면 클라이언트가 클라이언트 애플리케이션의 중요한 데이터를 암호화하고 암호화 키를 SQL Server에 표시하지 않을 수 있습니다. 클라이언트 컴퓨터에 설치된 상시 암호화 지원 드라이버가 SQL Server 클라이언트 애플리케이션의 중요한 데이터를 자동으로 암호화하고 암호 해독합니다. 드라이버는 데이터를 SQL Server로 전달하기 전에 중요한 열의 데이터를 암호화하고 애플리케이션에 대한 의미 체계가 유지되도록 자동으로 쿼리를 다시 작성합니다. 마찬가지로, 드라이버는 쿼리 결과에 포함되고 암호화된 데이터베이스 열에 저장된 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화와 ODBC 드라이버 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)을 참조하세요.
 
Azure Active Directory를 통해 사용자, DBA 및 애플리케이션 프로그래머는 Azure AD(Azure Active Directory)의 ID를 사용하여 Microsoft Azure SQL Database 및 Microsoft SQL Server 2016에 연결하는 메커니즘으로 Azure Active Directory 인증을 사용할 수 있습니다. 자세한 내용은 [ODBC 드라이버에서 Azure Active Directory 사용](../../../connect/odbc/using-azure-active-directory.md) 및 [Azure Active Directory 인증을 사용하여 SQL Database 또는 SQL Data Warehouse에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)을 참조하세요.   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Windows의 Microsoft ODBC Driver 11 for SQL Server  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 제공되는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]Native Client ODBC 드라이버에 대한 모든 기능이 포함되어 있습니다. 자세한 내용은 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Windows 운영 체제에서 제공되는 ODBC 드라이버를 기반으로 합니다. 자세한 내용은 [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx)를 참조하세요.  
  
이 릴리스의 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에는 다음과 같은 새 기능이 포함되어 있습니다.  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>로그인 제한 시간을 지정하기 위한 bcp.exe -l 옵션
 
-l 옵션을 사용하여 서버에 연결을 시도할 때 `bcp.exe`에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 제한 시간(초)을 지정합니다. 기본 로그인 제한 시간은 15초입니다. 로그인 제한 시간은 0에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 `bcp.exe`는 오류 메시지를 생성합니다. 값 0은 제한 시간을 무한으로 지정합니다. 약 10초 미만의 로그인 시간 제한은 안정적이지 않습니다.  
  
### <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 [드라이버 인식 연결 풀링](https://msdn.microsoft.com/library/hh405031(VS.85).aspx)을 지원합니다. 자세한 내용은 [ODBC Driver for SQL Server에서 드라이버 인식 연결 풀링 | Microsoft Docs](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)을 참조하세요.  
  
### <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 [비동기 실행(알림 방법)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx)을 지원합니다. 사용 샘플은 [비동기 실행&#40;알림 방법&#41; 샘플](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)을 참조하세요.  
  
### <a name="connection-resiliency"></a>연결 복원력
애플리케이션이 Microsoft Azure SQL 데이터베이스에 연결되어 있는지 확인하려면 Windows 기반 ODBC 드라이버가 유휴 연결을 복원하면 됩니다. 자세한 내용은 [Windows ODBC 드라이버에서 연결 복원](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)을 참조하세요.  
  
## <a name="behavior-changes"></a>동작 변경 내용

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 `-y0`에 `sqlcmd.exe` 옵션을 지정하면 표시 너비가 0인 경우 출력이 1MB로 잘렸습니다.
  
ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]부터 `-y0`이 지정된 경우 단일 열에서 검색할 수 있는 데이터 양에 제한이 없습니다. 이제 `sqlcmd.exe`가 2GB([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 최대 데이터 형식) 정도의 열을 스트림합니다.  
  
또 다른 차이점은 `-h`와 `-y0`를 모두 지정하면 옵션이 호환되지 않는다는 오류를 생성하는 것입니다. 열 제목 사이에 인쇄할 행 수를 지정하고 `-h`과 호환된 적 없었던 `-y0`는 무시되었지만 헤더는 인쇄되지 않았습니다.
  
`-y0`은 반환되는 데이터 크기에 따라 서버와 네트워크 모두에서 성능 문제를 일으킬 수 있습니다.

## <a name="see-also"></a>참고 항목  
[Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
