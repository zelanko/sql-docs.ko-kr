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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c1ab12a975d7b9c0aba77db9af31accac398a16
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199408"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 매핑
응용 프로그램을 호출할 때 **SQLFreeEnv** 는 ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLFreeEnv(henv)   
```  
  
 매핑되는  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 사용 하 여 합니다 *처리할* 인수는 값으로 설정 *henv*합니다.
