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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be99bc884a8baa66f3d632ee4731985f0cc85732
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306394"
---
# <a name="binding-parameter-markers"></a>바인딩 매개 변수 표식
응용 프로그램은 **SQLBindParameter**를 호출 하 여 매개 변수를 바인딩합니다. **SQLBindParameter** 는 한 번에 하나의 매개 변수를 바인딩합니다. 응용 프로그램은 다음을 지정 합니다.  
  
-   매개 변수 번호입니다. 매개 변수의 번호는 1부터 시작 하 여 SQL 문에서 매개 변수 순서를 늘립니다. SQL 문의 매개 변수 개수 보다 높은 매개 변수 번호를 지정 하는 것은 올바르지만 문이 실행 될 때 매개 변수 값이 무시 됩니다.  
  
-   매개 변수 형식 (입력, 입/출력 또는 출력)입니다. 프로시저 호출의 매개 변수를 제외 하 고 모든 매개 변수는 입력 매개 변수입니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)를 참조 하세요.  
  
-   매개 변수에 바인딩된 변수의 C 데이터 형식, 주소 및 바이트 길이입니다. 드라이버는 데이터를 C 데이터 형식에서 SQL 데이터 형식으로 변환할 수 있어야 합니다. 그렇지 않으면 오류가 반환 됩니다. 지원 되는 변환 목록은 부록 D: 데이터 형식에서 데이터 [를 C에서 SQL 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 을 참조 하세요.  
  
-   매개 변수 자체의 SQL 데이터 형식, 전체 자릿수 및 소수 자릿수입니다.  
  
-   길이/표시기 버퍼의 주소입니다. 이진 또는 문자 데이터의 바이트 길이를 제공 하 고, 데이터를 NULL로 지정 하거나, **Sqlputdata**를 사용 하 여 데이터를 보내도록 지정 합니다. 자세한 내용은 [길이/표시기 값 사용](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)을 참조 하세요.  
  
 예를 들어 다음 코드는 판매원 및 *CustID* 을 영업 사원의 및 CustID 열에 대 한 매개 *변수에 바인딩합니다.* *판매 직원* 은 가변 길이인 문자 데이터를 포함 하기 때문에 코드에서 *판매 직원* 의 바이트 길이 (11)를 지정 하 고 *SalesPersonLenOrInd* 를 바인딩하여 *판매 직원*의 데이터 바이트 길이를 포함 합니다. 이 정보는 고정 길이인 정수 데이터를 포함 하기 때문에 *CustID* 에 필요 하지 않습니다.  
  
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
  
 **SQLBindParameter** 가 호출 되 면 드라이버는이 정보를 문의 구조에 저장 합니다. 문이 실행 될 때이 정보를 사용 하 여 매개 변수 데이터를 검색 하 고 데이터 원본에 보냅니다.  
  
> [!NOTE]  
>  ODBC 1.0에서 매개 변수는 **SQLSetParam**를 사용 하 여 바인딩 되었습니다. 드라이버 관리자는 응용 프로그램 및 드라이버에서 사용 하는 ODBC 버전에 따라 **SQLSetParam** 와 **SQLBindParameter**간의 호출을 매핑합니다.
