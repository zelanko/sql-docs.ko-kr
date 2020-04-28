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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283860"
---
# <a name="between-predicate"></a>BETWEEN 조건자
구문은 다음과 같습니다:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 *expression1* 가 *식 2* 보다 크거나 같고 *expression1* 가 *expression3*보다 작거나 같은 경우에만 true를 반환 합니다.  
  
 이 구문의 의미 체계는 데스크톱 데이터베이스 드라이버 및 Microsoft Jet 엔진과 다릅니다. Microsoft Jet SQL에서 *식 2* 는 *expression3* 보다 클 수 있으므로 *expression1* 가 *expression3*보다 크거나 같고 *expression1* 가 *식 2*보다 작거나 같은 경우에만 문이 TRUE를 반환 합니다.
