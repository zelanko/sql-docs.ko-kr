---
title: "프로그래밍 지침 | Microsoft Docs"
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
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 50f9efe65f14dbd73ccbc3c6e81307c3893c469f
ms.openlocfilehash: 85ba8b35fa698769bd390837855729f3edbc7291
ms.contentlocale: ko-kr
ms.lasthandoff: 11/08/2017

---
# <a name="programming-guidelines"></a>프로그래밍 지침

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

프로그래밍 기능은 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 및에 대 한 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] macOS 및 Linux 기반으로 ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client Windows Data Access Components의 ODBC 기반 ([ODBC Programmer's Reference](http://go.microsoft.com/fwlink/?LinkID=45250)).  

결과 집합 MARS (Multiple Active) 오류 코드 및 기타 ODBC 응용 프로그램이 사용할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 포함 하 여 특정 기능 `/usr/local/include/msodbcsql.h` unixODBC 헤더를 포함 한 후 (`sql.h`, `sqlext.h`, `sqltypes.h`, 및 `sqlucode.h`). 다음에 대해 동일한 기호화 된 이름을 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-Windows ODBC 응용 프로그램에서 사용 하는 특정 항목입니다.  

## <a name="available-features"></a>사용 가능한 기능  
다음 섹션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ODBC 설명서 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) macOS 및 Linux에서 ODBC 드라이버를 사용할 때은 유효 합니다.  

-   [SQL Server (ODBC)와 통신](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [연결 및 쿼리 시간 제한 지원](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [커서](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [날짜/시간 기능 향상 (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [쿼리 실행 (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [오류 및 메시지 처리](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos 인증](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [큰 CLR 사용자 정의 형식 (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [트랜잭션 수행 (ODBC) (분산된 트랜잭션 제외)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [결과 처리 (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [저장된 프로시저 실행](http://msdn.microsoft.com/library/ms131440.aspx)
-   [스파스 열 지원 (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 암호화](http://msdn.microsoft.com/library/ms131691.aspx)
-   [테이블 반환된 매개 변수](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [U t F-8과 u t F-16 명령 및 데이터 API에 대 한](http://msdn.microsoft.com/library/ff878241.aspx)
-   [카탈로그 함수를 사용 하 여](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>지원되지 않는 기능

MacOS 및 Linux에서 ODBC 드라이버의이 릴리스에서 제대로 작동 하려면 다음과 같은 기능 확인 되지 않은:

-   장애 조치 클러스터 연결
-   [투명 네트워크 IP 확인](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)
-   [고급 드라이버 추적](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

다음 기능은이 릴리스의 macOS 및 Linux 기반 ODBC 드라이버에서 사용할 수 없습니다. 

-   분산 트랜잭션 (SQL_ATTR_ENLIST_IN_DTC 특성이 지원 되지 않습니다.)  
-   데이터베이스 미러링  
-   FILESTREAM  
-   에 설명 된 ODBC 드라이버 성능 프로 파일링, [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099), 및 다음과 같은 성능 관련 연결 특성:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   SQL_C_INTERVAL_YEAR_TO_MONTH와 같은 C 간격 유형 (에 문서화 되어 [데이터 형식 식별자 및 설명자](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   SQLSetConnectAttr 함수의 SQL_ATTR_ODBC_CURSORS 특성의 SQL_CUR_USE_ODBC 값입니다.

## <a name="character-set-support"></a>문자 집합 지원

인코딩 클라이언트는 다음 중 하나일 수 있습니다.
  -  UTF-8
  -  ISO 8859-1
  -  ISO 8859-2
  -  ISO 8859-3
  -  ISO 8859-4
  -  ISO-8859-5
  -  ISO 8859-6
  -  ISO 8859-7
  -  ISO-8859-8
  -  ISO-8859-9
  -  ISO 8859-13
  -  -8859-15
  
SQLCHAR 데이터는 지원 되는 문자 집합 중 하나 여야 합니다. SQLWCHAR 데이터는 UTF-16LE(Little Endian)이어야 합니다.  

SQLDescribeParameter가 서버에서 SQL 형식을 지정하지 않는 경우 드라이버에서는 SQLBindParameter의 *ParameterType* 매개 변수에 지정된 SQL 형식을 사용합니다. SQL_VARCHAR 같은 반각 문자 SQL 형식이 SQLBindParameter에서 지정 된, 드라이버 변환 제공 된 데이터를 클라이언트 코드 페이지에서 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 코드 페이지입니다. (기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 코드 페이지는 보통 1252입니다.) 클라이언트 코드 페이지 지원 되지 않는 경우 u t F-8로 설정 됩니다. 이 경우 드라이버는 다음의 기본 코드 페이지에 u t F-8 데이터를 변환합니다. 그러나 데이터 손실이 발생할 수 있습니다. 코드 페이지 1252가 문자를 나타낼 수 없는 경우 드라이버에서 해당 문자를 물음표('?')로 변환합니다. 이 데이터 손실을 방지하려면 SQLBindParameter에서 유니코드 SQL 문자 형식(예: SQL_NVARCHAR)을 지정합니다. 이 경우 드라이버는 데이터의 손실 없이 u t F-16 인코딩을 u t F-8에서 제공 된 유니코드 데이터를 변환 합니다.

Windows와 Linux와 macOS iconv 라이브러리의 여러 버전 간에 텍스트 인코딩 변환 차이가 있습니다. 코드 페이지 1255 (히브리어)으로 인코딩된 텍스트 데이터 변환 시 다르게 동작 하는 하나의 코드 포인트 (0xCA)에 있습니다. 이 문자 Windows에서 유니코드로 변환 0x05BA의 utf-16 코드 포인트를 생성 합니다. Libiconv 버전과 macOS 및 Linux에서 유니코드로 변환 1.15 이전의 생성 0x00CA의 utf-16 코드 포인트입니다.

UTF-8 멀티바이트 문자 또는 UTF-16 서로게이트가 SQLPutData 버퍼에서 분할될 때 데이터 손상이 발생합니다. 버퍼를 부분 문자 인코딩으로 끝나지 않는 SQLPutData 스트리밍에 사용합니다.  

## <a name="additional-notes"></a>추가 참고 사항  

1.  관리자 전용된 연결 (DAC)을 만들 수 있습니다를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인증 및 **호스트, 포트**합니다. Sysadmin 역할의 멤버는 먼저 DAC 포트를 검색해야 합니다. 참조 [데이터베이스 관리자를 위한 진단 연결](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) 검색 방법입니다. 예를 들어 DAC 포트가 33000를 하는 경우 연결할 수 있습니다를 사용 하 여 `sqlcmd` 다음과 같습니다.  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 연결 사용 해야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인증 합니다.  
    
2.  UnixODBC 드라이버 관리자는 문 특성이 SQLSetConnectAttr을 통해 전달될 때 모든 문 특성에 대해 "잘못된 특성/옵션 식별자"를 반환합니다. Windows에서 SQLSetConnectAttr 문 특성 값을 받는 드라이버에는 연결 핸들의 자식인 모든 활성 문의 해당 값을 설정 하려면 하면 합니다.  

## <a name="see-also"></a>관련 항목:  
[질문과 대답](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)

