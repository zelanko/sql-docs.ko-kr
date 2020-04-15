---
title: 오류 및 배치 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36a402686a695a08748df24a7b40a228d7a2ca7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300433"
---
# <a name="errors-and-batches"></a>오류 및 일괄 처리
SQL 문 일괄 처리를 실행하는 동안 오류가 발생하면 다음 네 가지 결과 중 하나가 가능합니다. (가능한 각 결과는 데이터 원본에 따라 다르며 일괄 처리에 포함된 문에 따라 달라질 수도 있습니다.)  
  
-   일괄 처리의 문이 실행되지 않습니다.  
  
-   일괄 처리의 문이 실행되지 않고 트랜잭션이 롤백됩니다.  
  
-   오류 문이 실행되기 전에 모든 문이 실행됩니다.  
  
-   오류 문을 제외한 모든 문이 실행됩니다.  
  
 처음 두 경우에서 **SQLExecute** 및 **SQLExecDirect** 반환 SQL_ERROR. 후자의 두 경우는 구현에 따라 SQL_SUCCESS_WITH_INFO 반환하거나 SQL_SUCCESS 수 있습니다. 모든 경우에, 추가 오류 정보는 **SQLGetDiagField,** **SQLGetDiagRec,** 또는 **SQLError**. 그러나 이 정보의 특성과 깊이는 데이터 원본에 따라 다릅니다. 또한 이 정보는 오류로 문을 정확하게 식별할 가능성은 거의 없습니다.
