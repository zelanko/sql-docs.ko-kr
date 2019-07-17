---
title: ORDER BY 식 목록 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100788"
---
# <a name="order-by-expression-list"></a>ORDER BY 식 목록
식은은 ORDER BY 절에서 사용할 수 있습니다. 예를 들어, 다음 절에서 테이블 정렬 되 세 가지 키 식에 의해: a + b, c + d 및 e입니다.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 정렬 안 함은 집합 함수 또는 set 함수를 포함 하는 식에서 허용 됩니다.
