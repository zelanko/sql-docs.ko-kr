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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b9a35275d95207fd8ceef296ecda4664a1c4e7f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793598"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 매핑
응용 프로그램을 호출할 때 **SQLFreeConnect** 는 ODBC를 통한 *3.x* 드라이버에 대 한 호출  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 매핑되는  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 사용 하 여 합니다 *처리할* 인수는 값으로 설정 *hdbc*합니다.
