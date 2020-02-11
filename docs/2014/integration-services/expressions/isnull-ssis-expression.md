---
title: ISNULL(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: df3612392859a8b7ed6301587cf4d630b2fecf4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769149"
---
# <a name="isnull-ssis-expression"></a>ISNULL(SSIS 식)
  식이 Null인지 여부에 따라 부울 결과를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ISNULL(expression)  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 임의 데이터 형식의 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_BOOL  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 **DiscontinuedDate** 열에 Null 값이 포함되어 있을 경우 TRUE를 반환합니다.  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 이 예에서는 **LastName** 열에 Null 값이 포함되어 있을 경우 "Unknown last name"을 반환합니다. 그렇지 않으면 **LastName**이 반환됩니다.  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 이 예에서는 **DaysToManufacture** 열에 Null 값이 포함되어 있을 경우 **AddDays**변수 값에 관계없이 항상 TRUE를 반환합니다.  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](functions-ssis-expression.md)   
 [COALESCE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/coalesce-transact-sql)  
  
  
