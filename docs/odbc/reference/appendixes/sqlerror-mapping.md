---
title: SQL오류 매핑 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302081"
---
# <a name="sqlerror-mapping"></a>SQLError 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLError를** 호출할 때  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 매핑됩니다.  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 *handleType* 인수는 SQL_HANDLE_ENV, SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT 값으로 설정하고 핸들 *인수는* *henv,* *hdbc*또는 *hstmt의*값으로 적절히 설정됩니다. *RecNumber* 인수는 드라이버 관리자에 의해 결정됩니다.
