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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1872806265470327f3e7bff468be2ba6d9011421
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792771"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 매핑
응용 프로그램을 호출할 때 **SQLFreeStmt** 사용 하 여는 *옵션* ODBC 3을 통해 SQL_DROP 인수의 *.x* 드라이버에 대 한 호출  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 매핑되는  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 사용 하 여 합니다 *처리할* 인수는 값으로 설정 *hstmt*합니다.
