---
title: 긴 데이터 얻기 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298993"
---
# <a name="getting-long-data"></a>Long 데이터 가져오기
DBMS는 *긴 데이터를* 255문자와 같은 특정 크기이상의 문자 또는 이진 데이터로 정의합니다. 이 데이터는 수천 개의 문자에 대한 부분 설명과 같이 단일 버퍼에 저장될 수 있을 만큼 작을 수 있습니다. 그러나 긴 텍스트 문서 나 비트 맵과 같이 메모리에 저장하기에는 너무 길 수 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없으므로 행의 다른 데이터를 가져온 후 **SQLGetData를** 사용하여 드라이버에서 검색됩니다.  
  
> [!NOTE]  
>  응용 프로그램은 문자 및 이진 데이터만 부분적으로 검색할 수 있지만 긴 데이터뿐만 아니라 **SQLGetData를**사용하여 모든 유형의 데이터를 실제로 검색할 수 있습니다. 그러나 데이터가 단일 버퍼에 들어갈 만큼 작으면 일반적으로 **SQLGetData**를 사용할 이유가 없습니다. 버퍼를 열에 바인딩하고 드라이버가 버퍼의 데이터를 반환하도록 하는 것이 훨씬 쉽습니다.  
  
 열에서 긴 데이터를 검색하려면 응용 프로그램이 먼저 **SQLFetchScroll** 또는 **SQLFetch를** 호출하여 행으로 이동하고 바인딩된 열에 대한 데이터를 가져옵니다. 그런 다음 응용 프로그램은 **SQLGetData를**호출합니다. **SQLGetData는** **SQLBindCol**: 문 핸들과 동일한 인수를 가짐입니다. 열 번호; 응용 프로그램 변수의 C 데이터 형식, 주소 및 바이트 길이; 및 길이/표시기 버퍼의 주소입니다. 두 함수는 본질적으로 동일한 작업을 수행하기 때문에 동일한 인수를 가지며 둘 다 드라이버에 응용 프로그램 변수를 설명하고 특정 열에 대한 데이터가 해당 변수에서 반환되도록 지정합니다. 주요 차이점은 **SQLGetData** 행을 가져온 후 호출 (그리고 때로는 이러한 이유로 *늦은 바인딩이라고도* 함) **및 SQLGetData에** 의해 지정 된 바인딩은 호출 기간 동안만 지속 됩니다.  
  
 단일 열에 대해 **SQLGetData는** **SQLFetch**: 열에 대한 데이터를 검색하고 응용 프로그램 변수의 유형으로 변환하고 해당 변수에서 반환합니다. 또한 길이/표시기 버퍼에서 데이터의 바이트 길이를 반환합니다. **SQLFetch가** 데이터를 반환하는 방법에 대한 자세한 내용은 [데이터 행 가져오기를](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)참조하십시오.  
  
 **SQLGetData는** 한 가지 중요한 점에서 **SQLFetch와** 다릅니다. 동일한 열에 대해 두 번 이상 연속으로 호출되는 경우 각 호출은 데이터의 연속된 부분을 반환합니다. 마지막 호출을 제외한 각 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004(문자열 데이터, 오른쪽 잘린)를 반환합니다. 마지막 호출은 SQL_SUCCESS 반환합니다. **SQLGetData는** 부분적으로 긴 데이터를 검색하는 데 사용되는 방법입니다. 반환할 데이터가 더 이상 없는 경우 **SQLGetData는** SQL_NO_DATA 반환합니다. 응용 프로그램은 긴 데이터를 함께 배치하는 책임을 지므로 데이터의 일부를 연결해야 할 수 있습니다. 각 부품은 null-종료됩니다. 응용 프로그램은 부품을 통합하는 경우 null 종료 문자를 제거해야 합니다. 부품의 데이터 검색은 가변 길이 의 책갈피뿐만 아니라 다른 긴 데이터에 대해서도 수행할 수 있습니다. 길이/표시기 버퍼에서 반환되는 값은 이전 호출에서 반환된 바이트 수만큼 각 호출에서 감소하지만 드라이버가 사용 가능한 데이터의 양을 검색하고 바이트 길이를 반환할 수 없는 SQL_NO_TOTAL. 다음은 그 예입니다.  
  
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
  
 **SQLGetData**를 사용하는 데는 몇 가지 제한 사항이 있습니다. 일반적으로 **SQLGetData로**액세스하는 열 :  
  
-   결과 집합의 열을 데이터 원본에서 읽는 방식으로 인해 열 수가 증가하는 순서로 액세스해야 합니다. 예를 들어 열 5에 대해 **SQLGetData를** 호출한 다음 열 4로 호출하는 오류입니다.  
  
-   바인딩할 수 없습니다.  
  
-   마지막 바인딩된 열보다 높은 열 번호가 있어야 합니다. 예를 들어 마지막 바인딩된 열이 열 3인 경우 열 2에 대해 **SQLGetData를** 호출하는 오류입니다. 따라서 응용 프로그램은 선택 목록의 끝에 긴 데이터 열을 배치해야 합니다.  
  
-   **SQLFetch** 또는 **SQLFetchScroll가** 두 개 이상의 행을 검색하기 위해 호출된 경우 사용할 수 없습니다. 자세한 내용은 [블록 커서 사용을](../../../odbc/reference/develop-app/using-block-cursors.md)참조하십시오.  
  
 일부 드라이버는 이러한 제한을 적용하지 않습니다. 상호 운용 가능한 응용 프로그램은 존재한다고 가정하거나 SQL_GETDATA_EXTENSIONS 옵션으로 **SQLGetInfo를** 호출하여 적용되지 않는 제한을 결정해야 합니다.  
  
 응용 프로그램에 문자 또는 이진 데이터 열의 모든 데이터가 필요하지 않은 경우 문을 실행하기 전에 SQL_ATTR_MAX_LENGTH 문 특성을 설정하여 DBMS 기반 드라이버의 네트워크 트래픽을 줄일 수 있습니다. 이렇게 하면 모든 문자 또는 이진 열에 대해 반환되는 데이터 바이트 수가 제한됩니다. 예를 들어 열에 긴 텍스트 문서가 포함되어 있다고 가정합니다. 이 열이 포함된 테이블을 찾아보는 응용 프로그램은 각 문서의 첫 페이지만 표시해야 할 수 있습니다. 이 문 특성은 드라이버에서 시뮬레이션할 수 있지만 이 작업을 수행할 이유는 없습니다. 특히 응용 프로그램이 문자 또는 이진 데이터를 줄이려는 경우 **SQLBindCol을** 사용하여 작은 버퍼를 열에 바인딩하고 드라이버가 데이터를 트렁크처리하도록 해야 합니다.
