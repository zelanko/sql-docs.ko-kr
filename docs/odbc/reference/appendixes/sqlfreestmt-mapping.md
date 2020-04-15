---
title: SQLFreeStmt 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d187db4d40132385b9ae4564fddbf89987e3e97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302014"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 SQL_DROP *옵션* 인수로 **SQLFreeStmt를** 호출하면  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 매핑됩니다.  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 *핸들* 인수를 *hstmt의*값으로 설정합니다.
