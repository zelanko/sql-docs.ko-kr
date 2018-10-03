---
title: SQLTransact 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5cf669883ce81528adbe1fbd8faeff2ed716218
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656187"
---
# <a name="sqltransact-mapping"></a>SQLTransact 매핑
**SQLTransact** 이제 바뀝니다 **SQLEndTran**합니다. 두 함수 간의 주요 차이점은 **SQLEndTran** 인수로 포함 *HandleType*를 수행 해야 하는 작업의 범위를 지정 하는 합니다. 합니다 *HandleType* 인수 환경 또는 연결 핸들을 지정할 수 있습니다. 다음에 호출할 **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 매핑되는  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 하는 경우 *ConnectionHandle* SQL_NULL_HDBC와 같지 않습니다. 합니다 *ConnectionHandle* 인수를 값으로 설정 됩니다 *hdbc*합니다.  
  
 **SQL_Transact** 에 매핑된  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 하는 경우 *ConnectionHandle* SQL_NULL_HDBC 같습니다. 합니다 *EnvironmentHandle* 인수를 값으로 설정 됩니다 *henv*합니다.  
  
 이전 사례와 둘 다에 *CompletionType* 인수를 동일한 값으로 설정 됩니다 *fType*합니다.
