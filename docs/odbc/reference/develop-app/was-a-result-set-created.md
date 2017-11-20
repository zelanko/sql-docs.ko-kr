---
title: "결과 집합 생성 되었습니까? | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c38b613ed4c2e6efb5737118030905ab9de60b1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="was-a-result-set-created"></a>결과 집합 생성 되었습니까?
대부분의 경우 응용 프로그램 프로그래머는 응용 프로그램을 실행 하는 문을 결과 집합을를 만들 됩니다 있는지 여부를 알고 합니다. 이 경우 응용 프로그램에서 프로그래머가 작성 된 하드 코드 된 SQL 문은 사용 하는 경우입니다. 일반적으로 응용 프로그램 런타임 시 SQL 문을 생성 하는 경우: 프로그래머가 쉽게 플래그를 지정 하는 코드를 포함 시킬 수 있는지 여부를 **선택** 문 또는 **삽입** 문이 되 고 구성 됩니다. 몇 가지 상황에서 프로그래머가 알 수 없습니다 수는 문은 결과 집합을 만듭니다 여부. 응용 프로그램 사용자가 입력 하 고 SQL 문을 실행 하는 방법을 제공 하는 경우에 마찬가지입니다. 응용 프로그램에서 런타임에 프로시저를 실행 하는 문을 생성 하는 경우에 마찬가지입니다.  
  
 이러한 경우에는 응용 프로그램 호출 **SQLNumResultCols** 결과 집합의 열 수를 결정 합니다. 문이 결과 집합; 0 이면 만들지 않은 다른 모든 숫자 이면 문이 결과 집합을 만들려면 않았습니다.  
  
 응용 프로그램에서 호출할 수 **SQLNumResultCols** 문이 준비 되거나 실행 된 후 언제 든 지 합니다. 그러나 일부 데이터 원본에 의해 준비 된 문을 생성 되는 결과 집합을 설명할 쉽게 수, 때문에 성능이 저하 됩니다 경우 **SQLNumResultCols** 문을 준비 된 후 실행 하기 전에 호출 됩니다.  
  
 일부 데이터 소스는 SQL 문의 결과 집합에 반환 하는 행 수를 결정도 지원 합니다. 이렇게 하려면 응용 프로그램 호출 **SQLRowCount**합니다. (커서 유형)에 따라 다름 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2, 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 옵션의 설정으로 표시 됩니다 정확히 어떤 행 개수를 나타냅니다. 에 대 한 호출에서 반환 된 **SQLGetInfo**합니다. 이 비트 마스크 각 커서 유형에 대해 반환 된 행 개수 정확한, 근사치 인지 나타내거나를 전혀 사용할 수 없습니다. 정적 행 개수 또는 키 집합 커서를 통해 변경 하 여 영향을 받는 여부 **SQLBulkOperations** 또는 **SQLSetPos**, 위치 지정된 update 또는 delete 문을 하 여 다른 비트에 따라 하거나 앞에 나열 된 옵션 인수는 동일 하 여 반환 합니다. 자세한 내용은 참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.

