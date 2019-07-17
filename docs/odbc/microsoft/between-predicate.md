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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138124"
---
# <a name="between-predicate"></a>BETWEEN 조건자
구문:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 경우 true를 반환 유일한 *expression1* 보다 크거나 같음 *expression2* 하 고 *expression1* 보다 작거나 같음 *expression3*.  
  
 이 구문의 의미 체계 데스크톱 데이터베이스 드라이버 및 Microsoft Jet 엔진에 대 한 서로 다릅니다. Microsoft Jet sql에서 *expression2* 보다 클 수 있습니다 *expression3* 문이 경우에 TRUE를 반환 하는 *expression1* 크거나 같거나 *expression3*, 및 *expression1* 보다 작거나 같음 *expression2*합니다.
