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
manager: craigg
ms.openlocfilehash: 632a922abb544a379892dfa168f55efd605304c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792961"
---
# <a name="closing-the-cursor"></a>커서 닫기
호출 응용 프로그램이 커서를 사용 하 여 완료 되 면 **SQLCloseCursor** 를 커서를 닫습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 응용 프로그램을 커서를 닫을 때까지 커서가 열릴 문은 다른 SQL 문을 실행 하는 등 다른 대부분의 작업에 사용할 수 없습니다. 커서가 열려 있는 동안 호출할 수 있는 함수의 전체 목록은 참조 하세요 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
> [!NOTE]  
>  커서 닫기, 응용 프로그램에서 호출 해야 **SQLCloseCursor**가 아닌 **SQLCancel**합니다.  
  
 커서가 열린 상태로 남게 명시적으로 닫았는지 될 때까지 트랜잭션이 커밋되거나 롤백될 때 경우 일부 데이터 소스는 커서 닫기 제외 합니다. 특히 결과의 끝에 도달을 설정 하면 **SQLFetch** sql_no_data, 커서를 닫지 않습니다. 빈 결과 집합 (결과 집합을 문이 성공적으로 실행 하는 반환 행이 없는 경우 생성)에 커서를 명시적으로 닫아야 합니다.
