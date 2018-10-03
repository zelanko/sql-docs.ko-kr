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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a278609ee53fe7898d32c1986da2650202b8a98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719211"
---
# <a name="sqlerror-mapping"></a>SQLError 매핑
응용 프로그램을 호출할 때 **SQLError** 는 ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 매핑되는  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 사용 하 여는 *HandleType* 인수를 적절 하 게 SQL_HANDLE_ENV, SQL_HANDLE_DBC를 호출 하 여, 값으로 설정 하며 *처리* 인수 값으로 설정 *henv*하십시오 *hdbc*, 또는 *hstmt*를 적절 하 게 합니다. 합니다 *RecNumber* 인수 드라이버 관리자에 의해 결정 됩니다.
