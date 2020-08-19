---
description: SQLFreeEnv 매핑
title: SQLFreeEnv 매핑 | Microsoft Docs
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
ms.openlocfilehash: 1c3ccbf3175c7f17d06b55799463fb7115997e01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421497"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **sqlfreeenv** 를 호출 하는 경우에 대 한 호출이  
  
```  
SQLFreeEnv(henv)   
```  
  
 매핑 대상  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 *Handle* 인수가 *henv*의 값으로 설정 된입니다.
