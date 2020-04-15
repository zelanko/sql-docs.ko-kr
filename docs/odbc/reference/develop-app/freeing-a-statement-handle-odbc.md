---
title: 성명서 핸들 ODBC 해제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01e4cb46edf1b1a0f1c6dfaa0273c1dd5b392686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305618"
---
# <a name="freeing-a-statement-handle-odbc"></a>명령문 핸들 ODBC 해제
앞에서 설명한 것처럼 문을 삭제하고 새 문을 할당하는 것보다 문을 다시 사용하는 것이 더 효율적입니다. 명령문에 새 SQL 문을 실행하기 전에 응용 프로그램은 현재 명령문 설정이 적절한지 확인해야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 일반적으로 이전 SQL 문에 대한 매개 변수 및 결과 집합은 바인딩되지 않은 SQL_RESET_PARAMS 및 SQL_UNBIND 옵션으로 **SQLFreeStmt를** 호출하고 새 SQL 문을 다시 불러야 합니다.  
  
 응용 프로그램이 문을 사용하여 완료되면 **SQLFreeHandle을** 호출하여 문을 해제합니다. 문을 해제 한 후 ODBC 함수에 대 한 호출에서 명령문의 핸들을 사용 하는 응용 프로그램 프로그래밍 오류입니다. 이렇게 하면 정의되지 않았지만 치명적인 결과가 있을 수 있습니다.  
  
 **SQLFreeHandle이** 호출되면 드라이버는 명령문에 대한 정보를 저장하는 데 사용되는 구조를 해제합니다.  
  
 **SQLDisconnect는** 연결의 모든 문을 자동으로 해제합니다.
