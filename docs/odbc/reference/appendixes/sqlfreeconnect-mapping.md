---
title: "SQLFreeConnect 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2695026040f7ac7d258012e502cebd961d5dc7fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 매핑
응용 프로그램 호출 하는 경우 **SQLFreeConnect** ODBC 3*.x* 드라이버에 대 한 호출  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 매핑됩니다.  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 와 *처리* 인수에 값으로 설정 *hdbc*합니다.
