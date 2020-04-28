---
title: 오류 및 일괄 처리 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300433"
---
# <a name="errors-and-batches"></a>오류 및 일괄 처리
SQL 문의 일괄 처리를 실행 하는 동안 오류가 발생 하면 다음 네 가지 결과 중 하나가 발생할 수 있습니다. 가능한 각 결과는 데이터 원본에 따라 다르며 일괄 처리에 포함 된 문에 따라서도 달라질 수 있습니다.  
  
-   일괄 처리에 문이 실행 되지 않습니다.  
  
-   일괄 처리에 문이 실행 되지 않고 트랜잭션이 롤백됩니다.  
  
-   오류 문 앞의 모든 문이 실행 됩니다.  
  
-   Error 문을 제외한 모든 문이 실행 됩니다.  
  
 처음 두 경우에서 **Sqlexecute** 및 **sqlexecdirect** 는 SQL_ERROR 반환 합니다. 두 번째 경우에는 구현에 따라 SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS를 반환할 수 있습니다. 모든 경우에 **SQLGetDiagField**, **SQLGetDiagRec**또는 **SQLError**를 사용 하 여 추가 오류 정보를 검색할 수 있습니다. 그러나이 정보의 특성과 깊이는 데이터 원본에만 해당 됩니다. 또한이 정보는 오류 메시지를 정확 하 게 식별할 가능성이 없습니다.
