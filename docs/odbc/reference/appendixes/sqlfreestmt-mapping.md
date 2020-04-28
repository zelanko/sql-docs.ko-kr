---
title: SQLFreeStmt 매핑 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302014"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 SQL_DROP의 *Option* 인수를 사용 하 여 **SQLFreeStmt** 를 호출 하는 경우에 대 한 호출은  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 매핑 대상  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 *핸들* 인수가 *hstmt*의 값으로 설정 된입니다.
