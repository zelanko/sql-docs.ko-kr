---
title: "SQLParamOptions 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLParamOptions
- SQLParamOptions function [ODBC], mapping
ms.assetid: 57ed65f6-9620-4738-b331-19d2a2b5cae4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce00768c82299f17546aac2d9c01eea32f8841f1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlparamoptions-mapping"></a>SQLParamOptions 매핑
응용 프로그램 호출 하는 경우 **SQLParamOptions** ODBC 3*.x* 드라이버, 호출  
  
```  
SQLParamOptions(hstmt, crow, piRow);  
```  
  
 두 번의 호출으로 매핑될 **SQLSetStmtAttr** 다음과 같습니다.  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, crow, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, piRow, 0);  
```

