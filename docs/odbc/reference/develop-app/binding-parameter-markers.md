---
title: "바인딩 매개 변수 표식을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea1c1ecd676c7a496f7856f0eb0b22b003183407
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="binding-parameter-markers"></a>바인딩 매개 변수 표식
응용 프로그램 호출 하 여 매개 변수를 바인딩할 **SQLBindParameter**합니다. **SQLBindParameter** 한 번에 하나의 매개 변수를 바인딩합니다. 응용 프로그램이 다음을 지정합니다.  
  
-   매개 변수 수입니다. 매개 변수 번호 1부터 시작 하는 SQL 문에서 증가 매개 변수 순서 대로 번호가 매겨집니다. 큰 매개 변수 값을 지정 하는 동안 SQL 문의 매개 변수 개수 보다 매개 변수 값은 무시 됩니다는 문이 실행 될 때입니다.  
  
-   매개 변수 형식 (입력, 입/출력 또는 출력)입니다. 프로시저 호출에 매개 변수를 제외한 모든 매개 변수는 입력된 매개 변수를 사용 합니다. 자세한 내용은 참조 [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
-   변수의 C 데이터 형식, 주소 및 바이트 길이 매개 변수에 바인딩됩니다. 드라이버는 SQL 데이터 형식에 C 데이터 형식에서 데이터를 변환할 수 있어야 합니다. 또는 오류가 반환 됩니다. 목록이 지원 되는 변환에 대 한 참조 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 부록 d: 데이터 형식에서입니다.  
  
-   SQL 데이터 형식, 정밀도 및 매개 변수 자체의 소수 자릿수입니다.  
  
-   길이/표시기 버퍼의 주소입니다. 이진 또는 문자 데이터의 바이트 길이 제공 것 데이터가 NULL을 지정 하거나 지정 된 데이터를 전송 됩니다 **SQLPutData**합니다. 자세한 내용은 참조 [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)합니다.  
  
 예를 들어 다음 코드 바인딩 *판매원* 및 *CustID* 영업 사원 및 CustID 열에 대 한 매개 변수를 합니다. 때문에 *판매원* 는 가변 길이 문자 데이터를 포함 코드의 바이트 길이 지정 합니다. *판매원* (11) 바인딩합니다 *SalesPersonLenOrInd* 를 에 있는 데이터의 바이트 길이 포함 *판매원*합니다. 이 정보에 대 한 필요 하지 않습니다. *CustID* 고정 길이의 인 정수 데이터를 포함 하므로 합니다.  
  
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
  
 때 **SQLBindParameter** 은 호출 드라이버가이 정보에에서 저장 된 문에 대 한 구조입니다. 문이 실행 될 때 매개 변수 데이터 검색 및 데이터 원본에 보내는 정보를 사용 합니다.  
  
> [!NOTE]  
>  ODBC 1.0에서 매개 변수를 바인딩된 **SQLSetParam**합니다. 드라이버 관리자 간의 호출을 매핑하 **SQLSetParam** 및 **SQLBindParameter**응용 프로그램 및 드라이버에서 사용 하는 ODBC의 버전에 따라 합니다.
