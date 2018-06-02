---
title: 커서 사용 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f4fd700f6642f2cbb6fae33115229a323689686e
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707731"
---
# <a name="using-cursors-odbc"></a>커서 사용(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC는 다음을 허용하는 커서 모델을 지원합니다.  
  
-   여러 커서 유형  
  
-   커서 내에서 스크롤 및 위치 지정  
  
-   여러 동시성 옵션  
  
-   위치 지정 업데이트  
  
 ODBC 응용 프로그램은 거의 커서를 선언하여 열거나 커서 관련 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하지 않습니다. SQL 문에서 반환된 모든 결과 집합에 대해 ODBC에서 자동으로 커서를 엽니다. 커서의 특징은 문 특성을 사용 하 여 설정에 의해 제어 됩니다 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) SQL 하기 전에 문이 실행 됩니다. 결과 집합 처리를 위한 ODBC API 함수는 인출, 스크롤 및 위치 지정 업데이트를 비롯한 모든 커서 기능을 지원합니다.  
  
 다음은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트와 ODBC 응용 프로그램의 커서 작업 방법을 비교한 것입니다.  
  
|작업|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|커서 동작 정의|DECLARE CURSOR 매개 변수를 통해 지정|사용 하 여 커서 특성 설정 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)|  
|커서 열기|커서 열기 선언 *cursor_name*|**SQLExecDirect** 또는 **SQLExecute**|  
|행 인출|FETCH|**SQLFetch** 또는 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|위치 지정 업데이트|UPDATE 또는 DELETE의 WHERE CURRENT OF 절|**SQLSetPos**|  
|커서 닫기|닫기 *cursor_name* DEALLOCATE|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 구현된 서버 커서는 ODBC 커서 모델의 기능을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 서버 커서를 사용하여 ODBC API의 커서 기능을 지원합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [커서 구현 방법](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [커서 유형](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [커서 동작](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [커서 속성](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [커서 프로그래밍 정보 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [행 스크롤 및 페치](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [위치 지정 업데이트 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [커서](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
