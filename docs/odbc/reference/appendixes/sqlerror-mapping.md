---
title: SQLError 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 577f07c6839ebd4b8fe2b9722fde3595bb7e70dd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlerror-mapping"></a>SQLError 매핑
응용 프로그램 호출 하는 경우 **SQLError** ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 매핑됩니다.  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 와 *HandleType* 를 적절 하 게 SQL_HANDLE_ENV, sql_handle_dbc 라는, 또는 여를 값으로 설정 하는 인수 및 *처리* 인수에 값으로 설정 *henv*, *hdbc*, 또는 *hstmt*를 적절 하 게 합니다. *RecNumber* 인수 드라이버 관리자에 의해 결정 됩니다.
