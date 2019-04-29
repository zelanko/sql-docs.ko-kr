---
title: SQLGetDescField | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 410aec64f1a10f8deaf7923fedda8b79c114eef3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014492"
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 IRD(구현 행 설명자) 전용의 드라이버별 설명자 필드를 노출합니다. IRD 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설명자 필드는 드라이버별 열 특성을 통해 참조됩니다. 사용 가능한 드라이버별 설명자 필드의 전체 목록에 대한 자세한 내용은 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)를 참조하십시오.  
  
 열 식별자 문자열이 포함된 설명자 필드는 대체로 길이가 0인 문자열입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]관련 설명자 필드 값은 모두 읽기 전용입니다.  
  
 특성이 같은 보고서 행 수준 특성 (예: SQL_CA_SS_COMPUTE_ID) 결과 집합의 모든 열에 대해 보고 되는 설명자 필드 SQLColAttribute를 사용 하 여 검색 합니다.  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField 및 테이블 반환 매개 변수  
 SQLGetDescField는 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열의 확장된 특성에 대 한 값을 가져오는 데 사용할 수 있습니다. 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetDescField 지원  
 새로운 날짜/시간 형식에 사용할 수 있는 설명자 필드에 대한 자세한 내용은 [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)를 참조하십시오.  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], SQLGetDescField 반환할 수 있습니다 **SQL_C_SS_TIME2** (에 대 한 **시간** 형식) 또는 **SQL_C_SS_TIMESTAMPOFFSET** (에 대 한  **datetimeoffset**) 대신 **SQL_C_BINARY**응용 프로그램에서 ODBC 3.8을 사용 하는 경우.  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetDescField 지원  
 **SQLGetDescField** 는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>스파스 열에 대한 SQLGetDescField 지원  
 SQLGetDescField 새로운 IRD 필드인 SQL_CA_SS_IS_COLUMN_SET 열 인지 확인 하려면 쿼리를 사용할 수는 **column_set** 열입니다.  
  
 자세한 내용은 [Sparse Columns Support &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)합니다.  
  
## <a name="example"></a>예제  
  
```  
typedef struct tagCOMPUTEBYLIST  
    {  
    SQLSMALLINT nBys;  
    SQLSMALLINT aByList[1];  
    } COMPUTEBYLIST;  
typedef COMPUTEBYLIST* PCOMPUTEBYLIST;   
  
SQLHDESC    hIRD;   
SQLINTEGER  cbIRD;   
SQLINTEGER  nSet = 0;   
  
// . . .  
// Execute a statement that contains a COMPUTE clause,  
//  then get the descriptor handle of the IRD and  
//  get some IRD values.  
  
SQLGetStmtAttr(g_hStmt, SQL_ATTR_IMP_ROW_DESC,  
    (SQLPOINTER) &hIRD, sizeof(SQLHDESC), &cbIRD);  
  
// For statement-wide column attributes, any  
//  descriptor record will do. You know that 1 exists,  
//  so use it.  
SQLGetDescField(hIRD, 1, SQL_CA_SS_NUM_COMPUTES,  
    (SQLPOINTER) &nComputes, SQL_IS_INTEGER, &cbIRD);  
  
if (nSet == 0)  
    {  
    SQLINTEGER      nOrderID;  
  
    printf_s("Normal result set.\n");  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ORDER,  
            (SQLPOINTER) &nOrderID, SQL_IS_INTEGER,  
            &cbIRD);  
  
        if (nOrderID != 0)  
            {  
            printf_s("Col in ORDER BY, pos: %ld",  
                nOrderID);  
            }  
            printf_s("\n");  
        }  
  
    printf_s("\n");  
    }  
else  
    {  
    PCOMPUTEBYLIST  pByList;  
    SQLSMALLINT     nBy;  
    SQLINTEGER      nColID;  
  
    printf_s("Computed result set number: %lu\n",  
        nSet);  
  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_BYLIST,  
        (SQLPOINTER) &pByList, SQL_IS_INTEGER,  
        &cbIRD);  
  
    if (pByList != NULL)  
        {  
        printf_s("Clause ordered by columns: ");  
        for (nBy = 0; nBy < pByList->nBys; )  
            {  
            printf_s("%u", pByList->aByList[nBy]);  
            nBy++;  
  
            if (nBy == pByList->nBys)  
                {  
                printf_s("\n");  
                }  
            else  
                {  
                printf_s(", ");  
                }  
            }  
        }  
    else  
        {  
        printf_s("Compute clause set not ordered.\n");  
        }  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ID, (SQLPOINTER) &nColID,  
            SQL_IS_INTEGER, &cbIRD);  
        printf_s("ColumnID: %lu, nColID);  
        }  
    printf_s("\n");  
    }  
  
if (SQLMoreResults(g_hStmt) == SQL_SUCCESS)  
    {  
    // Determine the result set indicator.  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_ID,  
        (SQLPOINTER) &nSet, SQL_IS_INTEGER, &cbIRD);  
    }  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQLGetDescField 함수](https://go.microsoft.com/fwlink/?LinkId=59351)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
