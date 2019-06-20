---
title: 결과 집합이 생성되었나요? | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db287e729678f54aaf637950c89c724724678f08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208400"
---
# <a name="was-a-result-set-created"></a>결과 집합이 생성되었나요?
대부분의 경우 응용 프로그램 프로그래머는 응용 프로그램을 실행는 문은 결과 집합을 생성 하는지 여부를 알고 있습니다. 이 경우 응용 프로그램 프로그래머가 작성 하드 코딩 된 SQL 문을 사용 하는 경우입니다. 이 일반적으로 응용 프로그램 런타임 시 SQL 문을 생성 하는 경우: 프로그래머가 플래그를 지정 하는 코드를 쉽게 포함할 수 있는지 여부를 **선택** 문 또는 **삽입** 문을 생성 되 고 합니다. 일부 경우에 프로그래머 알아낼 수는 없기 문이 결과 집합을 만듭니다 여부. 응용 프로그램 사용자가 입력 하 고 SQL 문을 실행 하는 방법을 제공 하는 경우에 그렇습니다. 응용 프로그램이 런타임에 프로시저를 실행 하는 문을 생성 하는 경우에 마찬가지입니다.  
  
 이러한 경우 응용 프로그램 호출 **SQLNumResultCols** 결과 집합의 열 수를 결정 합니다. 결과 집합을;이 0 인 경우 문을 만들지 않고 다른 모든 숫자 이면 문이 결과 집합을 만들지 않은 합니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLNumResultCols** 문이 준비 되거나 실행 된 후 언제 든 지 합니다. 그러나 일부 데이터 원본 준비 된 문에서 만들어지는 결과 집합으로 쉽게 설명할 수 없는, 때문에 성능이 저하 됩니다 하는 경우 **SQLNumResultCols** 문을 준비 되 면 실행 하기 전에 호출 됩니다.  
  
 일부 데이터 원본의 결과 집합에는 SQL 문에서 반환 하는 행의 수를 결정도 지원 합니다. 이렇게 하려면 응용 프로그램 호출 **SQLRowCount**합니다. (커서 유형)에 따라 다름 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2, 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 옵션의 설정에 따라 사실은 정확히 어떤 행 개수를 나타냅니다. 에 대 한 호출에서 반환한 **SQLGetInfo**합니다. 이 비트 마스크 각 커서 유형에 대해 반환 된 행 수를 정확 하 게, 근사치 인지 여부를 나타내거나를 전혀 사용할 수 없습니다. 정적 행 개수 여부 키 집합 커서를 통해 변경한 내용이 영향을 받지 **SQLBulkOperations** 또는 **SQLSetPos**, 또는 현재 위치 업데이트 또는 삭제 문을 실행 하 여 다른 비트에 종속 이전에 나열 된 동일한 옵션 인수를 반환 합니다. 자세한 내용은 참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
