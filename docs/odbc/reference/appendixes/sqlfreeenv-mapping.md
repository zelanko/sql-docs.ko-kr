---
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
ms.openlocfilehash: 1f56bfeaee32e83ded6d8269873c9c4c33ed434e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302034"
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
