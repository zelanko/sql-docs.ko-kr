---
title: "(SQL Server 가져오기 및 내보내기 마법사)는 MySQL 데이터 원본에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3df56fcda5b39c2895de83feac4f302686b1adf3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>(SQL Server 가져오기 및 내보내기 마법사)는 MySQL 데이터 원본에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **MySQL** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다. MySQL에 연결 하는 데 사용할 수 있는 여러 데이터 공급자가 있습니다.

> [!IMPORTANT]
> 자세한 요구 사항 및 MySQL 데이터베이스에 연결 하기 위한 필수 구성 요소는이 Microsoft 문서에서 다루지 않습니다. 이 문서에서는 이미 MySQL 클라이언트 소프트웨어가 설치 되어 있고 연결할 수 있는지 이미 성공적으로 대상 MySQL 데이터베이스를 가정 합니다. 자세한 정보에 대 한 MySQL 데이터베이스 관리자 또는 MySQL 설명서를 참조 하십시오.

## <a name="get-the-mysql-connectors"></a>MySQL 커넥터 가져오기
공급자와 드라이버에서이 항목에 설명 된 다운로드는 [MySQL 커넥터](https://dev.mysql.com/downloads/connector/) 페이지.

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>MySQL에 연결할.Net Framework Data Provider for MySQL
선택한 후 **MySQL에 대 한.NET Framework Data Provider** 에 **데이터 원본을 선택** 또는 **대상 선택** 마법사 페이지의 페이지 옵션은 공급자에 대 한 그룹화 된 목록을 제공 합니다. 이들 중 대부분은 이해 하기 어려운 이름 및 생소 한 설정입니다. 에서는 몇 가지 정보를 제공 하기만 하면 됩니다. 다른 설정에 대 한 기본값을 무시할 수 있습니다.

> [!NOTE]
> 이 데이터 공급자에 대 한 연결 옵션 MySQL 소스 또는 대상 인지 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

|필수 정보|.NET framework Data Provider for MySQL 속성|
|---|---|
|서버 이름|**Server**|
|데이터베이스 이름|**데이터베이스**|
|인증 (로그인) 정보|**사용자 Id** 및 **암호**|

연결 문자열을 입력할 필요가 없습니다는 **ConnectionString** 필드 목록입니다. MySQL 서버 이름에 대 한 개별 값을 입력 한 후 (**서버**)을 로그인 정보, 마법사 개별 속성 및 해당 값에서 연결 문자열을 조합 합니다. 

![1 / 2.NET 공급자와 함께 MySQL에 연결](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![2 / 2.NET 공급자와 함께 MySQL에 연결](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>MySQL ODBC 드라이버와 MySQL에 연결
ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. ODBC 드라이버를 연결 하려면 선택 하 여 시작 된 **.NET Framework Data Provider for ODBC** 데이터 원본으로 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 이 공급자는 ODBC 드라이버 주위에서 래퍼로 역할을 합니다.

다음은.NET Framework Data Provider for ODBC 선택한 후 볼 수 있는 제네릭 화면입니다.

![전에 odbc SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>(MySQL ODBC 드라이버)를 지정 하는 옵션

> [!NOTE]
> 이 데이터 공급자와 ODBC 드라이버에 대 한 연결 옵션 MySQL 소스 또는 대상 인지 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

다음 설정 및 값을 포함 하는 연결 문자열을 조합 하 MySQL ODBC 드라이버와 MySQL에 연결 합니다. 전체 연결 문자열의 형식이 설정 목록 바로 뒤에.

> [!TIP]
> 가장 적합 하는 연결 문자열을 어셈블하여 도움말을 봅니다. 연결 문자열을 제공 하는 대신 기존의 DSN (데이터 원본 이름)를 제공 합니다. 아니면를 새로 만듭니다. 이러한 옵션에 대 한 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.

**드라이버**  
ODBC 드라이버의 이름입니다.

**Server**  
MySQL server의 이름입니다. 

**데이터베이스**  
MySQL 데이터베이스의 이름입니다.

**UID** 및 **PWD**   
사용자 id와 암호를 연결 합니다.

### <a name="connection-string-format"></a>연결 문자열 형식
일반적인 연결 문자열의 형식은 다음과 같습니다.

    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>

### <a name="enter-the-connection-string"></a>연결 문자열 입력
에 대 한 연결 문자열을 입력의 **ConnectionString** 에 DSN 이름을 입력 하거나 필드는 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 연결 문자열을 입력 한 후 마법사는 문자열을 구문 분석 하 고 목록에서 개별 속성 및 해당 값을 표시 합니다.

다음 예제에서는이 연결 문자열을 사용합니다.

    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********

다음은 연결 문자열을 입력 한 후 표시 되는 화면입니다.

![ODBC로 MySQL에 연결](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>다른 데이터 공급자 및 자세한 정보
여기에 나열 되어 있지 않은 데이터 공급자와 MySQL에 연결 하는 방법에 대 한 정보를 참조 하십시오. [MySQL 연결 문자열](https://www.connectionstrings.com/mysql/)합니다. 또한이 제 3 자 사이트 데이터 공급자 및 연결 매개 변수가이 페이지에서 설명 하는 방법에 대 한 자세한 정보를 포함 합니다.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


