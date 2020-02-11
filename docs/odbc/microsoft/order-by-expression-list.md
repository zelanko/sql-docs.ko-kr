---
title: ORDER BY 식-목록 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cd88673c4b5309b7463256b85df4f92d6d360b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100788"
---
# <a name="order-by-expression-list"></a>ORDER BY 식 목록
ORDER BY 절에 식을 사용할 수 있습니다. 예를 들어 다음 절에서 테이블은 a + b, c + d 및 e의 세 가지 주요 식으로 정렬 됩니다.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 집합 함수 또는 set 함수를 포함 하는 식에는 정렬을 사용할 수 없습니다.
