---
title: SQLFreeStmt 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72f3924b668750030329e118e7201cbc0ea835d8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 매핑
응용 프로그램 호출 하는 경우 **SQLFreeStmt** 와 *옵션* SQL_DROP ODBC 3에 있는 인수의*.x* 드라이버에 대 한 호출  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 매핑됩니다.  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 와 *처리* 인수에 값으로 설정 *hstmt*합니다.
