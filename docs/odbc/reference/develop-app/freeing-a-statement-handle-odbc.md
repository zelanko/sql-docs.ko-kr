---
title: 문 핸들을 해제 하는 방법 ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305618"
---
# <a name="freeing-a-statement-handle-odbc"></a>명령문 핸들 ODBC 해제
앞서 언급 했 듯이 문을 삭제 하 고 새 문을 할당 하는 것 보다 문을 다시 사용 하는 것이 더 효율적입니다. 문에 대해 새 SQL 문을 실행 하기 전에 응용 프로그램에서 현재 문 설정이 적절 한지를 알아야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 일반적으로 이전 SQL 문에 대 한 매개 변수 및 결과 집합은 바인딩 해제 되어야 합니다 (SQL_RESET_PARAMS 및 SQL_UNBIND 옵션을 사용 하 여 **SQLFreeStmt** 호출) 하 고 새 sql 문에 대해 바인딩 해제 해야 합니다.  
  
 응용 프로그램에서 문 사용을 마치면 **Sqlfreehandle** 을 호출 하 여 문을 해제 합니다. 문을 해제 한 후에는 ODBC 함수 호출에서 문의 핸들을 사용 하는 응용 프로그램 프로그래밍 오류가 발생 합니다. 이렇게 하면 정의 되지 않았지만 심각한 결과가 발생할 수 있습니다.  
  
 **Sqlfreehandle** 을 호출 하면 드라이버는 문에 대 한 정보를 저장 하는 데 사용 되는 구조를 해제 합니다.  
  
 **Sqldisconnect** 는 연결에서 모든 문을 자동으로 해제 합니다.
