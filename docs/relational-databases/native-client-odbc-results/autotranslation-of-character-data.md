---
title: 문자 데이터의 자동 번역 | 마이크로 소프트 문서
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a8672f748af8d643fa39038be030efa5d434dc8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297884"
---
# <a name="autotranslation-of-character-data"></a>문자 데이터 자동 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL_C_CHAR 선언된 ANSI 문자 변수와 같은 문자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 또는 **char,** **varchar**또는 **텍스트** 데이터 형식을 사용하여 저장된 데이터는 제한된 수의 문자만 나타낼 수 있습니다. 즉, 문자당 1바이트를 사용하여 저장된 문자 데이터는 246자만 나타낼 수 있습니다. SQL_C_CHAR 변수에 저장된 값은 클라이언트 컴퓨터의 ACP(ANSI 코드 페이지)를 사용하여 해석되고, 서버의 **char,** **varchar**또는 **텍스트** 데이터 형식을 사용하여 저장된 값은 서버의 ACP를 사용하여 평가됩니다.  
  
 서버와 클라이언트모두 동일한 ACP를 가지고 있는 경우 SQL_C_CHAR, **char,** **varchar**또는 **텍스트** 개체에 저장된 값을 해석하는 데 아무런 문제가 없습니다. 서버와 클라이언트에 서로 다른 AMP가 있는 경우 char, **varchar**또는 **텍스트** 열, 변수 또는 매개 **변수에**사용되는 경우 클라이언트의 SQL_C_CHAR 데이터가 서버의 다른 문자로 해석될 수 있습니다. 예를 들어, 0xA5 값을 포함하는 문자 바이트는 코드 페이지 437을 사용하는 컴퓨터에서 문자 Ñ로 해석되고 코드 페이지 1252를 실행하는 컴퓨터에서 엔 기호(¥)로 해석됩니다.  
  
 유니코드 데이터는 문자당 2바이트를 사용하여 저장됩니다. 유니코드 사양에 따라 모든 확장 문자가 처리되기 때문에 모든 유니코드 문자는 컴퓨터에 관계없이 동일하게 해석됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버의 AutoTranslate 기능은 클라이언트와 다른 코드 페이지가 있는 서버 간에 문자 데이터를 이동하는 문제를 최소화하려고 시도합니다. 자동 번역은 [SQLDriverConnect의](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)연결 문자열, [SQLConfigDataSource의](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)구성 문자열또는 ODBC 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버의 데이터 원본을 구성할 때 설정할 수 있습니다.  
  
 자동 번역이 "아니요"로 설정되면 클라이언트와 **char,** **varchar**또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **데이터베이스의 텍스트** 열, 변수 또는 매개 변수 간에 이동된 SQL_C_CHAR 데이터에 대한 변환이 수행되지 않습니다. 데이터에 확장 문자가 포함되어 있고 클라이언트 컴퓨터와 서버 컴퓨터에서 서로 다른 코드 페이지를 사용하면 두 컴퓨터에서 비트 패턴이 서로 다르게 해석될 수 있습니다. 그러나 두 컴퓨터에서 동일한 코드 페이지를 사용하면 데이터가 동일하게 해석됩니다.  
  
 AutoTranslate가 "예"로 설정되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 유니코드를 사용하여 클라이언트와 **char,** **varchar**또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **데이터베이스의 텍스트** 열, 변수 또는 매개 변수 SQL_C_CHAR 간에 이동된 데이터를 변환합니다.  
  
-   클라이언트의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_C_CHAR 변수에서 데이터베이스의 **char,** **varchar**또는 **텍스트** 열, 변수 또는 매개 변수로 데이터를 전송하는 경우 ODBC 드라이버는 먼저 클라이언트의 ACP를 사용하여 SQL_C_CHAR 유니코드로 변환한 다음 유니코드에서 서버의 ACP를 사용하여 문자로 다시 변환합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char,** **varchar**또는 **텍스트** 열, 변수 또는 매개 변수에서 클라이언트의 SQL_C_CHAR 변수로 데이터를 전송하는 경우 네이티브 클라이언트 ODBC 드라이버는 먼저 서버의 ACP를 사용하여 문자에서 유니코드로 변환한 다음 유니코드에서 클라이언트의 ACP를 사용하여 SQL_C_CHAR 변환합니다.  
  
 이러한 모든 변환은 클라이언트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행되는 네이티브 클라이언트 ODBC 드라이버에 의해 수행되므로 서버 ACP는 클라이언트 컴퓨터에 설치된 코드 페이지 중 하나여야 합니다.  
  
 유니코드를 통해 문자를 변환하면 두 코드 페이지에 있는 모든 문자가 올바로 변환됩니다. 문자가 한 코드 페이지에만 있고 다른 한 코드 페이지에는 없는 경우 대상 코드 페이지에서 해당 문자를 나타낼 수 없습니다. 예를 들어 코드 페이지 1252에는 등록 상표 기호( )가 있지만 코드 페이지 437에는 없습니다.  
  
 다음과 같은 변환 작업은 AutoTranslate 설정의 영향을 받지 않습니다.  
  
-   문자 SQL_C_CHAR 클라이언트 변수와 유니코드 **nchar,** **nvarchar**또는 **ntext** 열, 변수 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 매개 변수 간에 데이터를 이동합니다.  
  
-   유니코드 SQL_C_WCHAR 클라이언트 변수와 문자 **char,** **varchar**또는 **텍스트** 열, 변수 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 매개 변수 간에 데이터를 이동합니다.  
  
 데이터를 문자에서 유니코드로 이동할 때는 항상 변환해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;처리 결과](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
