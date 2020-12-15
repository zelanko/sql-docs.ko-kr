---
description: 문자 데이터 자동 변환
title: 문자 데이터의 자동 변환을 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2de8b3a1fc6b1bd6547ec413fb5d8e4e0fbca6dd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438268"
---
# <a name="autotranslation-of-character-data"></a>문자 데이터 자동 변환
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **CHAR**, **varchar** 또는 **text** 데이터 형식을 사용 하 여 SQL_C_CHAR 선언 된 ANSI 문자 변수와 같은 문자 데이터는 제한 된 수의 문자만 나타낼 수 있습니다. 즉, 문자당 1바이트를 사용하여 저장된 문자 데이터는 246자만 나타낼 수 있습니다. SQL_C_CHAR 변수에 저장된 값은 클라이언트 컴퓨터의 ACP(ANSI 코드 페이지)를 사용하여 해석되고, 서버에서 **char**, **varchar** 또는 **text** 데이터 형식을 사용 하 여 저장 된 값은 서버의 ACP를 사용 하 여 평가 됩니다.  
  
 서버와 클라이언트 모두에 동일한 ACP가 있는 경우 SQL_C_CHAR, **CHAR**, **varchar** 또는 **text** 개체에 저장 된 값을 해석 하는 데 문제가 없습니다. 서버와 클라이언트가 다른 ACPs를 사용 하는 경우 **CHAR**, **varchar** 또는 **text** 열, 변수 또는 매개 변수에 사용 되는 경우 클라이언트의 SQL_C_CHAR 데이터가 서버에서 다른 문자로 해석 될 수 있습니다. 예를 들어 0xA5 값을 포함 하는 문자 바이트는 코드 페이지 437를 사용 하는 컴퓨터에서 문자 Ñ 해석 되 고 코드 페이지 1252를 실행 하는 컴퓨터에서 엔화 기호 (¥)로 해석 됩니다.  
  
 유니코드 데이터는 문자당 2바이트를 사용하여 저장됩니다. 유니코드 사양에 따라 모든 확장 문자가 처리되기 때문에 모든 유니코드 문자는 컴퓨터에 관계없이 동일하게 해석됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버의 자동 변환 기능은 다른 코드 페이지를 포함 하는 클라이언트와 서버 간에 문자 데이터를 이동 하는 문제를 최소화 하려고 시도 합니다. AutoTranslate은 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)의 연결 문자열에서 설정 하거나, [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)의 구성 문자열에서 설정 하거나, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] odbc 관리자를 사용 하 여 Native Client odbc 드라이버에 대 한 데이터 원본을 구성할 때 설정할 수 있습니다.  
  
 AutoTranslate를 "no"로 설정 하면 클라이언트의 SQL_C_CHAR 변수와 데이터베이스의 **CHAR**, **varchar** 또는 **text** 열, 변수 또는 매개 변수 간에 이동 되는 데이터에 대 한 변환이 수행 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 데이터에 확장 문자가 포함되어 있고 클라이언트 컴퓨터와 서버 컴퓨터에서 서로 다른 코드 페이지를 사용하면 두 컴퓨터에서 비트 패턴이 서로 다르게 해석될 수 있습니다. 그러나 두 컴퓨터에서 동일한 코드 페이지를 사용하면 데이터가 동일하게 해석됩니다.  
  
 AutoTranslate를 "예"로 설정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 유니코드를 사용 하 여 클라이언트의 SQL_C_CHAR 변수 사이에서 이동 하는 데이터와 데이터베이스의 **CHAR**, **varchar** 또는 **text** 열, 변수 또는 매개 변수로 데이터를 변환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   클라이언트의 SQL_C_CHAR 변수에서 데이터베이스의 **CHAR**, **varchar** 또는 **text** 열, 변수 또는 매개 변수로 데이터를 전송 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버는 먼저 클라이언트의 Acp를 사용 하 여 SQL_C_CHAR에서 유니코드로 변환한 다음, 서버의 acp를 사용 하 여 유니코드에서 문자로 다시 변환 합니다.  
  
-   데이터베이스의 **char**, **varchar** 또는 **text** 열, 변수 또는 매개 변수에서 클라이언트의 SQL_C_CHAR 변수로 데이터가 전송 될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client ODBC 드라이버는 먼저 서버 acp를 사용 하 여 문자에서 유니코드로 변환한 다음, 유니코드에서 클라이언트의 acp를 사용 하 여 SQL_C_CHAR으로 다시 변환 합니다.  
  
 이러한 모든 변환은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트에서 실행 되는 Native CLIENT ODBC 드라이버에 의해 수행 되므로 서버 ACP는 클라이언트 컴퓨터에 설치 된 코드 페이지 중 하나 여야 합니다.  
  
 유니코드를 통해 문자를 변환하면 두 코드 페이지에 있는 모든 문자가 올바로 변환됩니다. 문자가 한 코드 페이지에만 있고 다른 한 코드 페이지에는 없는 경우 대상 코드 페이지에서 해당 문자를 나타낼 수 없습니다. 예를 들어 코드 페이지 1252에는 등록 상표 기호( )가 있지만 코드 페이지 437에는 없습니다.  
  
 다음과 같은 변환 작업은 AutoTranslate 설정의 영향을 받지 않습니다.  
  
-   데이터베이스에서 문자 SQL_C_CHAR 클라이언트 변수와 유니코드 **nchar**, **nvarchar** 또는 **ntext** 열, 변수 또는 매개 변수로 데이터를 이동 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
-   데이터베이스에서 유니코드 SQL_C_WCHAR 클라이언트 변수와 문자 **char**, **varchar** 또는 **text** 열, 변수 또는 매개 변수 간에 데이터를 이동 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 데이터를 문자에서 유니코드로 이동할 때는 항상 변환해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;결과 처리 ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
