---
title: 프로그래밍 지침 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5030124775a8016fe5ddb716524276365aa47be7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613088"
---
# <a name="programming-guidelines"></a>프로그래밍 지침

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 및 Linux 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 프로그래밍 기능은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client([SQL Server Native Client(ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151))를 기반으로 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 Windows Data Access Components의 ODBC를 기반으로 합니다([ODBC 프로그래머 참조](http://go.microsoft.com/fwlink/?LinkID=45250)).  

ODBC를 사용 하 고 여러 활성 결과 집합 (MARS) 및 기타 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 포함 하 여 특정 기능 `/usr/local/include/msodbcsql.h` unixODBC 헤더를 포함 한 후 (`sql.h`를 `sqlext.h`를 `sqltypes.h`, 및 `sqlucode.h`). 그런 다음, Windows ODBC 응용 프로그램에서 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관련 항목에 대해 동일한 기호화된 이름을 사용합니다.

## <a name="available-features"></a>사용 가능한 기능  
ODBC([SQL Server Native Client(ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151))에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 설명서의 다음 섹션은 macOS 및 Linux 기반 ODBC 드라이버를 사용할 때 유용합니다.  

-   [SQL Server와 통신(ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [연결 및 쿼리 시간 제한 지원](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [커서](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [날짜/시간 기능 향상(ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [쿼리 실행(ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [오류 및 메시지 처리](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Kerberos 인증](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [큰 CLR 사용자 정의 형식(ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [트랜잭션 수행(ODBC)(분산 트랜잭션 제외)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [결과 처리(ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [저장 프로시저 실행](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [스파스 열 지원(ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 암호화](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [테이블 반환 매개 변수](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [명령 및 데이터 API용 UTF-8 및 UTF-16](http://msdn.microsoft.com/library/ff878241.aspx)
-   [카탈로그 함수 사용](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>지원되지 않는 기능

MacOS 및 Linux에서 ODBC 드라이버의이 릴리스에서 제대로 작동 하려면 다음과 같은 기능이 확인 되지 않은 합니다.

-   장애 조치 클러스터 연결
-   [투명 네트워크 IP 확인](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (이전 ODBC 드라이버 17)
-   [고급 드라이버 추적](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

다음 기능은 이 macOS 및 Linux 기반 ODBC 드라이버 릴리스에서 사용할 수 없습니다. 

-   분산 트랜잭션(SQL_ATTR_ENLIST_IN_DTC 특성이 지원되지 않음)  
-   데이터베이스 미러링  
-   FILESTREAM  
-   [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099)에 설명된 ODBC 드라이버 성능 프로파일링 및 성능과 관련된 연결 특성은 다음과 같습니다.  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   SQL_C_INTERVAL_YEAR_TO_MONTH와 같은 C 간격 유형([데이터 형식 식별자 및 설명자](http://msdn.microsoft.com/library/ms716351(VS.85).aspx)에 설명됨)
-   SQLSetConnectAttr 함수의 SQL_ATTR_ODBC_CURSORS 특성에 대한 SQL_CUR_USE_ODBC 값입니다.

## <a name="character-set-support"></a>문자 집합 지원

ODBC Driver 13 및 13.1 SQLCHAR 데이터는 u t F-8 이어야 합니다. 없는 다른 인코딩이 지원 됩니다.

ODBC 드라이버 17에 대 한 SQLCHAR 데이터 문자 집합/인코딩 중 하나를 사용할 수 있습니다.

|속성|설명|
|-|-|
|UTF-8|유니코드|
|CP437|MS-DOS 라틴어 미국|
|CP850|MS-DOS 라틴어 1|
|CP874|라틴 문자/태국어|
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
|ISO-8859-5|라틴 문자/키릴자모|
|ISO-8859-6|라틴 문자/아랍어|
|ISO-8859-7|라틴 문자/그리스어|
|ISO-8859-8 / CP1255|히브리어|
|ISO-8859-9 / CP1254|터키어|
|ISO-8859-13|라틴어-7|
|ISO-8859-15|라틴어 9|

연결 시 드라이버에서 로드 된 프로세스의 현재 로캘을 검색 합니다. 드라이버는 SQLCHAR (좁은 문자) 데이터에 대 한 해당 인코딩을 사용 위의 인코딩 중 하나를 사용 하는 경우 그렇지 않으면 u t F-8로 기본값은입니다. 모든 프로세스 기본적으로 "C" 로캘에서 시작 (및 따라서 기본값으로 드라이버 u t F-8로 인해) 이후 응용 프로그램을 위의 인코딩 중 하나를 사용 해야 하는 경우 사용 해야 합니다 **setlocale** 전에 적절 하 게 로캘을 설정 하는 함수 연결; 예를 빈 문자열을 사용 하 여 또는 원하는 로캘을 명시적으로 지정 하거나 `setlocale(LC_ALL, "")` 환경의 로캘 설정을 사용 하도록 합니다.

따라서는 일반적인 Linux 또는 Mac 환경에서 인코딩 u t F-8, 13 또는 13.1에서 ODBC 드라이버 17. 업그레이드 하는 사용자가 차이 관찰할 됩니다. 그러나 응용 프로그램 사용 하는 비-u t F-8 인코딩을 통해 위 목록에서 `setlocale()` u t F-8 대신 드라이버에서 데이터를 해당 인코딩을 사용 해야 합니다.

SQLWCHAR 데이터는 UTF-16LE(Little Endian)이어야 합니다.

드라이버를 기본값 (일반적으로 코드 페이지 1252) 인코딩 클라이언트에서 제공 된 데이터를 변환을 SQL_VARCHAR 지정 같은 반각 문자 SQL 형식이 SQLBindParameter에서를 사용 하 여 입력된 매개 변수를 바인딩하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인코딩. 출력 매개 변수의 경우 드라이버는 인코딩 클라이언트 데이터와 연결 된 데이터 정렬 정보에 지정 된 인코딩은에서 변환 합니다. 그러나 데이터 손실은---대상 인코딩 형식으로 표현할 수 없습니다 원본 인코딩으로 문자는 물음표로 변환 됩니다 ('? ').

입력된 매개 변수를 바인딩하는 경우이 데이터 손실을 방지 하려면 유니코드 SQL 문자 형식 SQL_NVARCHAR 등을 지정 합니다. 이 경우 드라이버는 인코딩을 u t F-16이 고 모든 유니코드 문자를 나타낼 수 있는 클라이언트에서 변환 합니다. 또한 대상 열 또는 매개 변수는 서버의 수도 있어야 유니코드 형식 (**nchar**, **nvarchar**하십시오 **ntext**) 인코딩을 사용 하 여 데이터 정렬/을 수 있는 하나 또는 원본 데이터의 모든 문자를 나타냅니다. 출력 매개 변수를 사용 하 여 데이터 손실 방지, 유니코드 SQL 유형과 유니코드 C 형식 (SQL_C_WCHAR), u t F-16으로 데이터를 반환 하는 드라이버를 일으키는 지정 또는 좁은 C를 입력 하 고 인코딩을 클라이언트 (이 경우 항상 u t F-8을 사용 하 여 가능한) 원본 데이터의 모든 문자를 나타낼 수 확인

데이터 정렬 및 인코딩에 대한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.

가지 Windows 및 Linux 및 macOS iconv 라이브러리의 여러 버전 간의 몇 가지 인코딩 변환 차이점이 있습니다. 텍스트 데이터를 코드 페이지 1255 (히브리어)를 유니코드로 변환 하면 다르게 동작 하는 하나의 코드 포인트 (0xca)가 합니다. Windows,이 문자 변환 하면 0x05BA의 utf-16 코드 포인트입니다. MacOS 및 Linux libiconv 버전 1.15 이전의 변환 하면 0x00CA 합니다. Big5/CP950의 2003 버전을 지원 하지 않는 iconv 라이브러리를 사용 하 여 Linux에서 (라는 `BIG5-2003`), 해당 수정 버전을 사용 하 여 추가 문자는 올바르게 변환 하지 않습니다. 코드 페이지 932 (일본어, Shift JIS), 원래 인코딩 표준에 정의 된 문자 디코딩 결과일 수도 다릅니다. 예를 들어, 0x80 바이트 Windows에서 u+0080 변환 하지만 Linux iconv 버전에 따라 macOS에서 U + 30FB 될 수 있습니다.

ODBC 드라이버 13 및 13.1에서 UTF-8 멀티바이트 문자 또는 UTF-16 서로게이트가 SQLPutData 버퍼로 분할되면 데이터 손상이 발생합니다. 버퍼를 부분 문자 인코딩으로 끝나지 않는 SQLPutData 스트리밍에 사용합니다. ODBC 드라이버 17을 사용 하 여이 제한이 제거 되었습니다.

## <a name="additional-notes"></a>참고 사항  

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 및 **호스트,포트**를 사용하여 DAC(관리자 전용 연결)를 만들 수 있습니다. Sysadmin 역할의 멤버는 먼저 DAC 포트를 검색해야 합니다. 참조 [데이터베이스 관리자를 위한 진단 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) 를 검색 하는 방법입니다. 예를 들어 DAC 포트가 33000인 경우 다음과 같이 `sqlcmd`로 연결할 수 있습니다.  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 연결은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용해야 합니다.  
    
2.  UnixODBC 드라이버 관리자는 문 특성이 SQLSetConnectAttr을 통해 전달될 때 모든 문 특성에 대해 "잘못된 특성/옵션 식별자"를 반환합니다. Windows에서 SQLSetConnectAttr이 명령문 특성 값을 받을 때 드라이버가 연결 핸들의 자식인 모든 활성 명령문의 해당 값을 설정합니다.  

## <a name="see-also"></a>참고 항목  
[질문과 대답](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[이 버전의 드라이버에서 알려진 문제](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)
