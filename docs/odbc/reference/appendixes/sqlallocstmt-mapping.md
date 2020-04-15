---
title: SQLAllocStmt 매핑 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305486"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLAllocStmt를** 호출할 때 다음을 호출합니다.  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 다음과 같이 드라이버 관리자에 의해 **SQLAllocHandle에** 매핑됩니다.  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 *입력핸들이* *hdbc및* *OutputHandlePtr로* 설정하여 *phstmt로*설정합니다.
