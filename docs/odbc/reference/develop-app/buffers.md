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
ms.openlocfilehash: ad13379552e3a5a576b0aa5cc8720ca6ca1688a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118738"
---
# <a name="buffers"></a>버퍼
버퍼는 응용 프로그램과 드라이버 간에 데이터를 전달 하는 데 사용 되는 응용 프로그램 메모리의 일부입니다. 예를 들어 응용 프로그램 버퍼는 **SQLBindCol**을 사용 하 여 결과 집합 열에 연결 하거나이 열 *에 바인딩할* 수 있습니다. 각 행이 인출 되 면 이러한 버퍼의 각 열에 대해 데이터가 반환 됩니다. *입력 버퍼* 는 응용 프로그램에서 드라이버로 데이터를 전달 하는 데 사용 됩니다. *출력 버퍼* 는 드라이버에서 응용 프로그램으로 데이터를 반환 하는 데 사용 됩니다.  
  
> [!NOTE]  
>  ODBC 함수가 SQL_ERROR 반환 하는 경우 해당 함수에 대 한 출력 인수의 내용이 정의 되지 않습니다.  
  
 이 논의에서는 기본적으로 사용 되지 않는 유형의 버퍼를 다룹니다. 이러한 버퍼의 주소는 SQLPOINTER 형식의 인수로 표시 됩니다 (예: **SQLBindCol**의 *Targetvalueptr* 인수). 그러나 여기에서 설명 하는 일부 항목 (예: 버퍼에 사용 되는 인수)은 **Sqltables**의 *TableName* 인수와 같이 드라이버에 문자열을 전달 하는 데 사용 되는 인수에도 적용 됩니다.  
  
 이러한 버퍼는 일반적으로 쌍으로 제공 됩니다. 데이터 *버퍼* 는 데이터 자체를 전달 하는 데 사용 되는 반면 *길이/표시기 버퍼* 는 데이터 버퍼의 데이터 길이 또는 SQL_NULL_DATA와 같은 특수 값 (데이터가 NULL 임을 나타냄)을 전달 하는 데 사용 됩니다. 데이터 버퍼의 데이터 길이는 데이터 버퍼 자체의 길이와 다릅니다. 다음 그림에서는 데이터 버퍼와 길이/표시기 버퍼 간의 관계를 보여 줍니다.  
  
 ![데이터 버퍼 및 길이&#47;표시기 버퍼](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 문자 또는 이진 데이터와 같은 가변 길이 데이터가 데이터 버퍼에 포함 될 때마다 길이/표시기 버퍼가 필요 합니다. 데이터 버퍼에 정수 또는 날짜 구조와 같은 고정 길이 데이터가 포함 되어 있는 경우 데이터의 길이를 이미 알 수 있으므로 길이/표시기 버퍼가 표시기 값을 전달 하는 데만 필요 합니다. 응용 프로그램에서 고정 길이 데이터를 포함 하는 길이/표시기 버퍼를 사용 하는 경우 드라이버는 전달 된 모든 길이를 무시 합니다.  
  
 데이터 버퍼와 여기에 포함 된 데이터의 길이는 문자가 아닌 바이트 단위로 측정 됩니다. 바이트 및 문자 길이가 동일 하기 때문에 ANSI 문자열을 사용 하는 프로그램의 경우 이러한 구분은 중요 하지 않습니다.  
  
 데이터 버퍼가 드라이버 정의 설명자 필드, 진단 필드 또는 특성을 나타내는 경우 응용 프로그램은 필드 또는 특성에 대 한 값을 나타내는 함수 인수의 특성을 드라이버 관리자에 게 표시 해야 합니다. 응용 프로그램은 필드 또는 특성을 다음 값 중 하나로 설정 하는 함수 호출의 길이 인수를 설정 하 여이를 수행 합니다. (필드 또는 특성의 값을 검색 하는 함수의 경우에도 마찬가지입니다 .이는 인수가 설정 함수에 대 한 값을 가리키는 경우에도 마찬가지입니다.)  
  
-   필드 또는 특성의 값을 나타내는 함수 인수가 문자열에 대 한 포인터인 경우 *길이* 인수는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   필드 또는 특성의 값을 나타내는 함수 인수가 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 *길이* 인수에 SQL_LEN_BINARY_ATTR (*length*) 매크로의 결과를 저장 합니다. 그러면 *길이* 인수에 음수 값이 배치 됩니다.  
  
-   필드 또는 특성에 대 한 값을 나타내는 함수 인수가 문자열 또는 이진 문자열이 아닌 다른 값에 대 한 포인터인 경우 *길이* 인수는 SQL_IS_POINTER 값을 가져야 합니다.  
  
-   필드 또는 특성에 대 한 값을 나타내는 함수 인수에 고정 길이 값이 포함 된 경우 *길이* 인수는 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_ISI_USMALLINT입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [지연 버퍼](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [데이터 버퍼 사용](../../../odbc/reference/develop-app/using-data-buffers.md)
