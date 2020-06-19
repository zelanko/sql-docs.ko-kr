---
title: REPLACENULL(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 31b228ac01c3e687b2fa0e5df5758d9a942fa6ee
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969123"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL(SSIS 식)
  첫 번째 식 매개 변수의 값이 NULL이면 두 번째 식 매개 변수의 값을 반환하고, 그렇지 않으면 첫 번째 식의 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>인수  
 *expression 1*  
 이 식의 결과를 NULL과 비교합니다.  
  
 *expression 2*  
 첫 번째 식이 NULL로 평가되면 이 식의 결과가 반환됩니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_WSTR  
  
## <a name="remarks"></a>설명  
  
-   *expression 2* 길이는 0이 될 수 있습니다.  
  
-   인수가 Null이면 REPLACENULL은 Null을 반환합니다.  
  
-   BLOB 열(DT_TEXT, DT_NTEXT, DT_IMAGE)은 이 두 매개 변수에 대해 지원되지 않습니다.  
  
-   두 식은 반환 형식이 동일해야 합니다. 동일하지 않으면 함수가 두 번째 식을 첫 번째 식의 반환 형식으로 캐스팅하려고 하므로 데이터 형식이 호환되지 않는 경우 오류가 발생할 수 있습니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 예에서는 데이터베이스 열의 NULL 값을 문자열(1900-01-01)로 대체합니다. 이 함수는 특히 NULL 값을 다른 값으로 바꾸려는 공용 파생 열 패턴에 사용됩니다.  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]  
>  다음 예에서는 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]에서 이 함수를 사용하는 방법을 보여 줍니다.  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? "1900-01-01" : MyColumn)   
```  
  
  
