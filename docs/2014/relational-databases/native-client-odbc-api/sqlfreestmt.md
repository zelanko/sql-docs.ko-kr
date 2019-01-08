---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7e597bcfa80d7d45064c844986018d64617d5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359805"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  ODBC 3.0 이상에서는**SQLFreeStmt** 가 권장되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *SQLFreeStmt* 에 대해 정의된 모든 **Option**값을 지원합니다. 하지만 [SQLFreeStmt](sqlclosecursor.md)의 기능을 대체하거나 동일한 기능을 수행하는 [SQLCloseCursor](sqlbindparameter.md), [SQLBindParameter](sqlbindcol.md), **SQLBindCol**, [SQLSetDescField](sqlfreehandle.md) 및 **SQLFreeHandle** 을 대신 사용해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLFreeStmt 함수](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
