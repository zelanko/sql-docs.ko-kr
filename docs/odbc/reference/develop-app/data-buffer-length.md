---
title: 데이터 버퍼 길이 | Microsoft Docs
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
ms.openlocfilehash: 40fe9d23f14d4a7af80fe31a418cccf7133b7252
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067426"
---
# <a name="data-buffer-length"></a>데이터 버퍼 길이
응용 프로그램은 데이터 버퍼의 바이트 길이를 *bufferlength* 또는 이와 유사한 이름의 인수에 있는 드라이버로 전달 합니다. 예를 들어 SQLBindCol에 대 한 다음 호출에서 응용 프로그램은 **** *의 길이* (**sizeof (***valueptr***)**)를 지정 합니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 드라이버는 출력 문자열 인수가 있는 함수의 버퍼 길이 인수에서 항상 문자 수가 아니라 바이트 수를 반환 합니다.  
  
 데이터 버퍼 길이는 출력 버퍼에만 필요 합니다. 드라이버는 버퍼의 끝을 지나서 쓰기를 방지 하는 데 사용 합니다. 그러나 버퍼에 문자 또는 이진 데이터와 같은 가변 길이 데이터가 포함 되어 있는 경우에만 드라이버에서 데이터 버퍼 길이를 확인 합니다. 버퍼에 정수 또는 날짜 구조와 같은 고정 길이 데이터가 포함 되어 있는 경우 드라이버는 데이터 버퍼 길이를 무시 하 고 버퍼가 데이터를 저장할 수 있을 만큼 충분히 큰지 가정 합니다. 즉, 고정 길이 데이터는 잘리지 않습니다. 따라서 응용 프로그램에서 고정 길이 데이터에 충분 한 버퍼를 할당 하는 것이 중요 합니다.  
  
 데이터 출력이 아닌 출력 문자열이 발생 하는 경우 (예: **SQLGetCursorName**에 대해 반환 된 커서 이름) 버퍼 길이 인수에서 반환 되는 길이는 가능한 최대 문자 길이입니다.  
  
 드라이버가 이러한 버퍼에 쓰지 않으므로 입력 버퍼에 데이터 버퍼 길이가 필요 하지 않습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [길이/표시기 값 사용](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [데이터 길이, 버퍼 길이 및 잘라내기](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [문자 데이터 및 C 문자열](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
