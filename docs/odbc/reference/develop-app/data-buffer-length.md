---
title: 데이터 버퍼 길이 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a4e9a739201d74cfc6c4f7c18e64b91e0fabe4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305264"
---
# <a name="data-buffer-length"></a>데이터 버퍼 길이
응용 프로그램은 *BufferLength* 또는 유사한 이름의 인수에서 드라이버에 데이터 버퍼의 바이트 길이를 전달합니다. 예를 들어 **SQLBindCol에**대한 다음 호출에서 응용 프로그램은 *ValuePtr* 버퍼(sizeof(ValuePtr)의**길이를***ValuePtr***** 지정합니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 드라이버는 항상 출력 문자열 인수가 있는 함수의 버퍼 길이 인수에서 문자 수가 아닌 바이트 수를 반환합니다.  
  
 데이터 버퍼 길이는 출력 버퍼에만 필요합니다. 드라이버는 버퍼의 끝을 지나 쓰기를 피하기 위해 이를 사용합니다. 그러나 드라이버는 버퍼에 문자 또는 이진 데이터와 같은 가변 길이 데이터가 포함된 경우에만 데이터 버퍼 길이를 확인합니다. 버퍼에 정수 또는 날짜 구조와 같은 고정 길이 데이터가 포함된 경우 드라이버는 데이터 버퍼 길이를 무시하고 버퍼가 데이터를 보유할 수 있을 만큼 충분히 크다고 가정합니다. 즉, 고정 길이 데이터를 트렁킨다. 따라서 응용 프로그램에서 고정 길이 데이터에 대해 충분한 버퍼를 할당하는 것이 중요합니다.  
  
 데이터 이외의 출력 문자열이 잘리는 경우(예: **SQLGetCursorName에**대해 반환된 커서 이름) 버퍼 길이 인수에서 반환된 길이는 가능한 최대 문자 길이입니다.  
  
 드라이버가 이러한 버퍼에 쓰지 않기 때문에 입력 버퍼에는 데이터 버퍼 길이가 필요하지 않습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [길이/표시기 값 사용](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [데이터 길이, 버퍼 길이 및 잘라내기](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [문자 데이터 및 C 문자열](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
