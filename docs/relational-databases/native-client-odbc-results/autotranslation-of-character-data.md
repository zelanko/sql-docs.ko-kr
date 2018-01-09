---
title: "문자 데이터 자동 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 566e248ce15929f8ff599602e920544df395a453
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="autotranslation-of-character-data"></a>문자 데이터 자동 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  문자 데이터를 ANSI 문자 SQL_C_CHAR로 선언 된 변수 또는 데이터에 저장 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하는 **char**, **varchar**, 또는 **텍스트** 데이터 형식 수 제한 된 수를의 문자를 나타냅니다. 즉, 문자당 1바이트를 사용하여 저장된 문자 데이터는 246자만 나타낼 수 있습니다. SQL_C_CHAR 변수에 저장된 값은 클라이언트 컴퓨터의 ACP(ANSI 코드 페이지)를 사용하여 해석되고, 사용 하 여 저장 된 값 **char**, **varchar**, 또는 **텍스트** 서버의 ACP를 사용 하 여 서버에서 데이터 형식을 평가 됩니다.  
  
 서버와 클라이언트 모두에서 동일한 ACP 경우 이러한 문제가 발생 하지 않습니다 SQL_C_CHAR에 저장 된 값을 해석 **char**, **varchar**, 또는 **텍스트** 개체입니다. 서버와 클라이언트가 서로 다른 Acp를 한 경우 클라이언트의 SQL_C_CHAR 데이터에 사용 되는 경우 서버에서 다른 문자로 해석 될 수 있습니다 **char**, **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수입니다. 예를 들어, 0xA5 값이 포함 된 문자 바이트가 코드 페이지 437 사용 하는 컴퓨터에서는 Ñ 문자로 해석 되 고 코드 페이지 1252 실행 하는 컴퓨터에서는 엔화 기호 (￥)으로 해석 됩니다.  
  
 유니코드 데이터는 문자당 2바이트를 사용하여 저장됩니다. 유니코드 사양에 따라 모든 확장 문자가 처리되기 때문에 모든 유니코드 문자는 컴퓨터에 관계없이 동일하게 해석됩니다.  
  
 AutoTranslate 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 문제 문자 데이터를 이동 하는 클라이언트와 서버 간에 서로 다른 코드 페이지를 최소화 하려고 시도 합니다. AutoTranslate의 연결 문자열에 설정할 수 있습니다 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)의 구성 문자열에서 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)에 대 한 데이터 원본을 구성할 때 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ODBC 관리자를 사용 하 여 드라이버입니다.  
  
 클라이언트의 SQL_C_CHAR 변수와 간에 이동 되는 데이터에 변환을 수행은 AutoTranslate 설정 된 경우 "no"로, 및 **char**, **varchar**, 또는 **텍스트** 열, 변수 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 데이터에 확장 문자가 포함되어 있고 클라이언트 컴퓨터와 서버 컴퓨터에서 서로 다른 코드 페이지를 사용하면 두 컴퓨터에서 비트 패턴이 서로 다르게 해석될 수 있습니다. 그러나 두 컴퓨터에서 동일한 코드 페이지를 사용하면 데이터가 동일하게 해석됩니다.  
  
 AutoTranslate "yes"로 설정 된 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 유니코드를 사용 하 여 클라이언트의 SQL_C_CHAR 변수와 간에 이동 되는 데이터를 변환 하 고 **char**, **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스:  
  
-   클라이언트의 SQL_C_CHAR 변수에서 데이터를 보내면는 **char**, **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스, ODBC 드라이버는 먼저 다시 서버의 ACP를 사용 하 여 문자를 유니코드에서 다음 클라이언트의 ACP를 사용 하 여 유니코드로 SQL_C_CHAR에서 변환 합니다.  
  
-   데이터를 보내면는 **char**, **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 클라이언트의SQL_C_CHAR변수로데이터베이스[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 먼저 유니코드를 SQL_C_CHAR 클라이언트의 ACP를 사용 하 여 이동 후 서버의 ACP를 사용 하 여 유니코드로 문자에서 변환 합니다.  
  
 이러한 모든 변환 실행 되므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 서버 ACP는 클라이언트에서 실행 클라이언트 컴퓨터에 설치 된 코드 페이지 중 하나 여야 합니다.  
  
 유니코드를 통해 문자를 변환하면 두 코드 페이지에 있는 모든 문자가 올바로 변환됩니다. 문자가 한 코드 페이지에만 있고 다른 한 코드 페이지에는 없는 경우 대상 코드 페이지에서 해당 문자를 나타낼 수 없습니다. 예를 들어 코드 페이지 1252에는 등록 상표 기호( )가 있지만 코드 페이지 437에는 없습니다.  
  
 다음과 같은 변환 작업은 AutoTranslate 설정의 영향을 받지 않습니다.  
  
-   문자 SQL_C_CHAR 클라이언트 변수와 유니코드 간의 데이터 이동 **nchar**, **nvarchar**, 또는 **ntext** 열, 변수 또는 매개 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
-   유니코드 SQL_C_WCHAR 클라이언트 변수와 문자 간 데이터 이동 **char**, **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
 데이터를 문자에서 유니코드로 이동할 때는 항상 변환해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [처리 결과 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
