---
title: "버퍼 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7fa45570f0f5bda2190f7b3193f404ffccd3d621
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="buffers"></a>버퍼
버퍼는 드라이버 및 응용 프로그램 간에 데이터를 전달 하는 데 사용 되는 응용 프로그램 메모리의 일부입니다. 예를 들어 응용 프로그램 버퍼에 연결할 수 있는, 또는 *하면서 바인딩된* 결과 집합으로 열 **SQLBindCol**합니다. 각 행을 인출할 때 이러한 버퍼에 각 열에 대 한 데이터가 반환 됩니다. *입력 버퍼* 드라이버;에 응용 프로그램에서 데이터를 전달 하는 데 사용 됩니다 *출력 버퍼* 응용 프로그램에는 드라이버에서 데이터를 반환 하는 데 사용 됩니다.  
  
> [!NOTE]  
>  ODBC 함수 SQL_ERROR를 반환 하는 경우 출력 매개 변수를 해당 함수의의 내용을 정의 되지 않습니다.  
  
 이 토론 주로 확인할 수 없는 형식의 버퍼와 함께 자체와 관련 됩니다. 이 버퍼의 주소와 같은 대 SQLPOINTER, 형식의 인수로 표시는 *TargetValuePtr* 인수 **SQLBindCol**합니다. 그러나 버퍼를 사용 하는 인수 같은 여기에서 설명 된 항목 중 일부에 적용 드라이버와 같은 문자열을 전달 하는 데 사용 되는 인수는 *TableName* 인수 **SQLTables**합니다.  
  
 일반적으로 이러한 버퍼 쌍으로 제공 합니다. *데이터 버퍼* 는 자체 데이터를 전달 하는 데 사용 *길이/표시기 버퍼* 데이터가 NULL 인지 여부를 나타내는 SQL_NULL_DATA 같은 특수 값 또는 데이터 버퍼에 있는 데이터의 길이 전달 하는 데 사용 됩니다. 데이터 버퍼에 있는 데이터의 길이 자체 데이터 버퍼의 길이와 다릅니다. 다음 그림은 데이터 버퍼 및 길이/표시기 버퍼 간의 관계를 보여 줍니다.  
  
 ![데이터 버퍼 및 길이 &#47; 표시기 버퍼](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 길이/표시기 버퍼는 데이터 버퍼에는 문자 또는 이진 데이터 등의 가변 길이 데이터가 포함 될 때마다 필요 합니다. 데이터 버퍼에는 정수 또는 날짜 구조를 같은 고정 길이 데이터를 포함 하는 경우에 길이/표시기 버퍼 데이터의 길이 이미 알려져 있으므로 표시기 값을 받는 데만 필요 합니다. 고정 길이 데이터로 길이/표시기 버퍼를 사용 하는 응용 프로그램, 드라이버에 전달 된 길이 무시 합니다.  
  
 데이터 버퍼 및 포함 된 데이터의 길이 문자가 아닌 바이트 단위로 측정 됩니다. 이러한 구분이 바이트 수와 문자에서 길이 같기 때문에 ANSI 문자열을 사용 하는 프로그램에 대 한 중요 하지 않습니다.  
  
 데이터 버퍼를 나타낼 경우 드라이버에서 정의 된 설명자 필드, 진단 필드 또는 특성, 응용 프로그램을 나타내야 드라이버 관리자를 함수 인수는 필드 또는 특성에 대 한 값을 나타내는 특성입니다. 응용 프로그램은 다음 값 중 하나에 필드 또는 특성을 설정 하는 함수 호출의 길이 인수를 설정 하 여이 수행 합니다. (동일한은 필드 또는 인수 설정 함수에 대 한 인수 자체에 값을 가리키는 예외와 특성의 값을 검색 하는 함수에도 마찬가지입니다.)  
  
-   함수 인수는 필드 또는 특성에 대 한 값을 나타내는 문자열을에 대 한 포인터가 고 *길이* 인수는 SQL_NTS 또는 문자열의 길이입니다.  
  
-   응용 프로그램 이진 버퍼에 대 한 포인터를 함수 인수는 필드 또는 특성에 대 한 값을 나타내는 사용 하는 경우는 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *길이* 인수입니다. 이렇게 하면 배치에 음수 값은 *길이* 인수입니다.  
  
-   함수는 필드 또는 특성에 대 한 값을 나타내는 인수가 문자열 또는 이진 문자열 이외의 값에 대 한 포인터는 *길이* 인수 SQL_IS_POINTER 값이 있어야 합니다.  
  
-   필드 또는 특성에 대 한 값을 나타내는 함수 인수는 고정 길이 값을 포함 하는 경우는 *길이* 인수가 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, 또는 SQL_ISI_USMALLINT를 적절 하 게 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [지연 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [데이터 버퍼 사용](../../../odbc/reference/develop-app/using-data-buffers.md)
