---
title: SQLTransact 매핑 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304884"
---
# <a name="sqltransact-mapping"></a>SQLTransact 매핑
**SQLTransact는** 이제 **SQLEndTran로**대체됩니다. 두 함수의 주요 차이점은 **SQLEndTran에** 수행할 작업의 범위를 지정하는 *인수 핸들Type이*포함되어 있다는 것입니다. *HandleType* 인수는 환경 또는 연결 핸들을 지정할 수 있습니다. **SQLTransact에**대한 다음 호출 :  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 매핑됩니다.  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 *연결핸들이* SQL_NULL_HDBC 같지 않은 경우. *연결핸들* 인수는 *hdbc의*값으로 설정됩니다.  
  
 **SQL_Transact** 매핑됩니다.  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 *연결핸들이* SQL_NULL_HDBC 것과 같다면 *환경 핸들* 인수는 *henv의*값으로 설정됩니다.  
  
 앞의 두 경우 *모두에서 CompletionType* 인수는 *fType*과 동일한 값으로 설정됩니다.
