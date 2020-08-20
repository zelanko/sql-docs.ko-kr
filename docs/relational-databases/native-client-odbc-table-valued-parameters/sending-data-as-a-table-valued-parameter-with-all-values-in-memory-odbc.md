---
description: 모든 값을 메모리에 로드하여 테이블 반환 매개 변수로 데이터 전송(ODBC)
title: 테이블 반환 매개 변수, 메모리의 값 (ODBC)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), sending data to a stored procedure with all values in memory
ms.assetid: 8b96282f-00d5-4e28-8111-0a87ae6d7781
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 676d0c40ca7c064945284d5a486ec0cda698688d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499086"
---
# <a name="sending-data-as-a-table-valued-parameter-with-all-values-in-memory-odbc"></a>모든 값을 메모리에 로드하여 테이블 반환 매개 변수로 데이터 전송(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 항목에서는 모든 값이 메모리에 있을 때 데이터를 테이블 반환 매개 변수로 저장 프로시저에 보내는 방법에 대해 설명합니다. 테이블 반환 매개 변수를 보여 주는 다른 예제는 [ODBC&#41;&#40;테이블 반환 매개 변수 사용 ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)을 참조 하세요.  
  
## <a name="prerequisite"></a>필수 조건  
 이 절차에서는 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]이 서버에서 실행되었다고 가정합니다.  
  
```sql
create type TVParam as table(ProdCode integer, Qty integer)  
create procedure TVPOrderEntry(@CustCode varchar(5), @Items TVPParam,   
            @OrdNo integer output, @OrdDate datetime output)  
         as   
         set @OrdDate = GETDATE();  
         insert into TVPOrd (OrdDate, CustCode)   
values (@OrdDate, @CustCode) output OrdNo);   
         select @OrdNo = SCOPE_IDENTITY();   
         insert into TVPItem (OrdNo, ProdCode, Qty)  
select @OrdNo, @Items.ProdCode, @Items.Qty   
from @Items  
```  
  
## <a name="to-send-the-data"></a>데이터를 전송하려면  
  
1.  SQL 매개 변수의 변수를 선언합니다. 이 경우 테이블 값 전체가 메모리에 포함되므로 테이블 값의 열 값이 배열로 선언됩니다.  
  
    ```cpp
    SQLRETURN r;  
    // Variables for SQL parameters.  
    #define ITEM_ARRAY_SIZE 20  
  
    SQLCHAR CustCode[6];  
    SQLCHAR *TVP = (SQLCHAR *) "TVParam";  
    SQLINTEGER ProdCode[ITEM_ARRAY_SIZE], Qty[ITEM_ARRAY_SIZE];  
    SQLINTEGER OrdNo;  
    char OrdDate[23];  
  
    // Variables for indicator/length variables associated with parameters.  
    SQLLEN cbCustCode, cbTVP, cbProdCode[ITEM_ARRAY_SIZE], cbQty[ITEM_ARRAY_SIZE], cbOrdNo, cbOrdDate;  
    ```  
  
