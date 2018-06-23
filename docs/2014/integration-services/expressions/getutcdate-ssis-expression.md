---
title: GETUTCDATE(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 091063acbaea65d155e578ff6a4c21c95d941a39
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088878"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE(SSIS 식)
  DT_DBTIMESTAMP 형식을 사용하여 현재 시스템 날짜를 UTC 시간(국제 표준시 또는 그리니치 표준시)으로 반환합니다. GETUTCDATE 함수는 인수가 필요 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>인수  
 InclusionThresholdSetting  
  
## <a name="result-types"></a>결과 형식  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 현재 날짜의 연도가 UTC 시간으로 반환됩니다.  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 이 예에서는 **ModifiedDate** 열의 날짜와 현재 UTC 날짜 사이의 일 수가 반환됩니다.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 이 예에서는 현재 UTC 날짜에 3개월을 더합니다.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>관련 항목  
 [GETDATE &#40;SSIS 식&#41;](getdate-ssis-expression.md)   
 [함수 &#40;SSIS 식&#41;](functions-ssis-expression.md)  
  
  