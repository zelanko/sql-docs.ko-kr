---
description: BETWEEN 조건자
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
ms.openlocfilehash: 2f2283f5824e4be0c9702bfe8feef9fe3109849a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500386"
---
# <a name="between-predicate"></a>BETWEEN 조건자
구문은 다음과 같습니다:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 *expression1* 가 *식 2* 보다 크거나 같고 *expression1* 가 *expression3*보다 작거나 같은 경우에만 true를 반환 합니다.  
  
 이 구문의 의미 체계는 데스크톱 데이터베이스 드라이버 및 Microsoft Jet 엔진과 다릅니다. Microsoft Jet SQL에서 *식 2* 는 *expression3* 보다 클 수 있으므로 *expression1* 가 *expression3*보다 크거나 같고 *expression1* 가 *식 2*보다 작거나 같은 경우에만 문이 TRUE를 반환 합니다.
