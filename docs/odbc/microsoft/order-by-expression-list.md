---
title: ORDER BY 식 목록 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f210642f14b945ee62bd4eba3d1a722d8b8e11c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="order-by-expression-list"></a>ORDER BY 식 목록
식은은 ORDER BY 절에 사용할 수 있습니다. 예를 들어 절에서 테이블 정렬 되는 세 가지 주요 식을 통해: a + b, c + d 및 e입니다.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 순서가 있지 집합 함수 또는 set 함수를 포함 하는 식에서 허용 됩니다.
