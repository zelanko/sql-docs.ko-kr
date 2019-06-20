---
title: 바인딩 매개 변수 표식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c71967bd72f7f13a725d47517cb9e66eee7da87f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199397"
---
# <a name="binding-parameter-markers"></a>바인딩 매개 변수 표식
응용 프로그램 매개 변수를 호출 하 여 바인딩합니다 **SQLBindParameter**합니다. **SQLBindParameter** 한 번에 하나의 매개 변수를 바인딩합니다. 사용 하 여 응용 프로그램이 다음을 지정합니다.  
  
-   매개 변수 수입니다. 매개 변수는 숫자 1부터 SQL 문에서 증가 매개 변수 순서 대로 번호가 지정 됩니다. 큰 매개 변수 값을 지정할 수 있지만 SQL 문의 매개 변수 수보다 매개 변수 값은 무시 됩니다 문이 실행 된 경우.  
  
-   매개 변수 형식 (입력, 입/출력 또는 출력)입니다. 프로시저 호출에 매개 변수를 제외 하 고 모든 매개 변수는 입력된 매개 변수를 사용 합니다. 자세한 내용은 [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)이 섹션의 뒷부분에 나오는.  
  
-   변수의 C 데이터 유형, 주소 및 바이트 길이 매개 변수에 바인딩됩니다. 드라이버는 SQL 데이터 형식으로 C 데이터 형식에서 데이터를 변환할 수 있어야 합니다. 또는 오류가 반환 됩니다. 지원 되는 변환의 목록을 참조 하세요 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 d: 데이터 형식입니다.  
  
-   SQL 데이터 형식, 정밀도 및 매개 변수 자체의 확장입니다.  
  
-   길이/표시기 버퍼의 주소입니다. 바이트 길이의 이진 또는 문자 데이터를 제공 합니다.이 데이터는 NULL을 지정 또는 사용 하 여 데이터를 보내도록 지정 **SQLPutData**합니다. 자세한 내용은 [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)입니다.  
  
 예를 들어, 다음 코드를 바인딩합니다 *SalesPerson* 하 고 *CustID* 영업 사원 및 CustID 열에 대 한 매개 변수를 합니다. 때문에 *SalesPerson* 는 가변 길이 문자 데이터를 포함 코드의 바이트 길이 지정 *영업 직원* (11) 바인딩합니다 *SalesPersonLenOrInd* 를 에 있는 데이터의 바이트 길이 포함할 *SalesPerson*합니다. 이 정보에 대 한 필요는 없습니다 *CustID* 고정 길이 정수 데이터를 포함 하므로 합니다.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 때 **SQLBindParameter** 는 호출 드라이버의에서 정보가 포함이 문에 대 한 구조입니다. 문이 실행 될 때 매개 변수 데이터를 검색 하 여 데이터 원본에 보내는 정보를 사용 합니다.  
  
> [!NOTE]  
>  ODBC 1.0에서 사용 하 여 매개 변수가 바인딩된 **SQLSetParam**합니다. 드라이버 관리자 간의 호출을 매핑합니다 **SQLSetParam** 하 고 **SQLBindParameter**응용 프로그램 및 드라이버에서 사용 하는 ODBC의 버전에 따라 합니다.
