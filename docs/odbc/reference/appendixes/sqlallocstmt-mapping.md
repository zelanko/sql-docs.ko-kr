---
description: SQLAllocStmt 매핑
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
ms.openlocfilehash: e8307dce9e95c98ff92912517d5b574883d6298c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424925"
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
