---
title: SQLRemoveDefaultDataSource 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea540d2ef6747bbe3bfc9ac55f04afe1d63349f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537238"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 함수
**규칙**  
 도입 된 버전: ODBC 1.0에서 사용 되지 않음  
  
 **요약**  
 ODBC 3.0에서 합니다 **SQLRemoveDefaultDataSource** 함수에 대 한 호출으로 대체 되었습니다 [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) 사용 하 여는 *문제점과* ODBC_REMOVE_DEFAULT_DSN의 인수입니다. 경우는 ODBC 2 *.x* 이 함수를 호출 하는 설치 프로그램을 ODBC 설치 관리자는 다음 매핑할 것 **SQLConfigDataSource** 호출 합니다.  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
