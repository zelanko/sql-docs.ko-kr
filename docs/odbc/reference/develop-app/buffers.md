---
title: 버퍼 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c49e83e12463665f86f8cc15dc595e6ba2c506f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306288"
---
# <a name="buffers"></a>버퍼
버퍼는 응용 프로그램과 드라이버 간에 데이터를 전달하는 데 사용되는 모든 응용 프로그램 메모리 조각입니다. 예를 들어 응용 프로그램 버퍼는 **SQLBindCol**을 사용하여 결과 집합 열과 연결되거나 *바인딩될* 수 있습니다. 각 행을 가져오면 이러한 버퍼의 각 열에 대한 데이터가 반환됩니다. *입력 버퍼는* 응용 프로그램에서 드라이버로 데이터를 전달하는 데 사용됩니다. *출력 버퍼는* 드라이버에서 응용 프로그램에 데이터를 반환하는 데 사용됩니다.  
  
> [!NOTE]  
>  ODBC 함수가 SQL_ERROR 반환하는 경우 해당 함수에 대한 출력 인수의 내용은 정의되지 않습니다.  
  
 이 설명에서는 주로 확정되지 않은 형식의 버퍼와 관련이 있습니다. 이러한 버퍼의 주소는 **SQLBindCol**의 *TargetValuePtr* 인수와 같은 SQLPOINTER 형식의 인수로 나타납니다. 그러나 버퍼와 함께 사용되는 인수와 같이 여기에서 설명하는 일부 항목은 **SQLTable의** *TableName* 인수와 같이 문자열을 드라이버에 전달하는 데 사용되는 인수에도 적용됩니다.  
  
 이러한 버퍼는 일반적으로 쌍으로 제공됩니다. *데이터 버퍼는* 데이터 자체를 전달하는 데 사용되며 *길이/표시기 버퍼는* 데이터 버퍼의 데이터 길이 또는 데이터가 NULL임을 나타내는 SQL_NULL_DATA 같은 특수 값을 전달하는 데 사용됩니다. 데이터 버퍼의 데이터 길이는 데이터 버퍼 자체의 길이와 다릅니다. 다음 그림에서는 데이터 버퍼와 길이/표시기 버퍼 간의 관계를 보여 주며 있습니다.  
  
 ![데이터 버퍼 및 길이&#47;표시기 버퍼](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 데이터 버퍼에 문자 또는 이진 데이터와 같은 가변 길이 데이터가 포함될 때마다 길이/표시기 버퍼가 필요합니다. 데이터 버퍼에 정수 또는 날짜 구조와 같은 고정 길이 데이터가 포함된 경우 데이터의 길이가 이미 알려져 있으므로 표시기 값을 전달하는 데만 길이/표시기 버퍼가 필요합니다. 응용 프로그램에서 고정 길이 데이터가 있는 길이/표시기 버퍼를 사용하는 경우 드라이버는 길이가 전달된 모든 길이를 무시합니다.  
  
 데이터 버퍼와 포함된 데이터의 길이는 문자가 아닌 바이트 단위로 측정됩니다. 이러한 구분은 바이트와 문자길이가 동일하기 때문에 ANSI 문자열을 사용하는 프로그램에는 중요하지 않습니다.  
  
 데이터 버퍼가 드라이버 정의 설명자 필드, 진단 필드 또는 특성을 나타내는 경우 응용 프로그램은 드라이버 관리자에게 필드 또는 특성에 대한 값을 나타내는 함수 인수의 특성을 나타내야 합니다. 응용 프로그램은 필드 또는 특성을 다음 값 중 하나로 설정하는 함수 호출에서 length 인수를 설정하여 이 작업을 수행합니다. (인수가 설정 함수에 대한 값이 인수 자체에 있는 값을 가리키는 경우를 제외하고는 필드 또는 특성의 값을 검색하는 함수에도 마찬가지입니다.)  
  
-   필드 또는 특성의 값을 나타내는 함수 인수가 문자열 문자열에 대한 포인터인 경우 *length* 인수는 문자열 또는 SQL_NTS 길이입니다.  
  
-   필드 또는 특성의 값을 나타내는 함수 인수가 이진 버퍼에 대한 포인터인 경우 응용 프로그램은*SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 *길이* 인수에 배치합니다. 이렇게 하면 *길이* 인수에 음수 값이 배치됩니다.  
  
-   필드 또는 특성의 값을 나타내는 함수 인수가 문자열 또는 이진 문자열이 아닌 값에 대한 포인터인 경우 *length* 인수에는 SQL_IS_POINTER 값이 있어야 합니다.  
  
-   필드 또는 특성의 값을 나타내는 함수 인수에 고정 길이 값이 포함되어 있으면 *길이* 인수는 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_ISI_USMALLINT 적절하게 포함됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [지연 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [데이터 버퍼 사용](../../../odbc/reference/develop-app/using-data-buffers.md)
