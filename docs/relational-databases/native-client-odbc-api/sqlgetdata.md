---
description: SQLGetData
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 68d230ed9696188ea0ff1c3aee1ab16007494984
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810572"
---
# <a name="sqlgetdata"></a>SQLGetData
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLGetData** 는 열 값을 바인딩하지 않고 결과 집합 데이터를 검색하는 데 사용됩니다. 동일한 열에서**SQLGetData** 를 연속해서 호출하여 **text**, **ntext**또는 **image** 데이터 형식 열에서 많은 양의 데이터를 검색할 수 있습니다.  
  
 애플리케이션이 결과 집합 데이터를 인출하기 위해 변수를 바인딩해야 하는 요구 사항은 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLGetData **를 사용하여**Native Client ODBC 드라이버에서 모든 열의 데이터를 검색할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 임의의 열 순서로 데이터를 검색하기 위한 **SQLGetData** 사용을 지원하지 않습니다. **SQLGetData** 를 사용하여 처리된, 바인딩되지 않은 모든 열은 결과 집합의 바인딩된 열보다 높은 열 서수를 가져야 합니다. 애플리케이션은 바인딩되지 않은 가장 낮은 서수 열 값에서 가장 높은 서수 열 값으로 데이터를 처리해야 합니다. 서수 번호가 더 낮은 열의 데이터를 검색하려고 하면 오류가 발생합니다. 애플리케이션에서 서버 커서를 사용하여 결과 집합 행을 보고하는 경우 현재 행을 다시 인출한 다음 열 값을 인출할 수 있습니다. 읽기 전용, 정방향 전용 기본 커서에서 문이 실행된 경우 해당 문을 다시 실행하여 **SQLGetData**를 백업해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 **SQLGetData**를 사용하여 검색된 **text**, **ntext** 및 **image**데이터의 길이를 정확하게 보고합니다. 애플리케이션은 *StrLen_or_IndPtr* 매개 변수 반환 값을 이용하여 긴 데이터를 신속하게 검색할 수 있습니다.  
  
> [!NOTE]  
>  큰 값 형식에 대해 *StrLen_or_IndPtr* 은 데이터 잘림이 발생할 경우 SQL_NO_TOTAL을 반환합니다.  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetData 지원  
 날짜/시간 형식의 결과 열 값은 [SQL에서 C로 변환](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)에 설명 된 대로 변환 됩니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetData 지원  
 **SQLGetData** 는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetData 함수](../../odbc/reference/syntax/sqlgetdata-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
