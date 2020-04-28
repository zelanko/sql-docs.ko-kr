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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 447233a3ba014a5ef92f2f49840ad302f8aeccf0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305486"
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
