---
description: SQLRemoveDefaultDataSource 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0010e59cc4dfad2d54b8b1c4e59e83ea72fcd3ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487091"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 함수
**규칙**  
 소개 된 버전: ODBC 1.0, 사용 되지 않음  
  
 **요약**  
 ODBC 3.0에서 **Sqlremovedefaultdatasource** 함수는 ODBC_REMOVE_DEFAULT_DSN의 *frequest* 인수를 사용 하 여 [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) 에 대 한 호출로 대체 되었습니다. ODBC 2.x 설치 프로그램에서이 함수를 호출 하면*odbc 설치 관리자* 가 다음 **SQLConfigDataSource** 호출에 매핑합니다.  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
