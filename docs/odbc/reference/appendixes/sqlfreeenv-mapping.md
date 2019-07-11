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
ms.openlocfilehash: 6070d7a9d9a7d2eafa35b87c94d6cfd320f916ae
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793575"
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 매핑
응용 프로그램을 호출할 때 **SQLFreeEnv** 는 ODBC를 통한 *3.x* 드라이버에 대 한 호출  
  
```  
SQLFreeEnv(henv)   
```  
  
 매핑되는  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 사용 하 여 합니다 *처리할* 인수는 값으로 설정 *henv*합니다.
