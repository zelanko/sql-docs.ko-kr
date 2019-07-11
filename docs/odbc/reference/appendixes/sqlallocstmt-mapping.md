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
ms.openlocfilehash: 1139d87d9f97a3d63236c03e7cf4ced787ad8e85
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793547"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 매핑
응용 프로그램을 호출할 때 **SQLAllocStmt** 는 ODBC를 통한 *3.x* 드라이버, 호출 합니다.  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 에 매핑된 **SQLAllocHandle** 같이 드라이버에서 드라이버 관리자에서:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 사용 하 여 *InputHandle* 로 설정 *hdbc* 하 고 *OutputHandlePtr* 로 *phstmt*합니다.
