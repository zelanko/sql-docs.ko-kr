---
title: "(SQL Server 가져오기 및 내보내기 마법사)는 Oracle 데이터 원본에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e589e7f7a0262d258342bf887ec84c57d57dc978
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>(SQL Server 가져오기 및 내보내기 마법사)는 Oracle 데이터 원본에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **Oracle** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다. Oracle에 연결 하는 데 사용할 수 있는 여러 데이터 공급자가 있습니다.

> [!IMPORTANT]
> 자세한 요구 사항 및 Oracle 데이터베이스에 연결 하기 위한 필수 구성 요소는이 Microsoft 문서에서 다루지 않습니다. 이 문서에는 Oracle 클라이언트 소프트웨어가 설치 되어 있는 연결할 수 있는지 이미 성공적으로 대상 Oracle 데이터베이스로 가정 합니다. 자세한 내용은 Oracle 데이터베이스 관리자 또는 Oracle 설명서를 참조 하십시오.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Oracle에 연결 하는.net Framework Data Provider for Oracle
선택한 후 **.NET Framework Data Provider for Oracle** 에 **데이터 원본을 선택** 또는 **대상 선택** 마법사 페이지의 페이지 옵션은 공급자에 대 한 그룹화 된 목록을 제공 합니다. 이들 중 대부분은 이해 하기 어려운 이름 및 생소 한 설정입니다. 다행히 두 개 또는 세 가지 정보를 제공 하기만 하면 됩니다. 다른 설정에 대 한 기본값을 무시할 수 있습니다.

> [!NOTE]
> 이 데이터 공급자에 대 한 연결 옵션은 Oracle 소스 또는 대상 인지는 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

|필수 정보|.NET framework Data Provider for Oracle 속성|
|---|---|
|서버 이름|**데이터 원본**|
|인증 (로그인) 정보|**사용자 ID** 및 **암호**; 또는, **통합 보안**|

연결 문자열을 입력할 필요가 없습니다는 **ConnectionString** 필드 목록입니다. Oracle 서버 이름에 대 한 개별 값을 입력 한 후 (**데이터 소스**) 개별 속성 및 해당 값에서 연결 문자열을 조합 하는 로그인 정보, 마법사 및 합니다. 

![.NET 공급자와 Oracle에 연결](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Oracle 용 Microsoft ODBC 드라이버와 Oracle에 연결
ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. ODBC 드라이버를 연결 하려면 선택 하 여 시작 된 **.NET Framework Data Provider for ODBC** 데이터 원본으로 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 이 공급자는 ODBC 드라이버 주위에서 래퍼로 역할을 합니다.

다음은.NET Framework Data Provider for ODBC 선택한 후 볼 수 있는 제네릭 화면입니다.

![전에 ODBC 사용 하 여 Oracle에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>(ODBC Driver for Oracle)를 지정 하는 옵션

> [!NOTE]
> 이 데이터 공급자와 ODBC 드라이버에 대 한 연결 옵션 Oracle 소스 또는 대상 인지 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

Oracle에 대 한 ODBC 드라이버를 사용 하 여 Oracle에 연결 하려면 다음 설정 및 값을 포함 하는 연결 문자열을 조합 합니다. 전체 연결 문자열의 형식이 설정 목록 바로 뒤에.

> [!TIP]
> 가장 적합 하는 연결 문자열을 어셈블하여 도움말을 봅니다. 연결 문자열을 제공 하는 대신 기존의 DSN (데이터 원본 이름)를 제공 합니다. 아니면를 새로 만듭니다. 이러한 옵션에 대 한 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.

**드라이버**  
ODBC 드라이버의 이름 **Oracle 용 Microsoft ODBC**합니다.

**Server**  
Oracle 서버의 이름입니다. 

**Uid** 및 **Pwd**   
사용자 id와 암호를 연결 합니다.

### <a name="connection-string-format"></a>연결 문자열 형식
일반적인 연결 문자열의 형식은 다음과 같습니다.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>연결 문자열 입력
에 대 한 연결 문자열을 입력의 **ConnectionString** 에 DSN 이름을 입력 하거나 필드는 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 연결 문자열을 입력 한 후 마법사는 문자열을 구문 분석 하 고 목록에서 개별 속성 및 해당 값을 표시 합니다.

다음은 연결 문자열을 입력 한 후 표시 되는 화면입니다.

![ODBC 사용 하 여 Oracle에 연결](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>내 Oracle 서버 이름은 무엇입니까?
Oracle 서버 이름을 가져오려면 다음 쿼리 중 하나를 실행 합니다.

`SELECT host_name FROM v$instance`

또는

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 자세한 정보
여기에 나열 되어 있지 않은 데이터 공급자와 Oracle에 연결 하는 방법에 대 한 정보를 참조 하십시오. [Oracle 연결 문자열](https://www.connectionstrings.com/oracle/)합니다. 또한이 제 3 자 사이트 데이터 공급자 및 연결 매개 변수가이 페이지에서 설명 하는 방법에 대 한 자세한 정보를 포함 합니다.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


