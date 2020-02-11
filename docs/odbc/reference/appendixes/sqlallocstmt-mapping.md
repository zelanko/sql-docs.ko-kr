---
title: SQLAllocStmt 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf79d3ef813e87e785cea588cfc1d6e3eed44ee4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064987"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 매핑
응용 프로그램에서 ODBC *3.x 드라이버를* 통해 **sqlallocstmt** 를 호출 하는 경우에 대 한 호출을 수행 합니다.  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 드라이버 관리자는 다음과 같이 **SQLAllocHandle** 에 매핑됩니다.  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 *InputHandle* 를 *hdbc* 로 설정 하 고 *OutputHandlePtr* 를 *phstmt*로 설정 합니다.
