---
title: SQLFreeEnv 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0e17b07e842960908bf7ac306d09f1aa46ff157
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 매핑
응용 프로그램 호출 하는 경우 **SQLFreeEnv** ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLFreeEnv(henv)   
```  
  
 매핑됩니다.  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 와 *처리* 인수에 값으로 설정 *henv*합니다.
