---
title: Linux 및 macOS 기반 ODBC 드라이버의 알려진 문제
ms.date: 03/05/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0486cea609f0ab6bcc1261d6cad26f47f123476f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80912529"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Linux 및 macOS 기반 ODBC 드라이버의 알려진 문제

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에는 Linux 및 macOS 기반 Microsoft ODBC Driver 13, 13.1 및 17 for SQL Server를 사용하는 경우 알려진 문제 목록이 포함되어 있습니다. 연결 문제를 해결하는 단계도 제공됩니다.

## <a name="known-issues"></a>알려진 문제

추가 문제는 [Microsoft ODBC 드라이버 팀 블로그](https://blogs.msdn.com/b/sqlnativeclient/)에 게시됩니다.  

- 시스템 라이브러리 제한으로 인해 Alpine Linux는 더 적은 수의 문자 인코딩과 로캘을 지원합니다. 예를 들어 en_US.UTF-8은 사용할 수 없습니다. 자세한 내용은 [musl libc - glibc의 기능 차이점](https://wiki.musl-libc.org/functional-differences-from-glibc.html)을 참조하세요.

- Windows, Linux 및 macOS는 PUA(프라이빗 사용 영역) 또는 EUDC(최종 사용자 정의)의 문자를 다르게 변환합니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 내에서 서버에 수행되는 변환은 Windows 변환 라이브러리를 사용합니다. 드라이버의 변환에는Windows, Linux 또는 macOS 변환 라이브러리를 사용합니다. 이러한 변환을 수행할 때 각 라이브러리는 다른 결과를 생성할 수 있습니다. 자세한 내용은 [최종 사용자 정의 및 프라이빗 사용 영역 문자](/windows/desktop/Intl/end-user-defined-characters)를 참조하세요.

- 클라이언트 인코딩이 UTF-8인 경우 드라이버 관리자가 항상 UTF-8에서 UTF-16으로 올바르게 변환하는 것은 아닙니다. 현재 문자열에서 1개 이상의 문자가 올바른 UTF-8 문자가 아닌 경우 데이터 손상이 발생합니다. ASCII 문자는 올바르게 매핑됩니다. ODBC API의 SQLCHAR 버전(예: SQLDriverConnectA)을 호출할 때 드라이버 관리자가 이 변환을 시도합니다. ODBC API의 SQLWCHAR 버전(예: SQLDriverConnectW)을 호출할 때 드라이버 관리자가 이 변환을 시도하지 않습니다.  

- *SQLBindParameter*의 **ColumnSize** 매개 변수는 SQL 형식의 문자 수를 가리키는 반면에, *BufferLength*는 애플리케이션의 버퍼에 있는 바이트 수입니다. 그러나 SQL 데이터 형식이 `varchar(n)` 또는 `char(n)`이고, 애플리케이션이 매개 변수를 SQL_C_CHAR 또는 SQL_C_VARCHAR로 바인딩하고, 클라이언트의 문자 인코딩이 UTF-8인 경우, *ColumnSize*의 값이 서버에서 데이터 형식의 크기와 정렬되는 경우에도 드라이버에서 "문자열 데이터의 오른쪽이 잘렸습니다"라는 오류를 받을 수 있습니다. 이 오류는 문자 인코딩 간 변환 시 데이터의 길이가 변경될 수 있기 때문에 발생합니다. 예를 들어 오른쪽 아포스트로피 문자(U+2019)는 CP-1252에서 1바이트 0x92로 인코딩되지만, UTF-8에서는 3바이트 시퀀스 0xe2 0x80 0x99로 인코딩됩니다.

예를 들어 사용하는 인코딩이 UTF-8인데 출력 매개 변수에 대해 *SQLBindParameter*의 *BufferLength* 및 **ColumnSize**에 모두 1을 지정한 다음, 서버에서 `char(1)` 열에 저장된 앞의 문자를 검색하려고(CP-1252를 사용하여) 시도하면 드라이버에서 해당 문자를 3바이트 UTF-8 인코딩으로 변환하지만 결과를 1바이트 버퍼에 맞출 수 없습니다. 반대 방향에서는 클라이언트 및 서버의 서로 다른 코드 페이지 간 변환을 수행하기 전에 *ColumnSize*를 *SQLBindParameter*의 **BufferLength**와 비교합니다. 예를 들어 *ColumnSize* 1은 *BufferLength* 3보다 작기 때문에 드라이버가 오류를 생성합니다. 이 오류를 방지하려면 변환 후의 길이가 지정된 버퍼 또는 열에 맞는지 확인합니다. *ColumnSize*는 `varchar(n)` 형식에 대해 8000보다 클 수 없습니다.

## <a name="troubleshooting-connection-problems"></a><a id="connectivity"></a> 연결 문제 해결  

ODBC 드라이버를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 수 없는 경우 다음 정보를 사용하여 문제를 확인합니다.  
  
가장 일반적인 연결 문제는 UnixODBC 드라이버 관리자의 복사본이 두 개 설치되는 것입니다. libodbc\*.so\*에 대해 /usr을 검색합니다. 둘 이상의 파일 버전이 표시되면 둘 이상의 드라이버 관리자가 설치된 것일 수 있습니다. 애플리케이션이 잘못된 버전을 사용할 수 있습니다.
  
`/etc/odbcinst.ini` 파일을 이러한 항목과 함께 다음 섹션이 포함되도록 편집하여 연결 로그를 사용하도록 설정합니다.

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
다른 연결 오류가 발생하고 로그 파일이 표시되지 않으면 컴퓨터에 드라이버 관리자의 복사본이 두 개 있을 수 있습니다. 그렇지 않으면 로그 출력은 다음과 같은 형태가 됩니다.  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
예를 들어 ASCII 문자 인코딩이 UTF-8이 아닌 경우 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
설치된 드라이버 관리자가 둘 이상이면 애플리케이션에서 잘못된 관리자를 사용 중이거나 드라이버 관리자가 올바르게 빌드되지 않은 것입니다.  
  
연결 오류를 해결하는 방법에 대한 자세한 내용은 다음을 참조하세요.  

- [SQL 연결 문제를 해결하는 단계](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [SQL Server 2005 연결 문제 해결 - 1부](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [연결 링 버퍼를 사용하여 SQL Server 2008의 연결 문제 해결](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [SQL Server 인증 문제 해결사](https://docs.microsoft.com/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>다음 단계

ODBC 드라이버 설치 지침은 다음 문서를 참조하세요.

- [Linux 기반 Microsoft ODBC Driver for SQL Server 설치](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [macOS 기반 Microsoft ODBC Driver for SQL Server 설치](install-microsoft-odbc-driver-sql-server-macos.md)

자세한 내용은 [프로그래밍 지침](programming-guidelines.md) 및 [릴리스 정보](release-notes-odbc-sql-server-linux-mac.md)를 참조하세요.  
