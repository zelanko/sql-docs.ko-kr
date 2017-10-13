---
title: "(SQL Server 가져오기 및 내보내기 마법사) PostgreSQL 데이터 원본에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c82ae7eedc3e18e7591cf7ab30a507920695247
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>(SQL Server 가져오기 및 내보내기 마법사) PostgreSQL 데이터 원본에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **PostgreSQL** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다. 

> [!IMPORTANT]
> 자세한 요구 사항 및 PostgreSQL 데이터베이스에 연결 하기 위한 필수 구성 요소는이 Microsoft 문서에서 다루지 않습니다. 이 문서에서는 이미 PostgreSQL 클라이언트 소프트웨어가 설치 되어 있고 연결할 수 있는지 이미 성공적으로 대상 PostgreSQL 데이터베이스에 가정 합니다. 자세한 내용은 PostgreSQL 데이터베이스 관리자 또는 PostgreSQL 설명서를 참조 하십시오.

## <a name="get-the-postgresql-odbc-driver"></a>PostgreSQL ODBC 드라이버

### <a name="install-the-odbc-driver-with-stack-builder"></a>스택 작성기로 ODBC 드라이버를 설치 합니다.
스택 PostgreSQL ODBC 드라이버 (psqlODBC) PostgreSQL의 설치를 추가 하는 작성기를 실행 합니다.

![PostgreSQL ODBC 스택 작성기와 함께 설치](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>또는 최신 ODBC 드라이버를 다운로드 합니다.
이 FTP 사이트-에서 직접 PostgreSQL ODBC 드라이버 (psqlODBC)의 최신 버전은 Windows 설치 관리자 다운로드 또는 [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/)합니다. .Zip 파일에서 파일을 추출 하 고.msi 파일을 실행 합니다.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>PostgreSQL ODBC 드라이버 (psqlODBC) PostgreSQL에 연결
ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. ODBC 드라이버를 연결 하려면 선택 하 여 시작 된 **.NET Framework Data Provider for ODBC** 데이터 원본으로 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 이 공급자는 ODBC 드라이버 주위에서 래퍼로 역할을 합니다.

다음은.NET Framework Data Provider for ODBC 선택한 후 볼 수 있는 제네릭 화면입니다.

![PostgreSQL 전에 odbc 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>(PostgreSQL ODBC 드라이버)를 지정 하는 옵션

> [!NOTE]
> 이 데이터 공급자와 ODBC 드라이버에 대 한 연결 옵션 PostgreSQL 소스 또는 대상 인지 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

PostgreSQL PostgreSQL ODBC 드라이버와 연결할 다음 설정 및 값을 포함 하는 연결 문자열을 조합 합니다. 전체 연결 문자열의 형식이 설정 목록 바로 뒤에.

> [!TIP]
> 가장 적합 하는 연결 문자열을 어셈블하여 도움말을 봅니다. 연결 문자열을 제공 하는 대신 기존의 DSN (데이터 원본 이름)를 제공 합니다. 아니면를 새로 만듭니다. 이러한 옵션에 대 한 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.

**드라이버**  
ODBC 드라이버의-하거나 이름 **PostgreSQL ODBC Driver(UNICODE)** 또는 **PostgreSQL ODBC Driver(ANSI)**합니다.

**Server**  
PostgreSQL 서버의 이름입니다. 

**포트**  
PostgreSQL 서버에 연결 하는 데 사용할 포트입니다.

**데이터베이스**  
PostgreSQL 데이터베이스의 이름입니다.

**Uid** 및 **Pwd**   
**Uid** (사용자 id) 및 **Pwd** 연결할 (암호).

### <a name="connection-string-format"></a>연결 문자열 형식
일반적인 연결 문자열의 형식은 다음과 같습니다. 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>연결 문자열 입력
에 대 한 연결 문자열을 입력의 **ConnectionString** 에 DSN 이름을 입력 하거나 필드는 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 연결 문자열을 입력 한 후 마법사는 문자열을 구문 분석 하 고 목록에서 개별 속성 및 해당 값을 표시 합니다.

다음 예제에서는이 연결 문자열을 사용합니다.

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

다음은 연결 문자열을 입력 한 후 표시 되는 화면입니다.

![ODBC와 PostgreSQL에 연결](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 자세한 정보
PostgreSQL 여기에 나열 되어 있지 않은 데이터 공급자와 연결 하는 방법에 대 한 정보를 참조 하십시오. [PostgreSQL 연결 문자열](https://www.connectionstrings.com/postgresql/)합니다. 또한이 제 3 자 사이트 데이터 공급자 및 연결 매개 변수가이 페이지에서 설명 하는 방법에 대 한 자세한 정보를 포함 합니다.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


