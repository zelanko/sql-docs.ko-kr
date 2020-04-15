---
title: SQLFreeEnv 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f56bfeaee32e83ded6d8269873c9c4c33ed434e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302034"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLFreeEnv를** 호출하면  
  
```  
SQLFreeEnv(henv)   
```  
  
 매핑됩니다.  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 *핸들* 인수를 *henv의*값으로 설정합니다.
