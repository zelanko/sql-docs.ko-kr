---
title: SQLFreeConnect 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20da205d53acbebca1fee12134c04f17fb8b2db3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302044"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **SQLFreeConnect** 를 호출 하는 경우에 대 한 호출이  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 매핑 대상  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 *Handle* 인수가 *hdbc*의 값으로 설정 된입니다.
