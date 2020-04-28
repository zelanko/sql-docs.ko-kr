---
title: SQLError 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa3b66b29af755099cb273f3a19ca4e8230cd0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302081"
---
# <a name="sqlerror-mapping"></a>SQLError 매핑
응용 프로그램 *에서 ODBC 3.x* 드라이버를 통해 **SQLError** 를 호출 하는 경우  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 매핑 대상  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 *HandleType* 인수를 SQL_HANDLE_ENV 값으로 설정 하 고, SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT 하 고, 적절 하 게 *henv*, *hdbc*또는 *hstmt*의 값으로 *핸들* 인수를 설정 합니다. 지 *수* 인수는 드라이버 관리자에 의해 결정 됩니다.
