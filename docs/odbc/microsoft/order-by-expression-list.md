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
ms.topic: article
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b0942df15627234e3af07419d272b0eebd2dfec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="order-by-expression-list"></a>ORDER BY 식 목록
식은은 ORDER BY 절에 사용할 수 있습니다. 예를 들어 절에서 테이블 정렬 되는 세 가지 주요 식을 통해: a + b, c + d 및 e입니다.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 순서가 있지 집합 함수 또는 set 함수를 포함 하는 식에서 허용 됩니다.
