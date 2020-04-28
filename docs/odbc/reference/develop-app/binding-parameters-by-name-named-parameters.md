---
title: 이름으로 매개 변수 바인딩 (명명 된 매개 변수) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306374"
---
# <a name="binding-parameters-by-name-named-parameters"></a>이름으로 매개 변수 바인딩(명명된 매개 변수)
응용 프로그램에서는 특정 Dbms를 사용 하 여 프로시저 호출에서 위치가 아닌 이름으로 저장 프로시저에 대 한 매개 변수를 지정할 수 있습니다. 이러한 매개 변수를 *명명 된 매개 변수*라고 합니다. ODBC에서는 명명 된 매개 변수를 사용할 수 있습니다. ODBC에서 명명 된 매개 변수는 저장 프로시저에 대 한 호출에만 사용 되며 다른 SQL 문에서 사용할 수 없습니다.  
  
 드라이버는 IPD의 SQL_DESC_UNNAMED 필드 값을 확인 하 여 명명 된 매개 변수가 사용 되는지 여부를 확인 합니다. SQL_DESC_UNNAMED을 SQL_UNNAMED로 설정 하지 않은 경우 드라이버는 IPD의 SQL_DESC_NAME 필드에 있는 이름을 사용 하 여 매개 변수를 식별 합니다. 매개 변수를 바인딩하기 위해 응용 프로그램은 **SQLBindParameter** 를 호출 하 여 매개 변수 정보를 지정한 다음 **SQLSetDescField** 를 호출 하 여 IPD의 SQL_DESC_NAME 필드를 설정할 수 있습니다. 명명 된 매개 변수를 사용 하는 경우 프로시저 호출에서 매개 변수의 순서가 중요 하지 않으며 매개 변수의 레코드 번호가 무시 됩니다.  
  
 명명 되지 않은 매개 변수와 명명 된 매개 변수의 차이점은 설명자의 레코드 번호와 프로시저의 매개 변수 번호 간의 관계에 있습니다. 명명 되지 않은 매개 변수를 사용 하는 경우 첫 번째 매개 변수 표식은 매개 변수 설명자의 첫 번째 레코드와 관련 되어 있으며,이는 차례로 프로시저 호출의 첫 번째 매개 변수 (생성 순서)와 관련이 있습니다. 명명 된 매개 변수를 사용 하는 경우 첫 번째 매개 변수 표식은 여전히 매개 변수 설명자의 첫 번째 레코드와 관련 되어 있지만 설명자의 레코드 번호와 프로시저의 매개 변수 번호 간 관계는 더 이상 존재 하지 않습니다. 명명 된 매개 변수는 설명자 레코드 번호를 프로시저 매개 변수 위치에 매핑하는 데 사용 하지 않습니다. 대신 설명자 레코드 이름이 프로시저 매개 변수 이름에 매핑됩니다.  
  
> [!NOTE]  
>  IPD 자동 채우기를 사용 하는 경우 명명 된 매개 변수가 사용 되는 경우에도 설명자 레코드의 순서가 프로시저 정의의 매개 변수 순서와 일치 하도록 설명자를 채웁니다.  
  
 명명 된 매개 변수를 사용 하는 경우 모든 매개 변수는 명명 된 매개 변수 여야 합니다. 매개 변수가 명명 된 매개 변수가 아니면 매개 변수 ca를 명명 된 매개 변수로 사용할 수 없습니다. 명명 된 매개 변수와 명명 되지 않은 매개 변수가 혼합 되어 있는 경우에는 해당 동작이 드라이버에 따라 달라 집니다.  
  
 명명 된 매개 변수의 예로, SQL Server 저장 프로시저가 다음과 같이 정의 되어 있다고 가정 합니다.  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 이 절차에서 첫 번째 매개 변수인 @title_id의 기본값은 1입니다. 응용 프로그램은 다음 코드를 사용 하 여 하나의 동적 매개 변수만 지정 하도록이 프로시저를 호출할 수 있습니다. 이 매개 변수는 이름이 "\@quote" 인 명명 된 매개 변수입니다.  
  
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
