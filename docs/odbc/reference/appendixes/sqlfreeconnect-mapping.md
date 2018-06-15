---
title: SQLFreeConnect 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d646cc5af246925d89b571734eb967ddc7195676
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906288"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 매핑
응용 프로그램 호출 하는 경우 **SQLFreeConnect** ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 매핑됩니다.  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 와 *처리* 인수에 값으로 설정 *hdbc*합니다.
