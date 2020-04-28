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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da901c22eb26af063397b4af184179ebe5c75924
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298993"
---
# <a name="getting-long-data"></a>Long 데이터 가져오기
Dbms는 *긴 데이터* 를 255 문자와 같이 특정 크기의 문자 또는 이진 데이터로 정의 합니다. 이 데이터는 단일 버퍼에 저장할 만큼 작을 수 있습니다. 예를 들어, 몇 천 자에 대 한 파트 설명입니다. 긴 텍스트 문서나 비트맵과 같이 메모리에 저장 하는 데 너무 오래 걸릴 수 있습니다. 이러한 데이터는 단일 버퍼에 저장 될 수 없으므로 행의 다른 데이터를 가져온 후 **SQLGetData** 를 사용 하 여 드라이버에서 해당 데이터를 검색 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 긴 데이터만이 아니라 **SQLGetData**를 사용 하 여 모든 유형의 데이터를 검색할 수 있습니다. 단, 문자 및 이진 데이터만 파트에서 검색할 수 있습니다. 그러나 데이터가 단일 버퍼에 맞게 충분히 작은 경우 일반적으로 **SQLGetData**를 사용할 이유가 없습니다. 버퍼를 열에 바인딩하는 것이 훨씬 더 쉬울 뿐만 아니라 드라이버에서 버퍼의 데이터를 반환할 수 있습니다.  
  
 열에서 긴 데이터를 검색 하기 위해 응용 프로그램은 먼저 **Sqlfetchscroll** 또는 **sqlfetch** 를 호출 하 여 행으로 이동 하 고 바인딩된 열의 데이터를 인출 합니다. 그러면 응용 프로그램이 **SQLGetData**를 호출 합니다. **SQLGetData** 의 인수는 **SQLBindCol**와 동일 합니다. 문 핸들 열 번호입니다. 응용 프로그램 변수의 C 데이터 형식, 주소 및 바이트 길이입니다. 길이/표시기 버퍼의 주소입니다. 두 함수 모두 기본적으로 동일한 작업을 수행 하기 때문에 동일한 인수를 가집니다. 즉, 둘 다 응용 프로그램 변수를 드라이버에 설명 하 고 특정 열에 대 한 데이터를 해당 변수에 반환 하도록 지정 합니다. 주요 차이점은 **sqlgetdata** 는 행이 인출 된 후 (이 경우에는 이러한 이유로 인해 *런타임에 바인딩이* 라고도 함) **sqlgetdata에서 지정** 된 바인딩이 호출 기간 동안만 지속 된다는 것입니다.  
  
 단일 열에 대 한 **SQLGetData** 는 **sqlfetch**와 같이 동작 합니다 .이는 열에 대 한 데이터를 검색 하 고,이를 응용 프로그램 변수의 형식으로 변환 하 고, 해당 변수에 반환 합니다. 또한 길이/표시기 버퍼에 있는 데이터의 바이트 길이를 반환 합니다. **Sqlfetch** 가 데이터를 반환 하는 방법에 대 한 자세한 내용은 [데이터 행 페치](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)를 참조 하세요.  
  
 **SQLGetData** 는 한 가지 중요 한 측면에서 **sqlfetch** 와 다릅니다. 동일한 열에 대해 연속적으로 두 번 이상 호출 되는 경우 각 호출은 데이터의 연속 부분을 반환 합니다. 마지막 호출을 제외한 각 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽 잘림)을 반환 합니다. 마지막 호출은 SQL_SUCCESS을 반환 합니다. 이는 **SQLGetData** 를 사용 하 여 파트에서 긴 데이터를 검색 하는 방법입니다. 반환할 데이터가 더 이상 없으면 **SQLGetData** 는 SQL_NO_DATA을 반환 합니다. 응용 프로그램은 데이터의 일부를 연결 하는 것을 의미 하는 긴 데이터를 함께 배치 해야 합니다. 각 파트는 null로 종료 됩니다. 파트를 연결 하는 경우 응용 프로그램은 null 종료 문자를 제거 해야 합니다. 다른 긴 데이터 뿐만 아니라 가변 길이 책갈피에 대해 파트의 데이터 검색을 수행할 수 있습니다. 길이/표시기 버퍼에서 반환 된 값은 이전 호출에서 반환 된 바이트 수 만큼 각 호출에서 감소 하지만, 드라이버에서 사용 가능한 데이터의 양을 검색 하 여 SQL_NO_TOTAL 바이트 길이를 반환할 수는 일반적이 지 않습니다. 다음은 그 예입니다.  
  
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
  
 **SQLGetData**사용에 대 한 몇 가지 제한 사항이 있습니다. 일반적으로 **SQLGetData**를 사용 하 여 액세스 한 열은 다음과 같습니다.  
  
-   는 결과 집합의 열을 데이터 원본에서 읽는 방식 때문에 열 번호를 늘려야 합니다. 예를 들어 열 5에 대해 **SQLGetData** 를 호출한 다음 열 4에 대해 호출 하면 오류가 발생 합니다.  
  
-   는 바인딩할 수 없습니다.  
  
-   는 마지막으로 바인딩된 열 보다 높은 열 번호를 가져야 합니다. 예를 들어 마지막으로 바인딩된 열이 열 3 인 경우 열 2에 대해 **SQLGetData** 를 호출 하면 오류가 발생 합니다. 따라서 응용 프로그램은 긴 데이터 열을 선택 목록의 끝에 넣어야 합니다.  
  
-   두 개 이상의 행을 검색 하기 위해 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출한 경우에는를 사용할 수 없습니다. 자세한 내용은 [블록 커서 사용](../../../odbc/reference/develop-app/using-block-cursors.md)을 참조 하세요.  
  
 일부 드라이버는 이러한 제한을 적용 하지 않습니다. 상호 운용 가능한 응용 프로그램은 존재를 가정 하거나 SQL_GETDATA_EXTENSIONS 옵션으로 **SQLGetInfo** 를 호출 하 여 적용 되지 않는 제한을 확인 해야 합니다.  
  
 응용 프로그램에 문자 또는 이진 데이터 열의 모든 데이터가 필요 하지 않은 경우 문을 실행 하기 전에 SQL_ATTR_MAX_LENGTH statement 특성을 설정 하 여 DBMS 기반 드라이버의 네트워크 트래픽을 줄일 수 있습니다. 그러면 모든 문자 또는 이진 열에 대해 반환 되는 데이터 바이트 수가 제한 됩니다. 예를 들어 긴 텍스트 문서를 포함 하는 열이 있다고 가정 합니다. 이 열이 포함 된 테이블을 탐색 하는 응용 프로그램은 각 문서의 첫 페이지만 표시 해야 할 수 있습니다. 이 문 특성은 드라이버에서 시뮬레이션할 수 있지만이 작업을 수행 하는 이유는 없습니다. 특히 응용 프로그램이 문자 또는 이진 데이터를 잘라내는 경우 **SQLBindCol** 를 사용 하 여 작은 버퍼를 열에 바인딩한 후 드라이버에서 데이터를 잘라내는 것이 좋습니다.
