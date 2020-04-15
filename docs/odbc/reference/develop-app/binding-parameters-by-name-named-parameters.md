---
title: 이름으로 바인딩 매개 변수 (명명 된 매개 변수) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306374"
---
# <a name="binding-parameters-by-name-named-parameters"></a>이름으로 매개 변수 바인딩(명명된 매개 변수)
특정 DBMS를 사용하면 응용 프로그램이 프로시저 호출의 위치가 아닌 이름으로 매개 변수를 저장 프로시저에 지정할 수 있습니다. 이러한 매개 변수를 *명명된 매개 변수라고 합니다.* ODBC는 명명된 매개 변수의 사용을 지원합니다. ODBC에서 명명된 매개 변수는 저장 프로시저 호출에서만 사용되며 다른 SQL 문에서는 사용할 수 없습니다.  
  
 드라이버는 IPD의 SQL_DESC_UNNAMED 필드의 값을 확인하여 명명된 매개 변수가 사용되는지 여부를 확인합니다. SQL_DESC_UNNAMED SQL_UNNAMED 설정되지 않은 경우 드라이버는 IPD의 SQL_DESC_NAME 필드의 이름을 사용하여 매개 변수를 식별합니다. 매개 변수를 바인딩하기 위해 응용 프로그램은 **SQLBindParameter를** 호출하여 매개 변수 정보를 지정한 다음 **SQLSetDescField를** 호출하여 IPD의 SQL_DESC_NAME 필드를 설정할 수 있습니다. 명명된 매개 변수를 사용하는 경우 프로시저 호출의 매개 변수 순서는 중요하지 않으며 매개 변수의 레코드 번호는 무시됩니다.  
  
 명명되지 않은 매개 변수와 명명된 매개 변수의 차이는 설명자의 레코드 번호와 프로시저의 매개 변수 번호 간의 관계에 있습니다. 명명되지 않은 매개 변수를 사용하는 경우 첫 번째 매개 변수 마커는 매개 변수 설명자의 첫 번째 레코드와 관련이 있으며, 이 레코드는 프로시저 호출의 첫 번째 매개 변수(생성 순서)와 관련이 있습니다. 명명된 매개 변수를 사용하는 경우 첫 번째 매개 변수 마커는 여전히 매개 변수 설명자의 첫 번째 레코드와 관련이 있지만 설명자의 레코드 번호와 프로시저의 매개 변수 번호 간의 관계는 더 이상 존재하지 않습니다. 명명된 매개변수는 설명자 레코드 번호의 매핑을 프로시저 매개 변수 위치에 사용하지 않습니다. 대신 설명자 레코드 이름이 프로시저 매개 변수 이름에 매핑됩니다.  
  
> [!NOTE]  
>  IPD의 자동 모집단이 활성화된 경우 드라이버는 설명자 레코드의 순서가 명명된 매개 변수가 사용되는 경우에도 프로시저 정의의 매개 변수 순서와 일치되도록 설명자를 채웁니다.  
  
 명명된 매개 변수가 사용되는 경우 모든 매개 변수의 이름을 매개 변수로 지정해야 합니다. 매개 변수가 명명된 매개 변수가 아닌 경우 매개 변수 ca의 이름이 지정되지 않습니다. 명명된 매개 변수와 명명되지 않은 매개 변수가 혼합된 경우 동작은 드라이버에 따라 다릅니다.  
  
 명명된 매개 변수의 예로 SQL Server 저장 프로시저가 다음과 같이 정의되었다고 가정합니다.  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 이 절차에서 첫 번째 @title_id매개 변수는 기본값이 1입니다. 응용 프로그램은 다음 코드를 사용하여 하나의 동적 매개 변수만 지정하도록 이 프로시저를 호출할 수 있습니다. 이 매개 변수는 "quote"라는\@이름의 매개 변수입니다.  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
