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
manager: craigg
ms.openlocfilehash: 330c245d8b5839fd8a721a7399a22edea78a2417
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63269950"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 매핑
응용 프로그램을 호출할 때 **SQLAllocStmt** 는 ODBC 3 *.x* 드라이버, 호출:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 에 매핑된 **SQLAllocHandle** 같이 드라이버에서 드라이버 관리자에서:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 사용 하 여 *InputHandle* 로 설정 *hdbc* 하 고 *OutputHandlePtr* 로 *phstmt*합니다.
