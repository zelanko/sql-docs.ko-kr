---
title: 숫자 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- integer data types [Integration Services]
- numeric data formats for fast parse
- locale-sensitive parsing [Integration Services]
- fast parse [Integration Services]
ms.assetid: fa3975ce-9d21-408a-857d-f85e30af27b0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0096f34a5815237ed3865e298ecc628083ce408
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424510"
---
# <a name="numeric-data-formats"></a>숫자 데이터 형식
  빠른 구문 분석에서는 데이터 구문 분석을 위해 로캘을 구분하지 않는 신속하고 간단한 루틴을 제공합니다. 빠른 구문 분석은 일부 제한된 정수 데이터 형식만 지원합니다.  
  
## <a name="integer-data-types"></a>정수 데이터 형식  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 제공되는 정수 데이터 형식은 DT_I1, DT_UI1, DT_I2, DT_UI2, DT_I4, DT_UI4, DT_I8 및 DT_UI8입니다. 자세한 내용은 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조 하세요.  
  
 빠른 구문 분석에서는 정수 데이터에 대해 다음과 같은 형식이 지원됩니다.  
  
-   0개 이상의 선행 및 후행 공백이나 탭 정지. 예를 들어 "  123  "은 유효한 값입니다. 공백으로만 이뤄진 값은 0으로 계산됩니다.  
  
-   선행 더하기 기호, 빼기 기호 또는 아무 기호도 사용되지 않음. 예를 들어 +123, -123 및 123은 유효한 값입니다.  
  
-   하나 이상의 힌두-아라비아 숫자(0-9). 예를 들어 345는 유효한 값입니다. 다른 언어의 숫자는 지원되지 않습니다.  
  
 지원되지 않는 데이터 형식은 다음과 같습니다.  
  
-   특수 문자. 예를 들어 통화 문자 $는 지원되지 않으며 $20 값은 구문 분석할 수 없습니다.  
  
-   줄 바꿈, 캐리지 리턴 및 줄 바꿈하지 않는 공백과 같은 공백 문자. 예를 들어 "123" 값은 구문 분석할 수 없습니다.  
  
-   정수의 16진 표시. 예를 들어 2EE 값은 구문 분석할 수 없습니다.  
  
-   정수의 공학 표시. 예를 들어 1E+10 값은 구문 분석할 수 없습니다.  
  
 다음 형식은 정수에 대한 출력 데이터 형식입니다.  
  
-   음수에는 빼기 기호가 표시되고 양수에는 기호가 표시되지 않습니다.  
  
-   공백이 사용되지 않습니다.  
  
-   하나 이상의 힌두-아라비아 숫자(0-9).  
  
  
