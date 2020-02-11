---
title: 커서 닫기 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036537"
---
# <a name="closing-the-cursor"></a>커서 닫기
응용 프로그램이 커서를 사용 하 여 완료 되 면 **SQLCloseCursor** 를 호출 하 여 커서를 닫습니다. 다음은 그 예입니다.  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 응용 프로그램이 커서를 닫을 때까지 커서를 열 때 사용 하는 문은 다른 SQL 문 실행과 같은 대부분의 다른 작업에 사용할 수 없습니다. 커서가 열려 있는 동안 호출 될 수 있는 전체 함수 목록은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.  
  
> [!NOTE]  
>  커서를 닫으려면 응용 프로그램이 **Sqlcancel**이 아닌 **SQLCloseCursor**를 호출 해야 합니다.  
  
 커서는 트랜잭션을 커밋하거나 롤백하는 경우를 제외 하 고는 명시적으로 닫을 때까지 열린 상태로 유지 됩니다 .이 경우 일부 데이터 소스는 커서를 닫습니다. 특히 **Sqlfetch** 가 SQL_NO_DATA를 반환할 때 결과 집합의 끝에 도달 하면 커서가 닫히지 않습니다. 빈 결과 집합 (문이 성공적으로 실행 되었지만 행이 반환 되지 않은 경우 생성 된 결과 집합)의 경우에도 명시적으로 닫아야 합니다.
