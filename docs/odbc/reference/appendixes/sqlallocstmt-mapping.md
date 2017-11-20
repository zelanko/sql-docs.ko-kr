---
title: "SQLAllocStmt 매핑 | Microsoft Docs"
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
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8361f0b77e8f15f775eece7aae9b599be5e62ac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 매핑
응용 프로그램 호출 하는 경우 **SQLAllocStmt** ODBC 3*.x* 드라이버에 대 한 호출:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 에 매핑된 **SQLAllocHandle** 드라이버 관리자가 다음과 같이 드라이버에서:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 와 *InputHandle* 로 설정 *hdbc* 및 *OutputHandlePtr* 로 설정 *phstmt*합니다.

