---
description: SQLParamOptions 매핑
title: SQLParamOptions 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLParamOptions
- SQLParamOptions function [ODBC], mapping
ms.assetid: 57ed65f6-9620-4738-b331-19d2a2b5cae4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a2204921708f6eb2ae7a65925d5c858a0020898
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424914"
---
# <a name="sqlparamoptions-mapping"></a>SQLParamOptions 매핑
응용 프로그램에서 ODBC *3.x 드라이버를* 통해 **sqlparamoptions** 를 호출 하는 경우  
  
```  
SQLParamOptions(hstmt, crow, piRow);  
```  
  
 는 다음과 같이 **SQLSetStmtAttr** 의 두 호출로 매핑됩니다.  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, crow, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, piRow, 0);  
```
