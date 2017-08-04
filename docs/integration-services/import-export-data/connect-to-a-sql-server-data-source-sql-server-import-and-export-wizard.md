---
title: "SQL Server 데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17910c8e30dee98f39e977896fb67774b54a798d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>SQL Server 데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **Microsoft SQL Server** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다. SQL Server에 연결 하는 데 사용할 수 있는 여러 데이터 공급자가 있습니다.

> [!TIP]
> 여러 서버를 사용 하 여 네트워크를 사용 하는 경우 서버의 드롭 다운 목록을 확장 하는 것이 아니라 서버 이름을 입력 하기가 수도 있습니다. 드롭 다운 목록을 누르면 사용 가능한 모든 서버에 대 한 네트워크를 쿼리 하는 시간이 많이 걸릴 수 있습니다 및 결과 원하는 서버에도 포함 될 수 있습니다.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>.NET Framework Data Provider for SQL Server를 사용하여 SQL Server에 연결 
선택한 후 **.NET Framework Data Provider for SQL Server** 에 **데이터 원본을 선택** 또는 **대상 선택** 마법사 페이지의 페이지에는 그룹화 된 공급자에 대 한 옵션 목록이 표시 됩니다. 이들 중 대부분은 이해 하기 어려운 이름 및 생소 한 설정입니다. 다행히 엔터프라이즈 데이터베이스를 연결 하려면 일반적으로 해야 몇 가지 정보를 제공 합니다. 다른 설정에 대 한 기본값을 무시할 수 있습니다.

> [!NOTE]
> 이 데이터 공급자에 대 한 연결 옵션은 SQL Server 소스 또는 대상 인지는 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

|필수 정보|.NET framework Data Provider for SQL Server 속성|
|---|---|
|서버 이름|**데이터 원본**|
|인증 (로그인) 정보|**통합 보안**; 또는, **사용자 ID** 및 **암호**<br/>서버에서 데이터베이스의 드롭 다운 목록을 보려는 경우 먼저 유효한 로그인 정보를 제공 해야 합니다.|
|데이터베이스 이름|**초기 카탈로그**|

![.NET 공급자와 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>(.NET Framework Data Provider for SQL Server)를 지정 하는 옵션

> [!NOTE]
> 이 데이터 공급자에 대 한 연결 옵션은 SQL Server 소스 또는 대상 인지는 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

**데이터 원본**  
 이름 또는 원본 또는 대상 서버의 IP 주소를 입력 하십시오. 또는 드롭 다운 목록에서 서버를 선택 합니다.  
 
 비표준 TCP 포트를 지정 하려면 해당 서버 이름 또는 IP 주소를 후 쉼표를 입력 한 다음 포트 번호를 입력 합니다.
 
 **초기 카탈로그**  
 원본 또는 대상 데이터베이스의 이름을 입력 하거나 드롭다운 목록에서 데이터베이스를 선택 합니다.  
  
 **통합 보안**  
 지정 **True** (권장), Windows 통합된 인증을 사용 하 여 연결할 또는 **False** 와 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. **False**를 지정하면 사용자 ID와 암호를 입력해야 합니다. 기본값은 **False**입니다.  
  
 **사용자 ID**  
 사용 중인 경우 사용자 이름을 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.  
  
 **암호**  
 사용 하는 경우 암호를 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>SQL Server 용 ODBC 드라이버와 SQL Server에 연결 
ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. ODBC 드라이버를 연결 하려면 선택 하 여 시작 된 **.NET Framework Data Provider for ODBC** 데이터 원본으로 합니다. 이 공급자는 ODBC 드라이버 주위에서 래퍼로 역할을 합니다.

> [!TIP]
> **최신 드라이버**합니다. 다운로드는 [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)합니다.

다음은.NET Framework Data Provider for ODBC 선택한 후 볼 수 있는 제네릭 화면입니다.

![전에 odbc SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>(SQL Server 용 ODBC 드라이버)를 지정 하는 옵션

> [!NOTE]
> ODBC 드라이버에 대 한 연결 옵션을 SQL Server 소스 또는 대상 인지 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

다음 설정 및 값을 포함 하는 연결 문자열을 조합 하 최신 ODBC 드라이버와 SQL Server에 연결 합니다. 전체 연결 문자열의 형식이 설정 목록 바로 뒤에.

> [!TIP]
> 가장 적합 하는 연결 문자열을 어셈블하여 도움말을 봅니다. 연결 문자열을 제공 하는 대신 기존의 DSN (데이터 원본 이름)를 제공 합니다. 아니면를 새로 만듭니다. 이러한 옵션에 대 한 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.

**드라이버**  
ODBC 드라이버의 이름입니다. 이름이 서로 다른 버전의 드라이버에 대 한 차이가 있습니다.

**Server**  
SQL Server의 이름입니다.

**데이터베이스**  
데이터베이스의 이름입니다.  

**Trusted_Connection**; 또는, **Uid** 및 **Pwd**  
지정 **Trusted_Connection = Yes** Windows 통합된 인증을 사용 하 여 연결을 지정 하려면 **Uid** (사용자 id) 및 **Pwd** (암호)을 SQL Server 인증을 사용 하 여 연결 합니다.

### <a name="connection-string-format"></a>연결 문자열 형식
Windows 통합된 인증을 사용 하는 연결 문자열의 형식은 다음과 같습니다.

    Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;

Windows 통합된 인증 대신 SQL Server 인증을 사용 하는 연결 문자열의 형식은 다음과 같습니다.

     Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;

### <a name="enter-the-connection-string"></a>연결 문자열 입력
에 대 한 연결 문자열을 입력의 **ConnectionString** 에 DSN 이름을 입력 하거나 필드는 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 연결 문자열을 입력 한 후 마법사는 문자열을 구문 분석 하 고 목록에서 개별 속성 및 해당 값을 표시 합니다.

다음 예제에서는이 연결 문자열을 사용합니다.

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

다음은 연결 문자열을 입력 한 후 표시 되는 화면입니다.

![다음 odbc SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>SQL Server 또는 SQL Server Native Client에 대 한 Microsoft OLE DB 공급자와 함께 SQL Server에 연결

> [!IMPORTANT]
> SQL Server 2012 이후에 Microsoft OLE DB Provider for SQL Server 및 SQL Server Native Client 버전의 SQL Server에서 지원 되지 않습니다. ODBC 드라이버를 대신 사용 합니다. ODBC 드라이버에 대 한 전환에 대 한 자세한 내용은 다음 블로그 게시물을 참조 하십시오.
>   -   [Microsoft의 ODBC 지원 고유 관계형 데이터 액세스에 대 한](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [새 Microsoft ODBC Driver for SQL Server 소개](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 자세한 정보
여기에 나열 되어 있지 않은 데이터 공급자와 SQL Server에 연결 하는 방법에 대 한 정보를 참조 하십시오. [SQL Server 연결 문자열](https://www.connectionstrings.com/sql-server/)합니다. 또한이 제 3 자 사이트 데이터 공급자 및 연결 매개 변수가이 페이지에서 설명 하는 방법에 대 한 자세한 정보를 포함 합니다.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


