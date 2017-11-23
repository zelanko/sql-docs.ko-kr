---
title: "오류 및 일괄 처리 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f00a70ec411824da13d37666c7b22f92248a236
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="errors-and-batches"></a>오류 및 일괄 처리
SQL 문의 일괄 처리를 실행 하는 동안 오류가 발생 하는 경우 다음 네 가지 결과 중 하나 작성할 수 있으며 (각 가능한 결과 데이터 원본에 따른 특정 및 일괄 처리에 포함 된 문을에 종속 될 수 있습니다.)  
  
-   일괄 처리에 문이 없습니다 실행 됩니다.  
  
-   일괄 처리에 문이 없습니다 실행 되 고 트랜잭션이 롤백됩니다.  
  
-   모든 오류 문 앞에 문은 실행 됩니다.  
  
-   모든 문을 error 문 제외 하 고 실행 됩니다.  
  
 처음 두 가지 경우에서 **SQLExecute** 및 **SQLExecDirect** SQL_ERROR를 반환 합니다. 후자의 두 가지 경우에는 구현에 따라 SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환할 수 있습니다. 모든 경우에 추가 오류 정보 수를 검색할 수와 **SQLGetDiagField**, **SQLGetDiagRec**, 또는 **SQLError**합니다. 그러나 특성 및 자세한이이 정보는 데이터 원본에 따른 특정입니다. 또한이 정보가 어렵습니다 오류가 문을 정확 하 게 식별 합니다.
