---
title: 프로그래밍 지침(SQL Server용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/12/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 45d1fc9d06dd814e4ee6d80ec5ecbbe9e58d09c3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798744"
---
# <a name="programming-guidelines"></a>프로그래밍 지침

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 및 Linux 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 프로그래밍 기능은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client([SQL Server Native Client(ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151))를 기반으로 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 Windows Data Access Components의 ODBC를 기반으로 합니다([ODBC 프로그래머 참조](https://go.microsoft.com/fwlink/?LinkID=45250)).  

ODBC 애플리케이션은 unixODBC 헤더(`sql.h`, `sqlext.h`, `sqltypes.h` 및 `sqlucode.h`)를 포함한 후 `/usr/local/include/msodbcsql.h`를 포함하여 MARS(Multiple Active Result Set) 및 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고유 기능을 사용할 수 있습니다. 그런 다음, Windows ODBC 애플리케이션에서 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관련 항목에 대해 동일한 기호화된 이름을 사용합니다.

## <a name="available-features"></a>사용 가능한 기능  
ODBC([SQL Server Native Client(ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151))에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 설명서의 다음 섹션은 macOS 및 Linux 기반 ODBC 드라이버를 사용할 때 유용합니다.  

-   [SQL Server와 통신(ODBC)](https://msdn.microsoft.com/library/ms131692.aspx)  
-   [연결 및 쿼리 시간 제한 지원](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [커서](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [날짜/시간 기능 향상(ODBC)](https://msdn.microsoft.com/library/bb677319.aspx)  
-   [쿼리 실행(ODBC)](https://msdn.microsoft.com/library/ms131677.aspx)  
-   [오류 및 메시지 처리](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Kerberos 인증](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [큰 CLR 사용자 정의 형식(ODBC)](https://msdn.microsoft.com/library/bb677316.aspx)  
-   [트랜잭션 수행(ODBC)(분산 트랜잭션 제외)](https://msdn.microsoft.com/library/ms131706.aspx)  
-   [결과 처리(ODBC)](https://msdn.microsoft.com/library/ms130812.aspx)  
-   [저장 프로시저 실행](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [스파스 열 지원(ODBC)](https://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 암호화](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [테이블 반환 매개 변수](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [명령 및 데이터 API용 UTF-8 및 UTF-16](https://msdn.microsoft.com/library/ff878241.aspx)
-   [카탈로그 함수 사용](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>지원되지 않는 기능

다음 기능은 이 macOS 및 Linux 기반 ODBC 드라이버 릴리스에서 올바르게 작동하는 것으로 확인되지 않았습니다.

-   장애 조치(failover) 클러스터 연결
-   [투명한 네트워크 IP 확인](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution)(ODBC 드라이버 17 이전)
-   [고급 드라이버 추적](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

다음 기능은 이 macOS 및 Linux 기반 ODBC 드라이버 릴리스에서 사용할 수 없습니다. 

-   분산 트랜잭션(SQL_ATTR_ENLIST_IN_DTC 특성이 지원되지 않음)  
-   데이터베이스 미러링  
-   FILESTREAM  
-   [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=234099)에 설명된 ODBC 드라이버 성능 프로파일링 및 성능과 관련된 연결 특성은 다음과 같습니다.  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   SQL_C_INTERVAL_YEAR_TO_MONTH와 같은 C 간격 유형([데이터 형식 식별자 및 설명자](https://msdn.microsoft.com/library/ms716351(VS.85).aspx)에 설명됨)
-   SQLSetConnectAttr 함수의 SQL_ATTR_ODBC_CURSORS 특성에 대한 SQL_CUR_USE_ODBC 값입니다.

## <a name="character-set-support"></a>문자 집합 지원

ODBC 드라이버 13 및 13.1의 경우 SQLCHAR 데이터는 UTF-8이어야 합니다. 다른 인코딩은 지원되지 않습니다.

ODBC 드라이버 17의 경우 다음 문자 세트/인코딩 중 하나의 SQLCHAR 데이터가 지원됩니다.

|속성|설명|
|-|-|
|UTF-8|유니코드|
|CP437|MS-DOS 라틴어 미국|
|CP850|MS-DOS 라틴어 1|
|CP874|라틴어/태국어|
|CP932|일본어, Shift_JIS|
|CP936|중국어 간체, GBK|
|CP949|한국어, EUC-KR|
|CP950|중국어 번체, Big5|
|CP1251|키릴 자모|
|CP1253|그리스어|
|CP1256|아랍어|
|CP1257|발트어|
|CP1258|베트남어|
|ISO-8859-1 / CP1252|라틴어-1|
|ISO-8859-2 / CP1250|라틴어-2|
|ISO-8859-3|라틴어-3|
|ISO-8859-4|라틴어-4|
|ISO-8859-5|라틴어/키릴 자모|
|ISO-8859-6|라틴어/아랍어|
|ISO-8859-7|라틴어/그리스어|
|ISO-8859-8 / CP1255|히브리어|
|ISO-8859-9 / CP1254|터키어|
|ISO-8859-13|라틴어-7|
|ISO-8859-15|라틴어-9|

연결 시 드라이버에서 로드된 프로세스의 현재 로캘을 검색합니다. 위의 인코딩 중 하나를 사용하는 경우 드라이버에서 SQLCHAR(반각 문자) 데이터에 해당 인코딩을 사용하며, 그렇지 않으면 기본적으로 UTF-8을 사용합니다. 모든 프로세스는 기본적으로 “C” 로캘로 시작하므로(그리고 따라서 드라이버에서 기본적으로 UTF-8을 사용하므로), 애플리케이션이 위의 인코딩 중 하나를 사용해야 하는 경우 연결하기 전에 원하는 로캘을 명시적으로 지정하거나 빈 문자열(예: `setlocale(LC_ALL, "")`)을 사용해 환경의 로캘 설정을 사용함으로써 **setlocale** 함수를 사용하여 로캘을 적합하게 설정해야 합니다.

그러므로 인코딩이 UTF-8인 일반적인 Linux 또는 Mac 환경에서 ODBC 드라이버 13 또는 13.1에서 17로 업그레이드하는 사용자의 경우 해당 차이점이 발생하지 않습니다. 그러나 `setlocale()`을 통해 위 목록의 UTF-8이 아닌 인코딩을 사용하는 애플리케이션은 드라이버에 대한 데이터에 UTF-8 대신 해당 인코딩을 사용해야 합니다.

SQLWCHAR 데이터는 UTF-16LE(Little Endian)이어야 합니다.

SQLBindParameter를 사용하여 입력 매개 변수를 바인딩하는 경우 SQL_VARCHAR와 같은 반각 문자 SQL 형식을 지정하면 드라이버에서 제공된 데이터를 클라이언트 인코딩에서 기본(일반적으로 코드 페이지 1252) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인코딩으로 변환합니다. 출력 매개 변수의 경우 드라이버에서 데이터와 연결된 정렬 정보에 지정된 인코딩에서 클라이언트 인코딩으로 변환합니다. 그러나 데이터 손실이 발생할 수 있습니다. --- 즉, 대상 인코딩에서 표현할 수 없는 원본 인코딩의 문자가 물음표('?')로 변환될 수 있습니다.

입력 매개 변수를 바인딩할 때 이 데이터 손실을 방지하려면 유니코드 SQL 문자 형식(예: SQL_NVARCHAR)을 지정합니다. 이 경우 드라이버는 클라이언트 인코딩에서 모든 유니코드 문자를 표현할 수 있는 UTF-16으로 변환합니다. 또한 서버의 대상 열 또는 매개 변수도 유니코드 형식(**nchar**, **nvarchar**, **ntext**) 또는 원래 원본 데이터의 모든 문자를 표현할 수 있는 정렬/인코딩을 포함하는 형식이어야 합니다. 출력 매개 변수에서 데이터 손실을 방지하려면 유니코드 SQL 형식 및 드라이버에서 데이터를 UTF-16으로 변환하게 하는 유니코드 C 형식(SQL_C_WCHAR) 또는 반각 C 형식을 지정하고 클라이언트 인코딩이 원본 데이터의 모든 문자를 표현할 수 있는지(UTF-8에서는 항상 가능) 확인합니다.

데이터 정렬 및 인코딩에 대한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.

Windows와 Linux 및 macOS 기반 iconv 라이브러의 여러 버전 간에는 인코딩 변환에서 몇 가지 차이점이 있습니다. 코드 페이지 1255(히브리어)의 텍스트 데이터에는 유니코드로 변환하면 다르게 동작하는 하나의 코드 포인트(0xCA)가 있습니다. Windows의 경우 이 문자는 UTF-16 코드 포인트 0x05BA로 변환됩니다. 1.15 이전 버전 libiconv를 포함하는 macOS 및 Linux의 경우 0x00CA로 변환됩니다. 2003 개정판 Big5/CP950(`BIG5-2003`)을 지원하지 않는 iconv 라이브러리를 포함하는 Linux의 경우 해당 개정판에서 추가된 문자는 올바르게 변환되지 않습니다. 코드 페이지 932(일본어, Shift-JIS)의 경우 원래 인코딩 표준에 정의되지 않은 문자를 해독한 결과도 다릅니다. 예를 들어 바이트 0x80은 Windows에서 U+0080으로 변환되지만 Linux 및 macOS에서는 iconv 버전에 따라 U+30FB가 될 수 있습니다.

ODBC 드라이버 13 및 13.1에서 UTF-8 멀티바이트 문자 또는 UTF-16 서로게이트가 SQLPutData 버퍼로 분할되면 데이터 손상이 발생합니다. 버퍼를 부분 문자 인코딩으로 끝나지 않는 SQLPutData 스트리밍에 사용합니다. 이 제한 사항은 ODBC 드라이버 17에서 제거되었습니다.

## <a name="additional-notes"></a>참고 사항  

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 및 **호스트,포트**를 사용하여 DAC(관리자 전용 연결)를 만들 수 있습니다. Sysadmin 역할의 멤버는 먼저 DAC 포트를 검색해야 합니다. 방법에 대해 알아보려면 [데이터베이스 관리자용 진단 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)을 참조하세요. 예를 들어 DAC 포트가 33000인 경우 다음과 같이 `sqlcmd`로 연결할 수 있습니다.  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 연결은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용해야 합니다.  
    
2.  UnixODBC 드라이버 관리자는 문 특성이 SQLSetConnectAttr을 통해 전달될 때 모든 문 특성에 대해 "잘못된 특성/옵션 식별자"를 반환합니다. Windows에서 SQLSetConnectAttr이 명령문 특성 값을 받을 때 드라이버가 연결 핸들의 자식인 모든 활성 명령문의 해당 값을 설정합니다.  

## <a name="see-also"></a>참고 항목  
[질문과 대답](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
