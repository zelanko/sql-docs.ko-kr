---
title: PostgreSQL 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ac871f330c84187a89f27d0bbc62f69d8f24bd93
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826331"
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>PostgreSQL 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)
이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **PostgreSQL** 데이터 원본에 연결하는 방법을 보여 줍니다. 

> [!IMPORTANT]
> PostgreSQL 데이터베이스에 연결하기 위한 자세한 요구 사항 및 필수 구성 요소는 이 Microsoft 문서에서 다루지 않습니다. 이 문서에서는 여러분의 컴퓨터에 PostgreSQL 클라이언트 소프트웨어가 설치되어 있고 대상 PostgreSQL 데이터베이스에 연결할 수 있다고 가정합니다. 자세한 내용은 PostgreSQL 데이터베이스 관리자에게 문의하거나 PostgreSQL 설명서를 참조하세요.

## <a name="get-the-postgresql-odbc-driver"></a>PostgreSQL ODBC 드라이버 받기

### <a name="install-the-odbc-driver-with-stack-builder"></a>스택 작성기로 ODBC 드라이버 설치
스택 작성기를 실행하여 설치된 PostgreSQL에 PostgreSQL ODBC 드라이버(psqlODBC)를 추가합니다.

![스택 작성기로 PostgreSQL ODBC 드라이버 설치](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>또는 최신 ODBC 드라이버 다운로드
또는 이 FTP 사이트([https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/))에서 직접 최신 버전의 PostgreSQL ODBC 드라이버(psqlODBC)에 대한 Windows Installer를 다운로드합니다. .zip 파일에서 파일을 추출하여 .msi 파일을 실행합니다.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>PostgreSQL ODBC 드라이버(psqlODBC)를 사용하여 PostgreSQL에 연결
ODBC 드라이버는 데이터 원본의 드롭다운 목록에 나열되지 않습니다. ODBC 드라이버를 연결하려면 먼저 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 데이터 원본으로 **.NET Framework Data Provider for ODBC**를 선택합니다. 이 공급자는 ODBC 드라이버 주위에서 래퍼 역할을 합니다.

다음은 .NET Framework Data Provider for ODBC를 선택하는 즉시 표시되는 제네릭 화면입니다.

![ODBC로 PostgreSQL에 연결 이전](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>지정 옵션(PostgreSQL ODBC 드라이버)

> [!NOTE]
> 이 데이터 공급자 및 ODBC 드라이버의 연결 옵션은 PostgreSQL이 원본이든 대상이든 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

PostgreSQL ODBC 드라이버를 사용하여 PostgreSQL에 연결하려면 다음 설정 및 값을 포함하는 연결 문자열을 조합합니다. 전체 연결 문자열의 형식은 설정 목록 바로 뒤에 옵니다.

> [!TIP]
> 도움을 받아 연결 문자열을 적절하게 조합합니다. 또는 연결 문자열을 제공하는 대신 기존 DSN(데이터 원본 이름)을 제공하거나 새 DSN을 만듭니다. 이러한 옵션에 대한 자세한 내용은 [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.

**드라이버**  
ODBC 드라이버의 이름 - **PostgreSQL ODBC 드라이버(유니코드)** 이거나 **PostgreSQL ODBC 드라이버(ANSI)** 입니다.

**Server**  
PostgreSQL 서버의 이름입니다. 

**포트**  
PostgreSQL 서버에 연결하는 데 사용할 포트입니다.

**데이터베이스 백업**  
PostgreSQL 데이터베이스의 이름입니다.

**Uid** 및 **Pwd**   
연결할 **Uid**(사용자 id) 및 **Pwd**(암호)입니다.

### <a name="connection-string-format"></a>연결 문자열 형식
다음은 일반적인 연결 문자열의 형식입니다. 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>연결 문자열 입력
**데이터 원본 선택** 또는 **대상 선택** 페이지에서 **ConnectionString** 필드에 연결 문자열을 입력하거나 **Dsn** 필드에 DSN 이름을 입력합니다. 연결 문자열을 입력하면 마법사에서 문자열을 구문 분석하고 개별 속성과 해당 값을 목록에 표시합니다.

다음 예제에서는 이 연결 문자열을 사용합니다.

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

다음은 연결 문자열을 입력한 후 표시되는 화면입니다.

![ODBC로 PostgreSQL에 연결](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 추가 정보
여기에 나열되지 않은 데이터 공급자를 사용하여 PostgreSQL에 연결하는 방법에 대한 자세한 내용은 [PostgreSQL 연결 문자열](https://www.connectionstrings.com/postgresql/)을 참조하세요. 또한 이러한 타사 사이트에는 이 페이지에서 설명하는 데이터 공급자 및 연결 매개 변수에 대한 자세한 정보가 포함되어 있습니다.

## <a name="see-also"></a>관련 항목:
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

