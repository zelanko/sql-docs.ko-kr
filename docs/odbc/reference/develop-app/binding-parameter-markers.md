---
title: 바인딩 매개 변수 마커 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306394"
---
# <a name="binding-parameter-markers"></a>바인딩 매개 변수 표식
응용 프로그램은 **SQLBindParameter**를 호출하여 매개 변수를 바인딩합니다. **SQLBindParameter는** 한 번에 하나의 매개 변수를 바인딩합니다. 응용 프로그램은 다음을 지정합니다.  
  
-   매개 변수 번호입니다. 매개 변수는 숫자 1부터 시작하여 SQL 문의 증가매개 변수 순서로 번호가 매겨져 있습니다. SQL 문의 매개 변수 수보다 높은 매개 변수 번호를 지정하는 것은 합법적이지만 문이 실행될 때 매개 변수 값은 무시됩니다.  
  
-   매개 변수 유형(입력, 입력/출력 또는 출력)입니다. 프로시저 호출의 매개 변수를 제외하고 모든 매개 변수는 입력 매개 변수입니다. 자세한 내용은 [절차 매개 변수를](../../../odbc/reference/develop-app/procedure-parameters.md)참조하십시오.  
  
-   매개 변수에 바인딩된 변수의 C 데이터 형식, 주소 및 바이트 길이입니다. 드라이버는 C 데이터 형식의 데이터를 SQL 데이터 유형으로 변환할 수 있어야 하며 오류가 반환됩니다. 지원되는 변환 목록은 부록 D: 데이터 [형식의 C에서 SQL 데이터 유형으로 데이터 변환을](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 참조하세요.  
  
-   매개 변수 자체의 SQL 데이터 형식, 정밀도 및 배율입니다.  
  
-   길이/표시기 버퍼의 주소입니다. 이진 또는 문자 데이터의 바이트 길이를 제공하고, 데이터가 NULL임을 지정하거나, **데이터가 SQLPutData**로 전송되도록 지정합니다. 자세한 내용은 [길이/표시기 값 사용을](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)참조하십시오.  
  
 예를 들어 다음 코드는 *SalesPerson* 및 CustID 열에 대한 매개 변수에 SalesPerson 및 *CustID를* 바인딩합니다. *SalesPerson에는* 가변 길이인 문자 데이터가 포함되어 있으므로 코드는 SalesPerson(11)의 바이트 길이를 지정하고 *SalesPersonLenOrInd를* 바인딩하여 *SalesPerson에서*데이터의 바이트 길이를 포함합니다. *SalesPerson* 이 정보는 고정 길이의 정수 데이터를 포함하므로 *CustID에* 필요하지 않습니다.  
  
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
  
 **SQLBindParameter가** 호출되면 드라이버는 이 정보를 명령문의 구조에 저장합니다. 문이 실행되면 정보를 사용하여 매개 변수 데이터를 검색하고 데이터 원본으로 보냅니다.  
  
> [!NOTE]  
>  ODBC 1.0에서 매개 변수는 **SQLSetParam**. 드라이버 관리자는 응용 프로그램 및 드라이버에서 사용되는 ODBC 버전에 따라 **SQLSetParam과** **SQLBindParameter**간에 호출을 매핑합니다.
