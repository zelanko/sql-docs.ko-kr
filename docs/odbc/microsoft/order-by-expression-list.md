---
title: 순서별 식 목록 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 272fa0be844569d322679d444807f8c332b4837b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291223"
---
# <a name="order-by-expression-list"></a>ORDER BY 식 목록
식은 ORDER BY 절에서 사용할 수 있습니다. 예를 들어 다음 절에서 테이블은 a+b, c+d 및 e의 세 가지 키 표현식으로 정렬됩니다.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 집합 함수 또는 집합 함수를 포함하는 식에는 순서가 허용되지 않습니다.
