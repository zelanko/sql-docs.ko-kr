---
title: SQLTransact 매핑 | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e938a4eb7c605d1ed9cf71c038bcc7187e1a8cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqltransact-mapping"></a>SQLTransact 매핑
**SQLTransact** 이제 바뀝니다 **SQLEndTran**합니다. 두 함수 간의 주요 차이점은 **SQLEndTran** 인수가 포함 되어 *HandleType*를 수행 해야 하는 작업의 범위를 지정 하는 합니다. *HandleType* 인수 환경 또는 연결 핸들을 지정할 수 있습니다. 다음에 대 한 호출 **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 매핑됩니다.  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 경우 *ConnectionHandle* SQL_NULL_HDBC 같지 않습니다. *ConnectionHandle* 인수 값으로 설정 되어 *hdbc*합니다.  
  
 **SQL_Transact** 매핑됩니다  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 경우 *ConnectionHandle* SQL_NULL_HDBC 같습니다. *EnvironmentHandle* 인수 값으로 설정 되어 *henv*합니다.  
  
 위의 경우 모두는 *CompletionType* 인수는 동일한 값으로 설정 되어 *fType*합니다.
