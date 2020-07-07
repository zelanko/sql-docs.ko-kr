---
title: ODBC 변경 문자 변환 처리
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bce5fa58dfb665d3c4fe23f417a8585a4ec8eb6
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009041"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>문자 변환을 처리 시 ODBC 드라이버 동작 변경
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]Native CLIENT ODBC 드라이버 (SQLNCLI11.dll)는 SQL_WCHAR * (NCHAR/nvarchar/nvarchar (max)) 및 SQL_CHAR \* (CHAR/VARCHAR/NARCHAR (max)) 변환의 수행 방법을 변경 했습니다. SQLGetData, SQLBindCol, SQLBindParameter와 같은 ODBC 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client ODBC 드라이버 사용 시 길이/표시기 매개 변수로 (-4) SQL_NO_TOTAL을 반환합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 드라이버는 길이 값을 반환했으며 이는 부정확할 수 있습니다.  
  
## <a name="sqlgetdata-behavior"></a>SQLGetData 동작  
 여러 가지 Windows 기능을 사용하여 버퍼 크기를 0으로 지정할 수 있고 반환된 길이가 반환된 데이터의 크기가 됩니다. 다음 패턴은 Windows 프로그래머에 공통적입니다.  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 그러나이 시나리오에서는 **SQLGetData** 를 사용 하면 안 됩니다. 다음 패턴을 사용할 수 없습니다.  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData** 를 호출 하 여 실제 데이터 청크를 검색할 수 있습니다. **SQLGetData** 를 사용 하 여 데이터 크기를 가져오는 것은 지원 되지 않습니다.  
  
 다음은 잘못된 패턴 사용 시 드라이버 변경에 따른 영향을 보여 줍니다. 이 응용 프로그램은 **varchar** 열을 쿼리하고 유니코드로 바인딩합니다 (SQL_UNICODE/SQL_WCHAR).  
  
 쿼리입니다`select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 버전|길이 또는 표시기 결과|Description|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 이하|6|드라이버는 CHAR를 WCHAR로 변환하면 길이 * 2로 수행될 수 있다고 잘못 가정합니다.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client(버전 11.0.2100.60) 이상|-4(SQL_NO_TOTAL)|드라이버는 더 이상 CHAR에서 WCHAR로 또는 WCHAR에서 CHAR로의 변환이 (곱하기) \* 2 또는 (나누기)/2 동작 이라고 가정 하지 않습니다.<br /><br /> **SQLGetData** 를 호출 하면 더 이상 예상한 변환의 길이가 반환 되지 않습니다. 드라이버가 CHAR에서 WCHAR 또는 WCHAR에서 CHAR로 변환을 검색하고 잘못될 수 있는 *2 또는 /2 동작 대신 (-4) SQL_NO_TOTAL을 반환합니다.|  
  
 **SQLGetData** 를 사용 하 여 데이터 청크를 검색 합니다. (의사 코드가 다음과 같이 표시됨)  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>SQLBindCol 동작  
 쿼리입니다`select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 버전|길이 또는 표시기 결과|Description|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 이하|20|**Sqlfetch** 는 데이터 우변에 잘림이 있음을 보고 합니다.<br /><br /> 길이는 저장된 데이터가 아니라 반환된 데이터의 길이입니다(문자에 적합하지 않을 수 있는 *2 CHAR에서 WCHAR 변환을 가정).<br /><br /> 버퍼에 저장된 데이터는 123\0입니다. 버퍼는 NULL로 끝나지 않을 수 있습니다.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client(버전 11.0.2100.60) 이상|-4(SQL_NO_TOTAL)|**Sqlfetch** 는 데이터 우변에 잘림이 있음을 보고 합니다.<br /><br /> 나머지 데이터가 변환되지 않았기 때문에 길이는 -4 (SQL_NO_TOTAL)를 나타냅니다.<br /><br /> 버퍼에 저장된 데이터는 123\0입니다. - 버퍼는 NULL로 끝나지 않을 수 있습니다.|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter(OUTPUT 매개 변수 동작)  
 쿼리입니다`create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 버전|길이 또는 표시기 결과|Description|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 이하|2468|**Sqlfetch** 는 더 이상 사용할 수 있는 데이터를 반환 하지 않습니다.<br /><br /> **SQLMoreResults** 는 더 이상 사용할 수 있는 데이터를 반환 하지 않습니다.<br /><br /> 길이는 버퍼에 저장된 데이터가 아니라 서버에서 반환된 데이터의 크기를 나타냅니다.<br /><br /> 원래 버퍼는 63바이트와 NULL 종결자를 포함합니다. 버퍼는 NULL로 끝나지 않을 수 있습니다.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client(버전 11.0.2100.60) 이상|-4(SQL_NO_TOTAL)|**Sqlfetch** 는 더 이상 사용할 수 있는 데이터를 반환 하지 않습니다.<br /><br /> **SQLMoreResults** 는 더 이상 사용할 수 있는 데이터를 반환 하지 않습니다.<br /><br /> 나머지 데이터가 변환되지 않았기 때문에 길이는 (-4) SQL_NO_TOTAL를 나타냅니다.<br /><br /> 원래 버퍼는 63바이트와 NULL 종결자를 포함합니다. 버퍼는 NULL로 끝나지 않을 수 있습니다.|  
  
## <a name="performing-char-and-wchar-conversions"></a>CHAR 및 WCHAR 변환 수행  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC 드라이버는 CHAR 및 WCHAR 변환을 수행하는 여러 가지 방법을 제공합니다. 논리는 blob (varchar (max), nvarchar (max), ...)을 조작 하는 것과 비슷합니다.  
  
-   **SQLBindCol** 또는 **SQLBindParameter**를 사용 하 여 바인딩할 때 데이터는 지정 된 버퍼에 저장 되거나 잘립니다.  
  
-   바인딩하지 않으면 **SQLGetData** 및 **sqlparamdata**를 사용 하 여 데이터를 청크로 검색할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
