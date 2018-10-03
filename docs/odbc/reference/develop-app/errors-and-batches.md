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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61effe29811cc7a8f6e23cbea127b2f757cc7b0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645941"
---
# <a name="errors-and-batches"></a>오류 및 일괄 처리
SQL 문의 일괄 처리를 실행 하는 동안 오류가 발생 하는 경우 다음 네 가지 결과 중 하나가 있을 수 있습니다. (각 가능한 결과 데이터 소스 관련 및 일괄 처리에 포함 된 문에서 따라 달라질 수 있습니다.)  
  
-   일괄 처리에 문이 실행 됩니다.  
  
-   일괄 처리에 문이 실행 되 고 트랜잭션이 롤백됩니다.  
  
-   모든 오류 문 앞에 문을 실행 됩니다.  
  
-   모든 오류 문 제외 하 고 문을 실행 됩니다.  
  
 처음 두 경우에 **SQLExecute** 하 고 **SQLExecDirect** SQL_ERROR를 반환 합니다. 후자의 두 가지 경우 구현에 따라 SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환할 수 있습니다. 모든 경우에 추가 오류 정보를 검색할 있습니다 사용 하 여 **SQLGetDiagField**하십시오 **SQLGetDiagRec**, 또는 **SQLError**합니다. 그러나 특성 및이 정보의 깊이 데이터 소스 관련 됩니다. 또한이 정보는 정확 하 게 문이 오류에서를 식별 하는 일을 할 수 없습니다.
