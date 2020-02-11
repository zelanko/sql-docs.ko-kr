---
title: BETWEEN 조건자 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a0ac99729966acdcb03c2aab0175c34bba0c08a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138124"
---
# <a name="between-predicate"></a>BETWEEN 조건자
구문은 다음과 같습니다:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 *expression1* 가 *식 2* 보다 크거나 같고 *expression1* 가 *expression3*보다 작거나 같은 경우에만 true를 반환 합니다.  
  
 이 구문의 의미 체계는 데스크톱 데이터베이스 드라이버 및 Microsoft Jet 엔진과 다릅니다. Microsoft Jet SQL에서 *식 2* 는 *expression3* 보다 클 수 있으므로 *expression1* 가 *expression3*보다 크거나 같고 *expression1* 가 *식 2*보다 작거나 같은 경우에만 문이 TRUE를 반환 합니다.
