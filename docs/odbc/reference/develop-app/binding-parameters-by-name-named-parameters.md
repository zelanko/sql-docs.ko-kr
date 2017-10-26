---
title: "바인딩 매개 변수 이름 (명명 된 매개 변수)으로 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b3047d17ff1e9785e203b6be0ab48c7c27fd88d1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="binding-parameters-by-name-named-parameters"></a>바인딩 (명명 된 매개 변수) 이름으로 매개 변수
특정 Dbms 프로시저 호출에서 위치에 따라이 대신 이름으로 저장된 프로시저에 매개 변수를 지정 하는 응용 프로그램을 허용 합니다. 이러한 매개 변수가 호출 *명명 된 매개 변수*합니다. ODBC는 명명 된 매개 변수 사용을 지원합니다. Odbc에서 명명 된 매개 변수 저장된 프로시저에 대 한 호출에만 사용 되 고 다른 SQL 문에서 사용할 수 없습니다.  
  
 드라이버는 지 여부를 결정 명명 된 매개 변수를 사용 IPD의 SQL_DESC_UNNAMED 필드의 값을 확인 합니다. SQL_DESC_UNNAMED 하면으로 설정 되지 않은, 드라이버는 매개 변수를 식별 하는 이름을 IPD의 SQL_DESC_NAME 필드에 사용 합니다. 응용 프로그램 호출 수 매개 변수를 바인딩하려면 **SQLBindParameter** 를 매개 변수 정보를 지정 하 고 그런 후 호출할 수 **SQLSetDescField** 는 IPD의 SQL_DESC_NAME 필드를 설정 하 합니다. 명명 된 매개 변수를 사용 하는 프로시저 호출에서 매개 변수 순서가 중요 하 고 매개 변수의 레코드 번호 무시 됩니다.  
  
 명명 되지 않은 매개 변수 및 명명 된 매개 변수 간의 차이점은 설명자 레코드 수와 프로시저에서 매개 변수 번호 간의 관계입니다. 이름 없는 매개 변수를 사용 하는 첫 번째 매개 변수 표식에 다시 연결 되는 순서에 따라 생성 프로시저 호출에 첫 번째 매개 변수에 매개 변수 설명자의 첫 번째 레코드 관련이 있습니다. 명명 된 매개 변수를 사용 하는 첫 번째 매개 변수 표식 앞에 여전히 매개 변수 설명자의 첫 번째 레코드 관련이 있지만 설명자 레코드 수와 프로시저에서 매개 변수 번호 간의 관계는 더 이상 존재 하지 않습니다. 명명 된 매개 변수 설명자 레코드 번호의 매핑을 프로시저 매개 변수 위치; 사용 하지 않는 대신, 설명자 레코드 이름은 프로시저 매개 변수 이름에 매핑됩니다.  
  
> [!NOTE]  
>  IPD의 자동 채우기를 사용 하는 경우 드라이버가 채워집니다 설명자를 설명자 레코드의 순서는 프로시저 정의에서 매개 변수의 순서 일치시킬지 되도록 명명 된 매개 변수를 사용 하는 경우에 합니다.  
  
 명명된 된 매개 변수를 사용 하는 경우 모든 매개 변수 이름을 지정 해야 매개 변수입니다. 매개 변수 명명된 된 매개 변수 없는 경우 매개 변수 이름을 지정할 매개 변수 ca의 없음. 명명 된 매개 변수 및 명명 되지 않은 매개 변수 혼합 되었으면 동작 드라이버 종속적 것입니다.  
  
 명명 된 매개 변수의 예를 들어 다음과 같이 정의 된 저장된 프로시저는 SQL Server 가정 합니다.  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 이 절차에서는 첫 번째 매개 변수 @title_id의 기본 값은 1입니다. 응용 프로그램 동적 매개 변수를 하나만 지정 되도록이 프로시저를 호출 하려면 다음 코드를 사용할 수 있습니다. 이 매개 변수는 명명된 된 매개 변수 이름으로 "@quote"입니다.  
  
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

