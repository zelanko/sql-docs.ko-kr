---
title: SQLRemoveDefault데이터소스 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 952ace7d17e8bb5b4c824761b02e5c8a0895f519
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303944"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 함수
**규칙**  
 버전 소개: ODBC 1.0, 더 이상 사용되지 않습니다.  
  
 **요약**  
 ODBC 3.0에서 **SQLRemoveDefaultDataSource** 함수는 ODBC_REMOVE_DEFAULT_DSN *fRequest* 인수와 [함께 SQLConfigDataSource에](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) 대한 호출로 대체되었습니다. ODBC 2 *.x* 설치 프로그램이 이 함수를 호출하는 경우 ODBC 설치 프로그램은 다음 **SQLConfigDataSource** 호출에 매핑됩니다.  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
