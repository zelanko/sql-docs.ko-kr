---
title: Long 데이터 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61f6e2d5c2999a1ff7cea86d497eb4f0fb13244
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061601"
---
# <a name="getting-long-data"></a>Long 데이터 가져오기
Dbms 정의할 *긴 데이터* 모든 문자 또는 이진 데이터 255 자 같은 특정 크기입니다. 이 데이터는 몇 천 문자의 일부 설명 등의 단일 버퍼에 저장할 수 있을 만큼 적습니다 수 있습니다. 그러나 긴 텍스트 문서 등 비트맵 메모리에 저장 하는 데 오랜 수 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없으므로 사용 하 여 파트의 드라이버에서 검색할 **SQLGetData** 행의 다른 데이터를 가져온 후 합니다.  
  
> [!NOTE]  
>  응용 프로그램 모든 형식의 사용 하 여 데이터를 실제로 검색할 수 있습니다 **SQLGetData**, 문자 및 이진 데이터 부분에서 검색할 수 있지만 데이터 뿐 아니라 long입니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 일반적으로 사용 하는 이유 **SQLGetData**합니다. 버퍼 열에 바인딩합니다 버퍼에 데이터를 반환 하는 드라이버 수를 훨씬 쉽습니다.  
  
 열에서 긴 데이터를 검색 하려면 응용 프로그램이 먼저 호출 **SQLFetchScroll** 하거나 **SQLFetch** 행으로 이동 하 여 바인딩된 열에 대 한 데이터를 인출 합니다. 그런 다음 응용 프로그램 호출 **SQLGetData**합니다. **SQLGetData** 와 동일한 인수가 **SQLBindCol**: 문 핸들을 열 수; 응용 프로그램 변수의 C 데이터 유형, 주소 및 바이트 길이 및 길이/표시기 버퍼의 주소입니다. 두 함수는 기본적으로 동일한 작업을 수행 하기 때문에 동일한 인수를 갖습니다. 모두 드라이버 응용 프로그램 변수를 설명 하며 특정 열에 대 한 데이터를 변수에 반환 되어야 함을 지정 합니다. 주요 차이점은는 **SQLGetData** 행이 인출 후에 호출 됩니다 (으로 인스턴스라고도 하며 *런타임에 바인딩* 따라서)와 바인딩을 지정 하 여 **SQLGetData**  호출 기간 동안만 존재 합니다.  
  
 단일 열에 관한 **SQLGetData** 처럼 **SQLFetch**: 열에 대 한 데이터를 검색, 응용 프로그램 변수 형식으로 변환 하 고 해당 변수에 반환 합니다. 또한 길이/표시기 버퍼의 데이터의 바이트 길이 반환합니다. 방법에 대 한 자세한 내용은 **SQLFetch** 반환 데이터를 참조 하십시오 [행의 데이터를 인출](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)합니다.  
  
 **SQLGetData** 에서 서로 다릅니다 **SQLFetch** 하나의 중요 한 측면입니다. 이 호출 하면 두 번 이상 연속 해 서에서 동일한 열에 대 한 각 호출 데이터의 연속 부분을 반환 합니다. 마지막 호출을 제외 하 고 각 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (문자열 데이터 오른쪽 잘림); 반환 마지막으로 호출한 관계 없이 SQL_SUCCESS를 반환합니다. 이것이 어떻게 **SQLGetData** 부분에 대 한 long 데이터를 검색 하는 데 사용 됩니다. 반환할 데이터가 더 이상 없을 때 **SQLGetData** SQL_NO_DATA를 반환 합니다. 응용 프로그램은 데이터의 부분을 연결 하는 것일는 긴 데이터를 함께 배치 하는 일을 담당 합니다. 각 파트는 null로 끝나는; 응용 프로그램 파트를 연결 하는 경우 null 종료 문자를 제거 해야 합니다. 다른 긴 데이터의 가변 길이 책갈피를도 대 한 부분에서 데이터 검색을 수행할 수 있습니다. 일반적으로 드라이버에서 사용 가능한 데이터의 크기를 검색 하 고 바이트 길이의 SQL_NO_TOTAL 반환 하지 못할 수 있지만 각 호출에서 길이/표시기 버퍼 감소 이전 호출에서 반환 된 바이트 수 만큼 반환 값입니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
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
  
 사용 하 여 몇 가지 제한 사항이 **SQLGetData**합니다. 일반적으로 열에 사용 하 여 액세스할 **SQLGetData**:  
  
-   (때문에 결과 집합의 열은 데이터 원본에서 읽는 방법을) 열 수를 늘려 순서 대로 액세스 해야 합니다. 오류가 호출 하는 것이 예를 들어 **SQLGetData** 5 열에 대해 다음 열 4에 대 한 호출 합니다.  
  
-   바인딩할 수 없습니다.  
  
-   마지막으로 바인딩된 열 보다 더 큰 열 값을 사용할 수 있어야 합니다. 예를 들어, 열 3 바인딩된 마지막 열을 사용 하는 경우 것이 호출에 오류가 **SQLGetData** 열 2에 대 한 합니다. 이러한 이유로 응용 프로그램 선택 목록의 끝에 long 데이터가 열을 배치 해야 합니다.  
  
-   경우에 사용할 수 없습니다 **SQLFetch** 하거나 **SQLFetchScroll** 둘 이상의 행을 검색 하기 위해 호출 되었습니다. 자세한 내용은 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)입니다.  
  
 일부 드라이버는 이러한 제한을 적용 하지 않습니다. 상호 운용 가능한 응용 프로그램은가 없거나 확인 되는 제한을 호출 하 여 적용 되지 않습니다 고 가정 하거나 해야 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 옵션을 사용 합니다.  
  
 응용 프로그램, 문자 또는 이진 데이터 열의 모든 데이터가 필요 없는 경우 문을 실행 하기 전에 SQL_ATTR_MAX_LENGTH 문 특성을 설정 하 여 DBMS 기반 드라이버의 네트워크 트래픽을 줄일 수 있습니다. 이 모든 문자 또는 이진 열에 대해 반환 되는 데이터의 바이트 수를 제한 합니다. 예를 들어, 긴 텍스트 문서를 포함 하는 열입니다. 에서는이 열이 포함 된 테이블을 탐색 하는 응용 프로그램을 각 문서의 첫 번째 페이지에 대해서만 표시 해야 합니다. 드라이버에서이 문 특성을 시뮬레이션할 수 있지만, 이지만이 작업을 수행할 필요가 없습니다. 특히, 응용 프로그램에서 문자 또는 이진 데이터를 자를 하려는 경우 해당 바인딩해야 작은 버퍼로 인 열에 **SQLBindCol** 및 드라이버는 데이터가 잘릴 수 있습니다.
