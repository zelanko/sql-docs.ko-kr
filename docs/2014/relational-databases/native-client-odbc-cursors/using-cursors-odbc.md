---
title: 커서 사용 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 61afedab4f4a1e309a08d9c2421ca7889811da8a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020455"
---
# <a name="using-cursors-odbc"></a>커서 사용(ODBC)
  ODBC는 다음을 허용하는 커서 모델을 지원합니다.  
  
-   여러 커서 유형  
  
-   커서 내에서 스크롤 및 위치 지정  
  
-   여러 동시성 옵션  
  
-   위치 지정 업데이트  
  
 ODBC 애플리케이션은 거의 커서를 선언하여 열거나 커서 관련 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하지 않습니다. SQL 문에서 반환된 모든 결과 집합에 대해 ODBC에서 자동으로 커서를 엽니다. 커서의 특징은 SQL 문이 실행 되기 전에 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 로 설정 된 문 특성에 의해 제어 됩니다. 결과 집합 처리를 위한 ODBC API 함수는 인출, 스크롤 및 위치 지정 업데이트를 비롯한 모든 커서 기능을 지원합니다.  
  
 다음은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트와 ODBC 애플리케이션의 커서 작업 방법을 비교한 것입니다.  
  
|작업|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|커서 동작 정의|DECLARE CURSOR 매개 변수를 통해 지정|[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 를 사용 하 여 커서 특성 설정|  
|커서 열기|커서 열기 *CURSOR_NAME* 선언|**Sqlexecdirect** 또는 **sqlexecute**|  
|행 인출|FETCH|**Sqlfetch** 또는 [sqlfetchscroll](../native-client-odbc-api/sqlfetchscroll.md)|  
|위치 지정 업데이트|UPDATE 또는 DELETE의 WHERE CURRENT OF 절|**SQLSetPos**|  
|커서 닫기|닫기 *cursor_name* 할당 취소|[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 구현된 서버 커서는 ODBC 커서 모델의 기능을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 서버 커서를 사용하여 ODBC API의 커서 기능을 지원합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [커서 구현 방법](implementation/how-cursors-are-implemented.md)  
  
-   [커서 유형](cursor-types.md)  
  
-   [커서 동작](cursor-behaviors.md)  
  
-   [커서 속성](properties/cursor-properties.md)  
  
-   [ODBC&#41;&#40;커서 프로그래밍 정보](programming/cursor-programming-details-odbc.md)  
  
-   [행 스크롤 및 페치](../native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [ODBC&#41;&#40;위치 지정 업데이트](positioned-updates-odbc.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [&#40;Transact-sql&#41;를 닫습니다.](/sql/t-sql/language-elements/close-transact-sql)   
 [커서로](../../relational-databases/cursors.md)   
 [Transact-sql&#41;&#40;할당 취소](/sql/t-sql/language-elements/deallocate-transact-sql)   
 [Transact-sql&#41;&#40;커서를 선언 합니다.](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [FETCH &#40;Transact-sql&#41;](/sql/t-sql/language-elements/fetch-transact-sql)   
 [OPEN&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/open-transact-sql)  
  
  