2.  매개 변수를 바인딩합니다. 테이블 반환 매개 변수가 사용될 경우 매개 변수를 바인딩하는 과정은 두 단계로 구성됩니다. 첫 번째 단계에서는 저장 프로시저의 단계 매개 변수가 다음과 같은 일반적인 방법으로 바인딩됩니다.  
  
    ```cpp
    // Bind parameters for call to TVPOrderEntryDirect.  
    // 1 - Custcode input  
    r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT,SQL_VARCHAR, SQL_C_CHAR, 5, 0, CustCode, sizeof(CustCode), &cbCustCode);  
  
    // 2 - Items TVP  
    r = SQLBindParameter(hstmt,   
        2,// ParameterNumber  
        SQL_PARAM_INPUT,// InputOutputType  
        SQL_C_DEFAULT,// ValueType   
        SQL_SS_TABLE,// Parametertype  
        ITEM_ARRAY_SIZE,// ColumnSize: For a table-valued parameter this is the row array size.  
        0,// DecimalDigits: For a table-valued parameter this is always 0.   
        TVP,// ParameterValuePtr: For a table-valued parameter this is the type name of the   
    //table-valued parameter, and also a token returned by SQLParamData.  
        SQL_NTS,// BufferLength: For a table-valued parameter this is the length of the type name or SQL_NTS.  
        &cbTVP);// StrLen_or_IndPtr: For a table-valued parameter this is the number of rows actually used.  
  
    // 3 - OrdNo output  
    r = SQLBindParameter(hstmt, 3, SQL_PARAM_OUTPUT,SQL_INTEGER, SQL_C_LONG, 0, 0, &OrdNo,  
       sizeof(SQLINTEGER), &cbOrdNo);  
    // 4 - OrdDate output  
    r = SQLBindParameter(hstmt, 4, SQL_PARAM_OUTPUT,SQL_TYPE_TIMESTAMP, SQL_C_CHAR, 23, 3, &OrdDate,   
       sizeof(OrdDate), &cbOrdDate);  
    ```  
  
3.  매개 변수를 바인딩하는 두 번째 단계에서는 테이블 반환 매개 변수의 열이 바인딩됩니다. 먼저 매개 변수 포커스가 테이블 반환 매개 변수의 서수로 설정됩니다. 그런 다음 테이블 값의 열은 저장 프로시저의 매개 변수 이지만 ParameterNumber의 열 서 수를 사용 하는 경우와 동일한 방식으로 SQLBindParameter를 사용 하 여 바인딩됩니다. 테이블 값 매개 변수가 더 있으면 포커스를 각 매개 변수에 차례로 설정하고 해당 열을 바인딩합니다. 마지막으로 매개 변수 포커스가 0으로 다시 설정됩니다.  
  
    ```cpp
    // Bind columns for the table-valued parameter (param 2).  
    // First set focus on param 2.  
    r = SQLSetStmtAttr(hstmt, SQL_SOPT_SS_PARAM_FOCUS, (SQLPOINTER) 2, SQL_IS_INTEGER);  
  
    // Col 1 - ProdCode  
    r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT,SQL_INTEGER, SQL_C_LONG, 0, 0, ProdCode, sizeof(SQLINTEGER), cbProdCode);  
    // Col 2 - Qty  
    r = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT,SQL_INTEGER, SQL_C_LONG, 0, 0, Qty, sizeof(SQLINTEGER), cbQty);  
  
    // Reset param focus.  
    r = SQLSetStmtAttr(hstmt, SQL_SOPT_SS_PARAM_FOCUS, (SQLPOINTER) 0, SQL_IS_INTEGER);  
    ```  
  
4.  매개 변수 버퍼를 채웁니다. `cbTVP`는 서버에 전송할 행 수로 설정됩니다.  
  
    ```cpp
    // Populate parameters.  
    cbTVP = 0; // Number of rows available for input.  
    strcpy_s((char *) CustCode, sizeof(CustCode), "CUST1"); cbCustCode = SQL_NTS;  
  
    ProdCode[cbTVP] = 1215;cbProdCode[cbTVP] = sizeof(SQLINTEGER);   
    Qty[cbTVP] = 5;cbQty[cbTVP] = sizeof(SQLINTEGER);   
    cbTVP++; // Number of rows available for input  
  
    ProdCode[cbTVP] = 1017;cbProdCode[cbTVP] = sizeof(SQLINTEGER);   
    Qty[cbTVP] = 2;cbQty[cbTVP] = sizeof(SQLINTEGER);   
    cbTVP++; // Number of rows available for input.  
    ```  
  
5.  다음과 같이 프로시저를 호출합니다.  

    ```cpp
    // Call the procedure.  
    r = SQLExecDirect(hstmt, (SQLCHAR *) "{call TVPOrderEntry(?, ?, ?, ?)}",SQL_NTS);  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 테이블 반환 매개 변수 프로그래밍 예제](https://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
  
  
