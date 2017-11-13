---
title: "Long 데이터를 가져오는 | Microsoft Docs"
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
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0ea30c211e3cfd66acf1588ef9ca2a45fd1037d1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getting-long-data"></a>긴 데이터 가져오기
Dbms 정의 *긴 데이터* 모든 문자 데이터 또는 255 자 같은 특정 크기에 대 한 이진 데이터입니다. 이 데이터 만큼 작지 않아서 몇 천 문자의 파트 설명 등의 단일 버퍼에 저장 될 수 있습니다. 그러나 너무 길어 긴 텍스트 문서 또는 비트맵 처럼 메모리에 저장할 수 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없습니다, 때문에 사용 하 여 파트에서 드라이버에서 검색 된 **SQLGetData** 행의 다른 데이터를 가져온 후 합니다.  
  
> [!NOTE]  
>  응용 프로그램에 모든 종류의 데이터를 검색할 실제로 수 **SQLGetData**, 뿐 아니라 (long) 데이터, 문자 및 이진 데이터 부분에서 검색할 수 있지만 합니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 없기 일반적으로 사용할 이유가 없습니다 **SQLGetData**합니다. 버퍼 열에 바인딩합니다 하는 버퍼에 데이터를 반환 하는 드라이버 훨씬 쉽습니다.  
  
 열에서 긴 데이터를 검색 하려면 응용 프로그램이 처음 호출 **SQLFetchScroll** 또는 **SQLFetch** 하는 행으로 이동 하 고 바인딩된 열에 대 한 데이터를 인출 합니다. 그런 다음 응용 프로그램 호출 **SQLGetData**합니다. **SQLGetData** 와 같은 인수에 **SQLBindCol**: 문 핸들; 열 번호; 응용 프로그램 변수의 C 데이터 형식, 주소 및 바이트 길이 길이/표시기 버퍼의 주소입니다. 두 함수는 기본적으로 동일한 작업을 수행 하기 때문에 동일한 인수가 있어야: 응용 프로그램 변수에서 드라이버에 설명와 특정 열에 대 한 데이터를 변수에 반환 되어야 함을 지정 합니다. 주요 차이점은 하 **SQLGetData** 하면 행이 인출 후에 호출 됩니다 (때때로 이라고 하 고 *런타임에 바인딩* 이러한 이유로)에 바인딩을 지정 하 고 **SQLGetData**  호출 기간 동안에만 유지 되는 기간.  
  
 단일 열에 대 한 **SQLGetData** 처럼 동작 **SQLFetch**: 열에 대 한 데이터를 검색, 응용 프로그램 변수 형식으로 변환 하 고 해당 변수에 반환 합니다. 또한 길이/표시기 버퍼의 데이터의 바이트 길이 반환합니다. 방법에 대 한 자세한 내용은 **SQLFetch** 반환 데이터 참조 [행의 데이터를 인출](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)합니다.  
  
 **SQLGetData** 에서 다른 **SQLFetch** 한 중요 한 측면에서 합니다. 호출 될 두 번 이상 연속 해 서에서 동일한 열에 대 한 각 호출 데이터의 연속 된 부분을 반환 합니다. 마지막 호출을 제외한 각 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다); 반환 마지막으로 호출한 관계 없이 SQL_SUCCESS를 반환 합니다. 이 어떻게 **SQLGetData** 부분에 long 데이터를 검색 하는 데 사용 됩니다. 반환할 데이터가 더 이상 없을 때 **SQLGetData** SQL_NO_DATA를 반환 합니다. 응용 프로그램은 긴 데이터를 함께 배치 하는 데 일부 데이터를 연결 하 의미입니다. 각 파트는 null로 끝나는; 응용 프로그램 부분을 연결 하는 경우 null 종결 문자를 제거 해야 합니다. 다른 긴 데이터의 경우와 다양 한 길이의 책갈피를도 대 한 부분에서 데이터 검색을 수행할 수 있습니다. 일반적으로 드라이버에서 사용 가능한 데이터의 크기를 검색 하 고 SQL_NO_TOTAL의 바이트 길이 반환 하지 못할 수 있지만 각 호출에 길이/표시기 버퍼 감소 이전 호출에서 반환 된 바이트 수로 반환 된 값입니다. 예를 들어  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 사용 하 여 몇 가지 제한 사항이 **SQLGetData**합니다. 일반적으로 열에으로 액세스할 **SQLGetData**:  
  
-   (때문에 결과 집합의 열은 데이터 원본에서 읽는 방법을) 열 수를 늘리면 순서 대로 액세스 해야 합니다. 호출 하는 오류는 예를 들어 **SQLGetData** 열 5에 대 한 다음 열 4에 대 한 호출입니다.  
  
-   바인딩할 수 없습니다.  
  
-   마지막 바인딩된 열 보다 더 높은 열 수가 있어야 합니다. 예를 들어 3 열이 바인딩된 마지막 열을 사용 하는 경우 것은 오류가 호출할 **SQLGetData** 열 2에 대 한 합니다. 이러한 이유로 응용 프로그램 선택 목록의 끝에 긴 데이터 열을 배치 해야 합니다.  
  
-   경우에 사용할 수 없습니다 **SQLFetch** 또는 **SQLFetchScroll** 둘 이상의 행을 검색 하기 위해 호출 되었습니다. 자세한 내용은 참조 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)합니다.  
  
 일부 드라이버는 이러한 제한을 적용 하지 않습니다. 상호 운용 가능한 응용 프로그램에는 이러한 없거나 결정 되는 제한을 호출 하 여 적용 되지 않습니다 가정 하거나 해야 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 옵션을 사용 합니다.  
  
 응용 프로그램 문자 또는 이진 데이터 열에 있는 모든 데이터, 필요 하지 않는 경우 문을 실행 하기 전에 SQL_ATTR_MAX_LENGTH 문 특성을 설정 하 여 DBMS 기반 드라이버에서 네트워크 트래픽을 줄일 수 있습니다. 문자 또는 이진 열에 대해 반환 되는 데이터의 바이트 수를 제한 합니다. 예를 들어 열 긴 텍스트 문서에 포함 되어 있다고 가정 합니다. 에서는이 열이 포함 된 테이블을 탐색 하는 응용 프로그램은 각 문서의 첫 번째 페이지에만 표시 해야 할 수 있습니다. 드라이버에서이 문 특성을 시뮬레이션할 수 있지만, 이지만이 작업을 수행할 필요가 없습니다. 특히, 응용 프로그램를 문자 또는 이진 데이터 truncate 하려는 경우 해당 바인딩해야 작은 버퍼의 열에 **SQLBindCol** 드라이버는 데이터가 잘릴 수 있도록 합니다.

