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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aaa056fca860a70f81ad7c3a4cd8539512bc25d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304884"
---
# <a name="sqltransact-mapping"></a>SQLTransact 매핑
**Sqltransact** 은 이제 **sqlendtran**로 대체 되었습니다. 두 함수 간의 주요 차이점은 **Sqlendtran** 에는 수행할 작업의 범위를 지정 하는 *HandleType*인수가 포함 되어 있다는 것입니다. *HandleType* 인수는 환경 또는 연결 핸들을 지정할 수 있습니다. **Sqltransact**에 대 한 다음 호출입니다.  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 매핑 대상  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 *ConnectionHandle* 가 SQL_NULL_HDBC와 같지 않은 경우 *ConnectionHandle* 인수는 *hdbc*의 값으로 설정 됩니다.  
  
 **SQL_Transact** 매핑 대상  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 *ConnectionHandle* 가 SQL_NULL_HDBC와 같으면입니다. *EnvironmentHandle* 인수는 *henv*의 값으로 설정 됩니다.  
  
 위의 두 경우 모두, 나머지 *형식* 인수는 *fType*과 동일한 값으로 설정 됩니다.
