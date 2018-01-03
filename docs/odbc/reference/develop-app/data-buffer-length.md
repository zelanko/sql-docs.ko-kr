---
title: "데이터 버퍼 길이가 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b9a95fac384f0df435bd28df9d21f3fa357e6d2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="data-buffer-length"></a>데이터 버퍼 길이
응용 프로그램 데이터 버퍼의 바이트 길이 드라이버에 전달 명명 된 인수로 *BufferLength* 또는 비슷한 이름입니다. 예를 들어, 다음에 호출에서 **SQLBindCol**, 응용 프로그램의 길이 지정 된 *ValuePtr* 버퍼 (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 항상 드라이버 버퍼 길이 인수는 출력 문자열 인수에 있는 모든 함수에 문자 수가 바이트의 수를 반환 합니다.  
  
 데이터는 버퍼 길이 출력 버퍼에만 필요 드라이버 버퍼의 끝을 지나서 쓰기 방지 하기 위해 사용 합니다. 그러나 드라이버는 버퍼에 문자 또는 이진 데이터와 같은 가변 길이 데이터를 포함 하는 경우에 데이터 버퍼 길이 확인 합니다. 드라이버는 데이터 버퍼 길이 무시 하 고이 버퍼에서 데이터를 포함할 수 있는 크기는 가정 버퍼에는 정수 또는 날짜 구조를 같은 고정 길이 데이터를 포함 하는 경우 즉, 고정 길이 데이터를 하지 자릅니다. 따라서 고정 길이 데이터에 대해 너무 큰 버퍼를 할당할 응용 프로그램에 대 한 것입니다.  
  
 비 데이터의 잘림은 문자열을 출력 하는 경우에 발생 (에 대해 반환 되는 커서 이름은 같은 **SQLGetCursorName**), 버퍼 길이 인수에 반환 된 길이 가능한 최대 문자 길이입니다.  
  
 드라이버는 이러한 버퍼에 쓸 데이터 버퍼 길이 입력된 버퍼에 대 한 필요 하지 않습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [데이터 길이, 버퍼 길이 및 잘라내기](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [문자 데이터 및 C 문자열](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
