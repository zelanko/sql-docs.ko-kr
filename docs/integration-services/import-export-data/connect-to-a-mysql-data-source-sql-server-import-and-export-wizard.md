---
title: MySQL 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a0cc86dfd923b3a17981b970dfb9aedbb888a0b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914226"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>MySQL 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **MySQL** 데이터 원본에 연결하는 방법을 보여 줍니다. MySQL에 연결하는 데 사용할 수 있는 데이터 공급자는 여러 개입니다.

> [!IMPORTANT]
> MySQL 데이터베이스에 연결하기 위한 자세한 요구 사항 및 필수 구성 요소는 이 Microsoft 문서에서 다루지 않습니다. 이 문서에서는 여러분의 컴퓨터에 MySQL 클라이언트 소프트웨어가 설치되어 있고 대상 MySQL 데이터베이스에 연결할 수 있다고 가정합니다. 자세한 내용은 MySQL 데이터베이스 관리자에게 문의하거나 MySQL 설명서를 참조하세요.

## <a name="get-the-mysql-connectors"></a>MySQL 커넥터 가져오기
[MySQL 커넥터](https://dev.mysql.com/downloads/connector/) 페이지에서 이 문서에 설명된 공급자 및 드라이버를 다운로드합니다.

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>.NET Framework Data Provider for MySQL을 사용하여 MySQL에 연결
마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **.NET Framework Data Provider for MySQL**을 선택하면 페이지에 공급자에 대한 옵션의 그룹화된 목록이 표시됩니다. 이러한 속성 중 대부분은 이해하기 어려운 이름이거나 생소한 설정입니다. 여기에서는 몇 가지 정보만 제공하면 됩니다. 다른 설정의 기본값은 무시할 수 있습니다.

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 MySQL이 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

|필수 정보|.Net Framework Data Provider for MySQL 속성|
|---|---|
|서버 이름|**Server**|
|데이터베이스 이름|**Database**|
|인증(로그인) 정보|**사용자 ID** 및 **암호**|
|||

목록의 **ConnectionString** 필드에 연결 문자열을 입력할 필요가 없습니다. MySQL 서버 이름(**Server**) 및 로그인 정보에 대한 개별 값을 입력하면 마법사는 개별 속성과 값에서 연결 문자열을 어셈블합니다. 

![.NET 공급자로 MySQL에 연결, 1/2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![.NET 공급자로 MySQL에 연결, 2/2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>MySQL ODBC 드라이버로 MySQL에 연결
ODBC 드라이버는 데이터 원본의 드롭다운 목록에 표시되지 않습니다. ODBC 드라이버를 연결하려면 먼저 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 데이터 원본으로 **.NET Framework Data Provider for ODBC**를 선택합니다. 이 공급자는 ODBC 드라이버 주위에서 래퍼 역할을 합니다.

다음은 .NET Framework Data Provider for ODBC를 선택한 직후 표시되는 일반적인 화면입니다.

![이전에 ODBC를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>지정할 옵션(MySQL ODBC 드라이버)

> [!NOTE]
> 이 데이터 공급자 및 ODBC 드라이버의 연결 옵션은 MySQL이 원본이건 대상이건 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

MySQL ODBC 드라이버를 사용하여 MySQL에 연결하려면 다음 설정 및 값을 포함하는 연결 문자열을 조합합니다. 전체 연결 문자열의 형식은 설정 목록 바로 뒤에 나옵니다.

> [!TIP]
> 도움을 받아 연결 문자열을 적절하게 조합합니다. 또는 연결 문자열을 제공하는 대신 기존 DSN(데이터 원본 이름)을 제공하거나 새 DSN을 만듭니다. 이러한 옵션에 대한 자세한 내용은 [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.

**드라이버**  
ODBC 드라이버의 이름입니다.

**Server**  
MySQL 서버의 이름입니다. 

**Database**  
MySQL 데이터베이스의 이름입니다.

**UID** 및 **PWD**   
연결할 사용자 ID와 암호입니다.

### <a name="connection-string-format"></a>연결 문자열 형식
다음은 일반적인 연결 문자열의 형식입니다.

```console
Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
```

### <a name="enter-the-connection-string"></a>연결 문자열 입력
**데이터 원본 선택** 또는 **대상 선택** 페이지에서 **ConnectionString** 필드에 연결 문자열을 입력하거나 **Dsn** 필드에 DSN 이름을 입력합니다. 연결 문자열을 입력하면 마법사에서 문자열을 구문 분석하고 개별 속성과 해당 값을 목록에 표시합니다.

다음 예제에서는 이 연결 문자열을 사용합니다.

```console
Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
```

다음은 연결 문자열을 입력한 후 표시되는 화면입니다.

![ODBC로 MySQL에 연결](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 추가 정보
여기에 나열되지 않은 데이터 공급자를 사용하여 MySQL에 연결하는 방법에 대한 내용은 [MySQL 연결 문자열](https://www.connectionstrings.com/mysql/)을 참조하세요. 또한 이러한 타사 사이트에는 이 페이지에서 설명하는 데이터 공급자 및 연결 매개 변수에 대한 자세한 정보가 포함되어 있습니다.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

