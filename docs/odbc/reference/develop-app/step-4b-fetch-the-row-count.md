---
description: '4b단계: 행 수 페치'
title: '4b 단계: 행 개수 가져오기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eab5e1e1bf7eba70e2d84b36349e2f982a0b14c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494606"
---
# <a name="step-4b-fetch-the-row-count"></a>4b단계: 행 수 페치
다음 단계는 다음 그림과 같이 행 개수를 인출 하는 것입니다.  
  
 ![행의 수를 페치하는 방법](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 3 단계에서 실행 된 문이 **UPDATE**, **DELETE**또는 **INSERT** 문인 경우 응용 프로그램은 **sqlrowcount**를 사용 하 여 영향을 받는 행 수를 검색 합니다. 자세한 내용은 [영향을 받는 행 수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)을 참조 하세요.  
  
 이제 응용 프로그램은 3 단계로 돌아와서 동일한 트랜잭션에서 다른 문을 실행 하거나 5 단계로 진행 하 여 트랜잭션을 커밋하거나 롤백합니다.
