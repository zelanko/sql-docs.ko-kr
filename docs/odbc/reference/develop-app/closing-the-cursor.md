---
title: 커서 닫기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299143"
---
# <a name="closing-the-cursor"></a>커서 닫기
응용 프로그램이 커서를 사용하여 완료되면 **SQLCloseCursor를** 호출하여 커서를 닫습니다. 다음은 그 예입니다.  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 응용 프로그램이 커서를 닫을 때까지 커서가 열리는 문은 다른 SQL 문을 실행하는 것과 같은 대부분의 다른 작업에 사용할 수 없습니다. 커서가 열려 있는 동안 호출할 수 있는 함수의 전체 목록은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.  
  
> [!NOTE]  
>  커서를 닫기 위해 응용 프로그램은 **SQLCloseCursor를**호출해야 **합니다.**  
  
 커서는 트랜잭션이 커밋되거나 롤백되는 경우를 제외하고 명시적으로 닫을 때까지 열려 있으며, 이 경우 일부 데이터 원본은 커서를 닫습니다. 특히 결과 집합의 끝에 도달 하는 **경우 SQLFetch** SQL_NO_DATA 반환 하는 경우 커서를 닫지 않습니다. 빈 결과 집합의 커서(문이 성공적으로 실행되었지만 행이 반환되지 않은 경우 생성된 결과 집합)도 명시적으로 닫아야 합니다.
