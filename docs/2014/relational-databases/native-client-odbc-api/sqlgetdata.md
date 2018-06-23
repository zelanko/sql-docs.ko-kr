---
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 370f018ad22dcdcfa1229a9a5b89fd2e2b9b27df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173114"
---
# <a name="sqlgetdata"></a>SQLGetData
  **SQLGetData** 는 열 값을 바인딩하지 않고 결과 집합 데이터를 검색하는 데 사용됩니다. 동일한 열에서**SQLGetData** 를 연속해서 호출하여 **text**, **ntext**또는 **image** 데이터 형식 열에서 많은 양의 데이터를 검색할 수 있습니다.  
  
 응용 프로그램이 결과 집합 데이터를 인출하기 위해 변수를 바인딩해야 하는 요구 사항은 없습니다. 모든 열의 데이터를 검색할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용 하 여 **SQLGetData**합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용 하 여 지원 하지 않습니다 **SQLGetData** 임의의 열 순서로 데이터를 검색 합니다. **SQLGetData** 를 사용하여 처리된, 바인딩되지 않은 모든 열은 결과 집합의 바인딩된 열보다 높은 열 서수를 가져야 합니다. 응용 프로그램은 바인딩되지 않은 가장 낮은 서수 열 값에서 가장 높은 서수 열 값으로 데이터를 처리해야 합니다. 서수 번호가 더 낮은 열의 데이터를 검색하려고 하면 오류가 발생합니다. 응용 프로그램에서 서버 커서를 사용하여 결과 집합 행을 보고하는 경우 현재 행을 다시 인출한 다음 열 값을 인출할 수 있습니다. 읽기 전용, 정방향 전용 기본 커서에서 문이 실행된 경우 해당 문을 다시 실행하여 **SQLGetData**를 백업해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 길이 정확 하 게 보고 **텍스트**, **ntext**, 및 **이미지** 데이터를 사용 하 여 검색 **SQLGetData** . 응용 프로그램은 *StrLen_or_IndPtr* 매개 변수 반환 값을 이용하여 긴 데이터를 신속하게 검색할 수 있습니다.  
  
> [!NOTE]  
>  큰 값 형식에 대해 *StrLen_or_IndPtr* 은 데이터 잘림이 발생할 경우 SQL_NO_TOTAL을 반환합니다.  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetData 지원  
 날짜/시간 형식의 결과 열 값에 설명 된 대로 변환 됩니다 [SQL에서 C로 변환을](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)합니다.  
  
 자세한 내용은 참조 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetData 지원  
 **SQLGetData** 는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 참조 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [SQLGetData 함수](http://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  