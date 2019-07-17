---
title: 바인딩 (명명 된 매개 변수) 이름으로 매개 변수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3fdd8d00bd6af5479079e66c1ca42f249e033d29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107638"
---
# <a name="binding-parameters-by-name-named-parameters"></a>이름으로 매개 변수 바인딩(명명된 매개 변수)
특정 Dbms 프로시저 호출에서 위치에 따라 대신 이름으로 저장된 프로시저에 매개 변수를 지정 하는 응용 프로그램을 허용 합니다. 이러한 매개 변수 라고 *명명 된 매개 변수*합니다. ODBC는 명명 된 매개 변수 사용을 지원합니다. Odbc에서 명명 된 매개 변수는 저장된 프로시저에 대 한 호출 에서만 사용 되며 및 다른 SQL 문에서 사용할 수 없습니다.  
  
 드라이버는 매개 변수 라는 여부를 확인 하려면 IPD의 SQL_DESC_UNNAMED 필드의 값을 확인 합니다. SQL_DESC_UNNAMED를 하면을 설정 하지 않으면 드라이버는 매개 변수를 식별 하는 이름을 IPD의 SQL_DESC_NAME 필드에 사용 합니다. 매개 변수를 바인딩하는 응용 프로그램이 호출할 수 **SQLBindParameter** 에 매개 변수 정보를 지정 하 고 다음 호출할 수 있습니다 **SQLSetDescField** IPD의 SQL_DESC_NAME 필드를 설정할 수 있습니다. 명명 된 매개 변수를 사용 하는 프로시저 호출에서 매개 변수의 순서가 중요 하 고 매개 변수의 레코드 번호 무시 됩니다.  
  
 설명자의 레코드 수와 프로시저의 매개 변수 번호 간의 관계는 명명 되지 않은 매개 변수 및 명명 된 매개 변수 간에 다릅니다. 명명 되지 않은 매개 변수를 사용 하는 첫 번째 매개 변수 표식은 프로시저 호출에서 생성 순서상에서 첫 번째 매개 변수에 연결 되는 매개 변수 설명자의 첫 번째 레코드는 관련이 있습니다. 명명 된 매개 변수를 사용 하는 첫 번째 매개 변수 표식을 첫 번째 매개 변수 설명자 레코드를 여전히 관련이 있지만 설명자의 레코드 수와 프로시저의 매개 변수 번호 간의 관계는 더 이상 존재 하지 않습니다. 프로시저 매개 변수 위치; 명명 된 매개 변수 설명자 레코드 번호 매핑의 사용 하지 마십시오 대신, 설명자 레코드 이름은 프로시저 매개 변수 이름에 매핑됩니다.  
  
> [!NOTE]  
>  IPD의 자동 채우기를 사용 하는 경우 드라이버가 채워집니다 설명자를 설명자 레코드의 순서에는 프로시저 정의에서 매개 변수의 순서와 일치는 명명 된 매개 변수를 사용 하는 경우에 합니다.  
  
 명명된 된 매개 변수를 사용 하는 경우 모든 매개 변수 이름은 매개 변수입니다. 매개 변수 명명된 된 매개 변수 없는 경우 다음 매개 변수 ca 하나도 될 명명 된 매개 변수입니다. 명명 된 매개 변수 및 명명 되지 않은 매개 변수 혼합 된 경우에 드라이버에 따라 다릅니다 동작을 것입니다.  
  
 명명 된 매개 변수의 예를 들어, 다음과 같이 정의 된 저장된 프로시저는 SQL Server를 가정 합니다.  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 첫 번째 매개 변수를이 절차에서는 @title_id의 기본 값은 1입니다. 응용 프로그램 하나만 동적 매개 변수를 지정 하는이 프로시저를 호출 하는 다음 코드를 사용할 수 있습니다. 이 매개 변수 이름 사용 하 여 명명된 된 매개 변수는 "\@따옴표"입니다.  
  
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
