---
title: SQL Server 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft 문서 도구
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a9d83d068e85a310dca4736f6514f235f23b6ce9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114652"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>SQL Server 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **Microsoft SQL Server** 데이터 원본에 연결하는 방법을 보여 줍니다. SQL Server에 연결하는 데 사용할 수 있는 여러 데이터 공급자가 있습니다.

> [!TIP]
> 여러 서버가 있는 네트워크를 사용하는 경우 서버의 드롭다운 목록을 확장하는 대신 서버 이름을 입력하는 것이 더 쉽습니다. 드롭다운 목록을 클릭하면 사용 가능한 모든 서버를 네트워크에 쿼리하는 데 많은 시간이 걸릴 수 있으며, 원하는 서버가 결과에 포함되지 않을 수도 있습니다.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>.NET Framework Data Provider for SQL Server를 사용하여 SQL Server에 연결 
마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **.NET Framework Data Provider for SQL Server**를 선택하는 경우 페이지에는 공급자에 대해 그룹화된 옵션 목록이 표시됩니다. 이러한 옵션 중 대부분은 이해하기 어려운 이름이거나 생소한 설정입니다. 다행히도 엔터프라이즈 데이터베이스에 연결하려면 일반적으로 몇 가지 정보만 제공해야 합니다. 다른 설정의 기본값을 무시할 수 있습니다.

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 SQL Server가 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

|필수 정보|.NET Framework Data Provider for SQL Server 속성|
|---|---|
|서버 이름|**데이터 원본**|
|인증(로그인) 정보|**통합 보안** 또는 **사용자 ID**/**암호**<br/>서버에 있는 데이터베이스의 드롭다운 목록을 보려면 먼저 유효한 로그인 정보를 제공해야 합니다.|
|데이터베이스 이름|**초기 카탈로그**|

![.NET 공급자를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>지정할 옵션(.NET Framework Data Provider for SQL Server)

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 SQL Server가 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

**데이터 원본**  
 원본 또는 대상 서버의 이름이나 IP 주소를 입력하거나 드롭다운 목록에서 서버를 선택합니다.  
 
 표준이 아닌 TCP 포트를 지정하려면 해당 서버 이름 또는 IP 주소 뒤에 쉼표를 입력한 다음 포트 번호를 입력합니다.
 
 **초기 카탈로그**  
 원본 또는 대상 데이터베이스의 이름을 입력하거나 드롭다운 목록에서 데이터베이스를 선택합니다.  
  
 **통합 보안**  
 Windows 통합 인증을 사용하여 연결하려면(권장) **True**를 지정하고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려면 **False**를 지정합니다. **False**를 지정하면 사용자 ID와 암호를 입력해야 합니다. 기본값은 **False**입니다.  
  
 **사용자 ID**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 암호를 입력합니다.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>ODBC Driver for SQL Server를 사용하여 SQL Server에 연결 
ODBC 드라이버는 데이터 원본의 드롭다운 목록에 표시되지 않습니다. ODBC 드라이버를 사용하여 연결하려면 **.NET Framework Data Provider for ODBC**를 데이터 원본으로 선택합니다. 이 공급자는 ODBC 드라이버 주위의 래퍼 역할을 합니다.

> [!TIP]
> **최신 드라이버를 가져오세요**. [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)를 다운로드합니다.

다음은 .NET Framework Data Provider for ODBC를 선택한 직후 표시되는 일반적인 화면입니다.

![이전에 ODBC를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>지정할 옵션(ODBC Driver for SQL Server)

> [!NOTE]
> ODBC 드라이버에 대한 연결 옵션은 SQL Server가 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

최신 ODBC 드라이버를 사용하여 SQL Server에 연결하려면 다음 설정 및 해당 값을 포함하는 연결 문자열을 조합합니다. 전체 연결 문자열의 형식은 설정 목록 바로 뒤에 나옵니다.

> [!TIP]
> 도움을 받아 연결 문자열을 적절하게 조합합니다. 또는 연결 문자열을 제공하는 대신 기존 DSN(데이터 원본 이름)을 제공하거나 새 DSN을 만듭니다. 이러한 옵션에 대한 자세한 내용은 [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.

**드라이버**  
ODBC 드라이버의 이름입니다. 이름은 드라이버의 다른 버전에 따라 다릅니다.

**Server**  
SQL Server 이름입니다.

**데이터베이스 백업**  
데이터베이스의 이름입니다.  

**Trusted_Connection** 또는 **Uid**/**Pwd**  
Windows 통합 인증을 사용하여 연결하려면 **Trusted_Connection=Yes**를 지정하거나, SQL Server 인증을 사용하여 연결하려면 **Uid**(사용자 ID) 및 **Pwd**(암호)를 지정합니다.

### <a name="connection-string-format"></a>연결 문자열 형식
다음은 Windows 통합 인증을 사용하는 연결 문자열의 형식입니다.

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

다음은 Windows 통합 인증 대신 SQL Server 인증을 사용하는 연결 문자열의 형식입니다.

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>연결 문자열 입력
**데이터 원본 선택** 또는 **대상 선택** 페이지에서 **ConnectionString** 필드에 연결 문자열을 입력하거나 **Dsn** 필드에 DSN 이름을 입력합니다. 연결 문자열을 입력하면 마법사에서 문자열을 구문 분석하고 개별 속성과 해당 값을 목록에 표시합니다.

다음 예제에서는 이 연결 문자열을 사용합니다.

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

다음은 연결 문자열을 입력한 후 표시되는 화면입니다.

![이후에 ODBC를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Microsoft OLE DB Provider for SQL Server 또는 SQL Server Native Client를 사용하여 SQL Server에 연결

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server 및 SQL Server Native Client는 SQL Server 2012 이후 버전에서 지원되지 않습니다. 대신 ODBC 드라이버를 사용합니다. ODBC 드라이버로 전환하는 방법에 대한 자세한 내용은 다음 블로그 게시물을 참조하세요.
>   -   [고유 관계형 데이터 액세스용 ODBC에 대한 Microsoft 지원](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [새로운 Microsoft ODBC Driver for SQL Server에 대한 소개](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 추가 정보
여기에 나열되지 않은 데이터 공급자를 사용하여 SQL Server에 연결하는 방법에 대한 자세한 내용은 [SQL Server 연결 문자열](https://www.connectionstrings.com/sql-server/)을 참조하세요. 또한 이러한 타사 사이트에는 이 페이지에서 설명하는 데이터 공급자 및 연결 매개 변수에 대한 자세한 정보가 포함되어 있습니다.

## <a name="see-also"></a>관련 항목:
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

