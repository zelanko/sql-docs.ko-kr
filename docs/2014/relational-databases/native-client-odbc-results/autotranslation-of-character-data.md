---
title: 문자 데이터는 Autotranslation | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5182ab1a72caac4181e50df2199f3e0457d3aaac
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806595"
---
# <a name="autotranslation-of-character-data"></a>문자 데이터 자동 변환
  ANSI 같은 문자 데이터를 SQL_C_CHAR로 선언 된 변수 또는 저장 된 데이터 문자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여는 **char**를 **varchar**, 또는 **텍스트** 데이터 형식 수 제한 된 수를의 문자를 나타냅니다. 즉, 문자당 1바이트를 사용하여 저장된 문자 데이터는 246자만 나타낼 수 있습니다. SQL_C_CHAR 변수에 저장된 값은 클라이언트 컴퓨터의 ACP(ANSI 코드 페이지)를 사용하여 해석되고, 사용 하 여 저장 된 값 **문자**, **varchar**, 또는 **텍스트** 데이터 형식은 서버에서 서버의 ACP를 사용 하 여 계산 됩니다.  
  
 서버와 클라이언트에 동일한 ACP 경우 이러한 문제가 발생 하지 않습니다 SQL_C_CHAR 라는 저장 된 값을 해석 **char**하십시오 **varchar**, 또는 **텍스트** 개체입니다. 서버와 클라이언트는 서로 다른 Acp를 사용 하면 경우에 사용 되는 경우 클라이언트의 SQL_C_CHAR 데이터를 서버의 다른 문자로 해석 될 수 있습니다 **char**하십시오 **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수입니다. 예를 들어 값 0xA5이 포함 된 문자 바이트가 문자로 해석 됩니다?? 코드를 사용 하는 컴퓨터 페이지 437 및 코드 페이지 1252 실행 하는 컴퓨터는 엔 로그온 (?)으로 해석 됩니다.  
  
 유니코드 데이터는 문자당 2바이트를 사용하여 저장됩니다. 유니코드 사양에 따라 모든 확장 문자가 처리되기 때문에 모든 유니코드 문자는 컴퓨터에 관계없이 동일하게 해석됩니다.  
  
 기능이 통합 된 AutoTranslate는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버를 악센트 부호가 있는 문자 데이터는 클라이언트와 서버 간에 이동 하는 문제를 최소화 하려고 합니다. AutoTranslate의 연결 문자열에서 설정할 수 있습니다 [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md)의 구성 문자열에 [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)에 대 한 데이터 소스를 구성할 때의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC ODBC 관리자를 사용 하는 드라이버입니다.  
  
 클라이언트의 SQL_C_CHAR 변수와 간에 이동 되는 데이터에서 변환이 수행 됩니다 AutoTranslate 설정 되 면 "no"로 하 고 **char**를 **varchar**, 또는 **텍스트** 열, 변수 또는에서 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 데이터에 확장 문자가 포함되어 있고 클라이언트 컴퓨터와 서버 컴퓨터에서 서로 다른 코드 페이지를 사용하면 두 컴퓨터에서 비트 패턴이 서로 다르게 해석될 수 있습니다. 그러나 두 컴퓨터에서 동일한 코드 페이지를 사용하면 데이터가 동일하게 해석됩니다.  
  
 AutoTranslate "yes"로 설정 된 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 유니코드를 사용 하 여 클라이언트의 SQL_C_CHAR 변수와 간에 이동 되는 데이터를 변환 하 고 **char**를 **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스:  
  
-   클라이언트의 SQL_C_CHAR 변수에서 데이터를 보내는 경우는 **char**를 **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 데이터베이스 드라이버는 먼저 다음 다시 서버의 ACP를 사용 하는 유니코드에서에서 클라이언트의 ACP를 사용 하 여 유니코드를 SQL_C_CHAR에서 변환 합니다.  
  
-   데이터를 보내는 경우는 **char**, **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_C_CHAR 변수로 는클라이언트에서데이터베이스[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 먼저 클라이언트의 ACP를 사용 하 여 SQL_C_CHAR로 다시 유니코드에서 다음 서버의 ACP를 사용 하 여 유니코드로 문자에서 변환 합니다.  
  
 모든 이러한 변환을 수행한 때문에 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ACP 서버는 클라이언트에서 실행 되는 네이티브 클라이언트 ODBC 드라이버가 클라이언트 컴퓨터에 설치 된 코드 페이지 중 하나 여야 합니다.  
  
 유니코드를 통해 문자를 변환하면 두 코드 페이지에 있는 모든 문자가 올바로 변환됩니다. 문자가 한 코드 페이지에만 있고 다른 한 코드 페이지에는 없는 경우 대상 코드 페이지에서 해당 문자를 나타낼 수 없습니다. 예를 들어 코드 페이지 1252 코드 페이지 437 않습니다 하지만 등록된 상표 기호 (?)에 있습니다.  
  
 다음과 같은 변환 작업은 AutoTranslate 설정의 영향을 받지 않습니다.  
  
-   문자 SQL_C_CHAR 클라이언트 변수와 유니코드 간 데이터 이동 **nchar**하십시오 **nvarchar**, 또는 **ntext** 열, 변수 또는 매개 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
-   유니코드 SQL_C_WCHAR 클라이언트 변수와 문자 간 데이터 이동 **char**하십시오 **varchar**, 또는 **텍스트** 열, 변수 또는 매개 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
 데이터를 문자에서 유니코드로 이동할 때는 항상 변환해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [결과 처리 &#40;ODBC&#41;](processing-results-odbc.md)   
 [데이터 정렬 및 유니코드 지원](../collations/collation-and-unicode-support.md)  
  
  
