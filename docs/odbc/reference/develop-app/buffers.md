---
title: 버퍼 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 306632f544f144aa4b21e150543c2d4ca5a37d0e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63008023"
---
# <a name="buffers"></a>버퍼
버퍼는 응용 프로그램 및 드라이버 간에 데이터를 전달 하는 데 사용 되는 응용 프로그램 메모리의 일부입니다. 예를 들어, 응용 프로그램 버퍼에 연결할 수 있는, 또는 *바인딩된* 결과 집합 열 **SQLBindCol**합니다. 각 행은 인출 하는 대로 이러한 버퍼의 각 열에 대 한 데이터가 반환 됩니다. *입력 버퍼* 드라이버; 응용 프로그램에서 데이터를 전달 하는 데 *출력 버퍼* 드라이버에서 응용 프로그램에 데이터를 반환 하는 데 사용 됩니다.  
  
> [!NOTE]  
>  ODBC 함수 SQL_ERROR를 반환 하는 경우 해당 함수에 출력 인수 내용의 정의 되지 않습니다.  
  
 이 토론 비활성화 유형의 버퍼를 사용 하 여 주로 자체와 관련 됩니다. 이러한 버퍼의 주소와 같은 대 SQLPOINTER, 형식의 인수로 표시 되는 *TargetValuePtr* 에서 인수 **SQLBindCol**합니다. 그러나 일부의 버퍼를 사용 하는 인수 등이 기사에서 다루는 항목에도 적용 드라이버에 같은 문자열을 전달 하는 데 사용 되는 인수를 *TableName* 에서 인수 **SQLTables**합니다.  
  
 일반적으로 이러한 버퍼 쌍으로 제공 합니다. *데이터 버퍼* 는 자체 데이터를 전달 하는 데 사용 *길이/표시기 버퍼* 데이터 버퍼에 데이터가 NULL 인지 여부를 나타내는 SQL_NULL_DATA 같은 특수 값을 데이터의 길이 전달 하는 데 사용 됩니다. 데이터 버퍼에 데이터의 길이 자체 데이터 버퍼의 길이 다릅니다. 다음 그림에서는 데이터 버퍼 및 길이/표시기 버퍼 간의 관계를 보여 줍니다.  
  
 ![데이터 버퍼 및 길이&#47;표시기 버퍼](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 길이/표시기 버퍼 데이터 버퍼에는 문자 또는 이진 데이터 등의 가변 길이 데이터가 포함 될 때마다 필요 합니다. 데이터 버퍼에는 정수 또는 날짜 구조와 같이 고정 길이 데이터를 포함 하는 경우 길이/표시기 버퍼 데이터의 길이 이미 알려져 있기 때문에 표시기 값을 받는 데만 필요 합니다. 고정 길이 데이터를 사용 하 여 길이/표시기 버퍼를 사용 하는 응용 프로그램, 드라이버에 전달 된 길이 무시 합니다.  
  
 데이터 버퍼 및 포함 된 데이터의 길이 문자가 아닌 바이트 단위로 측정 됩니다. 이 구분 문자와 바이트에서 길이가 같기 때문에 ANSI 문자열을 사용 하는 프로그램에 대 한 중요 하지 않습니다.  
  
 데이터 버퍼 설명자 드라이버에서 정의 된 필드, 진단 필드 또는 특성을 나타내는 필드 또는 특성에 대 한 값을 나타내는 함수 인수의 특성 응용 프로그램이 드라이버 관리자에을 지정 해야 합니다. 응용 프로그램은 다음 값 중 하나에 필드 또는 특성을 설정 하는 모든 함수 호출에서 길이 인수를 설정 하 여이 작업을 수행 합니다. (동일한 마찬가지 필드 또는 설정 함수에 대 한 인수 자체에 값을 가리키는 인수 예외를 사용 하 여 특성의 값을 검색 하는 함수입니다.)  
  
-   필드 또는 특성에 대 한 값을 나타내는 함수 인수는 문자열에 대 한 포인터 이면 합니다 *길이* 인수는 SQL_NTS 또는 문자열의 길이입니다.  
  
-   응용 프로그램 배치를 SQL_LEN_BINARY_ATTR의 결과 필드 또는 특성에 대 한 값을 나타내는 함수 인수가 이진 버퍼에 대 한 포인터 이면 (*길이*)에서 매크로 *길이* 인수입니다. 에 음수 값이 방식을 사용 하 여 *길이* 인수입니다.  
  
-   필드 또는 특성에 대 한 값을 나타내는 함수 인수가 아닌 문자열 또는 이진 문자열 값에 대 한 포인터 이면 합니다 *길이* 인수 SQL_IS_POINTER 값이 있어야 합니다.  
  
-   필드 또는 특성에 대 한 값을 나타내는 함수 인수에 고정 길이 값이 있는 경우는 *길이* 인수가 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, 또는 SQL_ISI_USMALLINT를 적절 하 게 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [지연 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [데이터 버퍼 사용](../../../odbc/reference/develop-app/using-data-buffers.md)
