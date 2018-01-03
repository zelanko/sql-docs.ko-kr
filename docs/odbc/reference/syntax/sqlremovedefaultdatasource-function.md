---
title: "SQLRemoveDefaultDataSource 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRemoveDefaultDataSource
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveDefaultDataSource
helpviewer_keywords: SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cba3b817fe4ec42ccf50682e504abe0783fd74ce
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 함수
**규칙**  
 ODBC 버전에 도입 된: 1.0에서 사용 되지 않습니다  
  
 **요약**  
 ODBC 3.0에서는 **SQLRemoveDefaultDataSource** 함수에 대 한 호출으로 대체 되었습니다 [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) 와 *문제점과* ODBC_REMOVE_DEFAULT_DSN의 인수입니다. ODBC 2 경우*.x* 이 함수를 호출 하는 설치 프로그램을 ODBC 설치 관리자는 그 다음에 매핑됩니다 **SQLConfigDataSource** 호출:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
