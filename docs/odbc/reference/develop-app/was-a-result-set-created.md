---
title: 결과 집합이 생성되었나요? | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c171a154dd16a291c5dbe1dcade8c01ea95fb084
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294551"
---
# <a name="was-a-result-set-created"></a>결과 집합이 생성되었나요?
대부분의 경우 응용 프로그램 프로그래머는 응용 프로그램에서 실행하는 명령문이 결과 집합을 만들지 여부를 알고 있습니다. 응용 프로그램이 프로그래머가 작성한 하드 코딩된 SQL 문을 사용하는 경우입니다. 일반적으로 응용 프로그램이 런타임에 SQL 문을 생성하는 경우: 프로그래머는 **SELECT** 문 또는 **INSERT** 문이 생성되는지 여부를 플래그하는 코드를 쉽게 포함할 수 있습니다. 일부 상황에서는 프로그래머가 명령문이 결과 집합을 만들지 여부를 알 수 없습니다. 응용 프로그램이 사용자가 SQL 문을 입력하고 실행할 수 있는 방법을 제공하는 경우에도 마찬가지입니다. 응용 프로그램이 프로시저를 실행하기 위해 런타임에 문을 생성하는 경우에도 마찬가지입니다.  
  
 이러한 경우 응용 프로그램은 **SQLNumResultCols를** 호출하여 결과 집합의 열 수를 결정합니다. 0이면 명령문이 결과 집합을 만들지 않았습니다. 다른 숫자인 경우 명령문은 결과 집합을 만들었습니다.  
  
 응용 프로그램은 명령문이 준비되거나 실행된 후 언제든지 **SQLNumResultCols를** 호출할 수 있습니다. 그러나 일부 데이터 원본은 준비된 문으로 생성되는 결과 집합을 쉽게 설명할 수 없으므로 문을 준비한 후 실행되기 전에 **SQLNumResultCols가** 호출되면 성능이 저하됩니다.  
  
 일부 데이터 원본은 결과 집합에서 SQL 문이 반환하는 행 수를 결정하는 데도 지원합니다. 이렇게 하려면 응용 프로그램에서 **SQLRowCount**를 호출합니다. 행 수가 나타내는 정확히 는 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 옵션(커서의 유형에 따라 다름)의 설정으로 **표시됩니다.** 이 비트 마스크는 반환된 행 수가 정확하거나 근사치인지 또는 전혀 사용할 수 없는지 각 커서 유형에 대해 나타냅니다. 정적 또는 키 집합 기반 커서에 대한 행 개수가 **SQLBulkOperations** 또는 **SQLSetPos를**통한 변경 내용또는 위치 가있는 업데이트 또는 삭제 문에 의해 영향을 받는지 여부는 이전에 나열된 동일한 옵션 인수에서 반환된 다른 비트에 따라 달라집니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조하십시오.
