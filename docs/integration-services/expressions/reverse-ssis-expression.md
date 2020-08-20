---
description: REVERSE(SSIS 식)
title: REVERSE(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 250f4a865ac488614459350ee42698d8dbb003fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477457"
---
# <a name="reverse-ssis-expression"></a>REVERSE(SSIS 식)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  문자 식을 역 순서로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 되돌릴 문자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>설명  
 *character_expression* DT_WSTR 데이터 형식이어야 합니다.  
  
 *character_expression* 이 null인 경우 REVERSE가 null 결과를 반환합니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 문자열 리터럴을 사용합니다. 반환 결과는 "ekiB niatnuoM"입니다.  
  
```  
REVERSE("Mountain Bike")  
```  
  
 이 예에서는 변수를 사용합니다. **Name** 이 Touring Bike이면 반환 결과는 "ekiB gniruoT"입니다.  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
