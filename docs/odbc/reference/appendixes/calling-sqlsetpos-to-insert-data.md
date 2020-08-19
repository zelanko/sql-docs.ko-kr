---
description: SQLSetPos를 호출하여 데이터 삽입
title: SQLSetPos를 호출 하 여 데이터 삽입 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 215d02e9b5bd92f6a22f7e45c8c29c7c5a0a6a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449015"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>SQLSetPos를 호출하여 데이터 삽입
Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.x 응용 프로그램이* SQL_ADD의 *작업* 인수를 사용 하 여 **SQLSetPos** 를 호출 하면 드라이버 관리자는이 호출을 **SQLBulkOperations**에 매핑하지 않습니다. ODBC 3.x 드라이버가 SQL_ADD를 사용 하 여 **SQLSetPos** 를 호출 하는 응용 프로그램에서 작동 해야 하는 경우 드라이버에서 해당 작업을 지원 해야 *합니다.*  
  
 **SQLSetPos** 를 호출할 때 동작의 한 가지 주요 차이점은 S6 상태에서 호출 될 때 SQL_ADD 발생 합니다. ODBC 2.x에서 드라이버가 **Sqlfetch**를 사용 하 여 커서가 배치 된 후에 상태 S6에서 SQL_ADD를 사용 하 여 **SQLSetPos** *를 호출*하면 드라이버가 S1010를 반환 했습니다. ODBC 3.x에서 SQL_ADD *작업* *을 사용*하는 **SQLBulkOperations** 는 S6 상태에서 호출할 수 있습니다. 두 번째 주요 차이점은 SQL_ADD *작업* 을 사용 하는 **SQLBulkOperations** 은 S5 상태에서 호출 될 수 있지만, SQL_ADD **작업** 을 사용 하는 **SQLSetPos** 는 사용할 수 없다는 것입니다. ODBC 3.x에서 동일한 호출에 대해 발생할 수 있는 문 전환의 *경우* [부록 B: Odbc 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.
