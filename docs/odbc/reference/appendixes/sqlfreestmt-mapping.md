---
title: "SQLFreeStmt 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: df3cfba17f19074fbe00f33ef7fba098a4fe8184
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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

