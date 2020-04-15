---
title: 술어 사이 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283860"
---
# <a name="between-predicate"></a>BETWEEN 조건자
구문은 다음과 같습니다:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 *expression1이* *식2보다* 크거나 같고 *식1이* *식3보다*크거나 같을 때만 true를 반환합니다.  
  
 이 구문의 의미 체계는 데스크톱 데이터베이스 드라이버와 Microsoft Jet 엔진에 대해 다릅니다. Microsoft Jet SQL에서 *식2는* *식1이* *식3보다* 크거나 같을 때만 true를 *expression3*반환하고 식1은 *식2보다*크거나 같을 수 있도록 *식2보다* 클 수 있습니다.
