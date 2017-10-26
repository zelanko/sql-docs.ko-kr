---
title: "조건자 사이 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8daaa0e1c26f00acbff2e6f7788eab8ee5ac8ce
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="between-predicate"></a>조건자 사이
구문:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 경우 true를 반환만 *expression1* 보다 크거나 같음 *expression2* 및 *expression1* 보다 작거나 같음 *expression3*.  
  
 이 구문의 의미 체계는 데스크톱 데이터베이스 드라이버 및 Microsoft Jet 엔진에서 서로 다릅니다. Microsoft Jet SQL에서 *expression2* 보다 클 수 *expression3* 문이 경우에 TRUE를 반환 되도록 *expression1* 보다크거나같은경우는*expression3*, 및 *expression1* 보다 작거나 같음 *expression2*합니다.

