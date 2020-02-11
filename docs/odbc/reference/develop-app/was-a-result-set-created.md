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
ms.openlocfilehash: 0f748e75f4e1579446b72b519356f2f649889fe0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078963"
---
# <a name="was-a-result-set-created"></a>결과 집합이 생성되었나요?
대부분의 경우 응용 프로그램 프로그래머는 응용 프로그램에서 실행 되는 문이 결과 집합을 생성 하는지 여부를 알 수 있습니다. 이는 응용 프로그램이 프로그래머가 작성 한 하드 코드 된 SQL 문을 사용 하는 경우에 해당 합니다. 일반적으로 응용 프로그램에서 런타임에 SQL 문을 생성 하는 경우입니다. 프로그래머는 **SELECT** 문 또는 **INSERT** 문이 생성 되 고 있는지 여부를 플래그 지정 하는 코드를 쉽게 포함할 수 있습니다. 몇 가지 상황에서 프로그래머는 문이 결과 집합을 만들지 여부를 알 수 없습니다. 응용 프로그램에서 사용자가 SQL 문을 입력 하 고 실행 하는 방법을 제공 하는 경우에도 마찬가지입니다. 응용 프로그램에서 런타임에 문을 생성 하 여 프로시저를 실행 하는 경우에도 마찬가지입니다.  
  
 이러한 경우 응용 프로그램은 **Sqlnumresultcols** 를 호출 하 여 결과 집합의 열 수를 확인 합니다. 0 인 경우 문은 결과 집합을 만들지 않습니다. 다른 숫자 이면 문에서 결과 집합을 만듭니다.  
  
 응용 프로그램은 문이 준비 되거나 실행 된 후 언제 든 지 **Sqlnumresultcols** 를 호출할 수 있습니다. 그러나 일부 데이터 원본은 준비 된 문으로 생성 되는 결과 집합을 쉽게 설명할 수 없기 때문에 문이 준비 된 후 실행 되기 전에 **Sqlnumresultcols** 를 호출 하면 성능이 저하 됩니다.  
  
 일부 데이터 소스는 SQL 문이 결과 집합에서 반환 하는 행 수를 결정 하는 기능도 지원 합니다. 이렇게 하기 위해 응용 프로그램은 **Sqlrowcount**를 호출 합니다. 행 개수가 나타내는 정확한 것은 **SQLGetInfo**호출에서 반환 되는 커서의 형식에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 옵션의 설정으로 표시 됩니다. 이 비트 마스크는 반환 되는 행 수가 정확한 지, 근사치 인지, 아니면 사용할 수 없는지에 대 한 각 커서 유형을 나타냅니다. 정적 또는 키 집합 커서에 대 한 행 개수가 **SQLBulkOperations** 또는 **SQLSetPos**를 통해 수행 된 변경 내용의 영향을 받는지 또는 배치 된 update 또는 delete 문에 의해 변경 된 내용에 따라 달라 지는 지는 앞서 설명한 것과 동일한 옵션 인수에서 반환 된 다른 비트에 따라 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조 하세요.
