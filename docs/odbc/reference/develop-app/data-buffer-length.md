---
title: 데이터 버퍼 길이가 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57f4fd34cfe3896bb29ed31f02906ce675e4b854
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811391"
---
# <a name="data-buffer-length"></a>데이터 버퍼 길이
명명 된 인수를 드라이버에 데이터 버퍼의 바이트 길이 전달 하는 응용 프로그램 *BufferLength* 또는 비슷한 이름입니다. 예를 들어, 다음에서에 호출할 **SQLBindCol**, 응용 프로그램의 길이 지정 합니다 *ValuePtr* 버퍼 (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 드라이버는 출력 문자열 인수를 사용 하는 모든 함수는 버퍼 길이 인수에 문자 수가 아니라 바이트 수를 항상 반환 됩니다.  
  
 데이터 버퍼 길이; 출력 버퍼에만 필요 드라이버는 버퍼의 끝을 지난 쓰기를 방지 하려면 하를 사용 합니다. 그러나 드라이버는 버퍼에 문자 또는 이진 데이터와 같은 가변 길이 데이터를 포함 하는 경우에 데이터 버퍼 길이 확인 합니다. 드라이버는 데이터 버퍼 길이 무시 하 고 버퍼 데이터를 저장 하기에 충분할 것으로 가정 버퍼에는 정수 또는 날짜 구조와 같이 고정 길이 데이터를 포함 하는 경우 즉, 고정 길이 데이터가 되지 자릅니다. 따라서 것이 고정 길이 데이터에 대해 충분히 큰 버퍼를 할당할 응용 프로그램에 대 한 중요 합니다.  
  
 발생의 비 데이터 잘림이 문자열을 출력 하는 경우 (에 대 한 반환 된 커서 이름이 같은 **SQLGetCursorName**), 버퍼 길이 인수에 반환 된 길이 가능한 최대 문자 길이입니다.  
  
 드라이버는 이러한 버퍼에 쓸 데이터 버퍼 길이 입력된 버퍼에 대 한 필요 하지 않습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [데이터 길이, 버퍼 길이 및 잘라내기](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [문자 데이터 및 C 문자열](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
