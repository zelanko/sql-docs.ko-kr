---
title: ROUND(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4b59e8f0256cba7e747ac6ee41d7e4e2fdf9feb1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967928"
---
# <a name="round-ssis-expression"></a>ROUND(SSIS 식)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  특정 길이나 전체 자릿수로 반올림한 숫자 식을 반환합니다. 길이 매개 변수는 정수여야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 유효한 숫자 유형의 식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 *length*  
 정수 식입니다. *numeric_expression* 을 반올림할 전체 자릿수입니다.  
  
## <a name="result-types"></a>결과 형식  
 *numeric*_*expression*과 동일한 형식입니다.  
  
## <a name="remarks"></a>Remarks  
 *length* 인수는 양의 정수이거나 0이어야 합니다.  
  
 인수가 Null이면 ROUND 결과도 Null입니다.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 리터럴을 길이 3으로 반올림합니다. 첫 번째 반환 결과는 137.1570이고 두 번째 반환 결과는 137.1580입니다.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>참고 항목  
 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
