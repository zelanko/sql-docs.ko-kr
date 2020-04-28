---
title: SQL 문의 상호 운용성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3d7a76c67096d2e76fe1cd3d4b15f73122699e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302804"
---
# <a name="interoperability-of-sql-statements"></a>SQL 문의 상호 운용성
응용 프로그램의 나머지와 마찬가지로 SQL 문은 상호 운용할 수 있거나 DBMS에 한정 될 수 있습니다. 응용 프로그램의 나머지 부분과 마찬가지로, 상호 운용 가능한 SQL 문이 응용 프로그램의 유형에 따라 달라 지는 방식을 선택 해야 합니다. 사용자 지정 응용 프로그램은 일반적으로 하나 또는 두 개의 Dbms 기능을 사용 하도록 설계 되었으므로 상호 운용 가능한 SQL 문을 사용 하는 것이 더 적습니다. 제네릭 응용 프로그램은 다양 한 Dbms에서 작동 하도록 설계 되었으므로 상호 운용할 수 있는 SQL 문을 사용 합니다. 및 수직 응용 프로그램은 일반적으로 특정 수준의 기능을 요구 하지만, 상호 운용 가능한 SQL 문을 사용 하는 경우에도 해당 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문법 선택](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [상호 운용 가능한 SQL 문 생성](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
