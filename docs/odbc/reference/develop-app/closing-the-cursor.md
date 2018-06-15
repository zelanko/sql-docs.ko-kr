---
title: 커서를 닫으면 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 794180396f9b233d32283f46264a696c80559d21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907718"
---
# <a name="closing-the-cursor"></a>커서 닫기
호출 응용 프로그램은 커서를 사용 하 여 완료 되 면 **SQLCloseCursor** 를 커서를 닫습니다. 예를 들어:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 응용 프로그램이 커서를 닫아야 커서가 열릴 문은 다른 SQL 문을 실행 하는 등 다른 대부분 작업에 사용할 수 없습니다. 커서가 열려 있는 동안 호출 될 수 있는 함수 목록은 전체 참조 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
> [!NOTE]  
>  커서 닫기, 응용 프로그램 호출 해야 **SQLCloseCursor**이 아니라 **SQLCancel**합니다.  
  
 커서가 열린 상태로 남게 명시적으로 닫았는지 될 때까지 제외는 트랜잭션이 커밋되거나 롤백될 때이 경우 일부 데이터 원본의 커서를 닫습니다. 특히 결과의 끝에 도달한 설정 때 **SQLFetch** sql_no_data가 반환, 커서를 닫지 않습니다. 빈 결과 집합 (결과 집합 생성 하는 문이 성공적으로 실행 되지만 반환 된 행이 없는 경우)에 커서를 명시적으로 닫아야 합니다.
