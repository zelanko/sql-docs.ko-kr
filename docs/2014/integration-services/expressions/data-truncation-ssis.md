---
title: 데이터 잘림(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 04f97fa81ff959a371409a046e29bf03f7043aa0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103653"
---
# <a name="data-truncation-ssis"></a>데이터 잘림(SSIS)
  식 처리 중 데이터가 잘릴 수 있습니다. 잘림은 다음과 같은 경우에 발생할 수 있습니다.  
  
-   문자열. 예를 들어 DT_WSTR 데이터 형식의 문자열 데이터를 문자 수로 측정된 동일한 길이의 DT_STR 데이터 형식 문자열로 변환하는 경우 원래 문자열에 더블바이트 문자가 포함되어 있으면 데이터가 손실됩니다.  
  
-   유효 자릿수. 예를 들어 정수를 DT_I4 데이터 형식에서 DT_I2 데이터 형식으로 캐스팅하거나 부호 없는 정수를 부호 있는 정수로 캐스팅하는 경우가 있습니다.  
  
-   무효 자릿수. 예를 들어 실수를 DT_R8에서 DT_R4로 캐스팅하거나 정수를 DT_I4 데이터 형식에서 DT_R4 데이터 형식으로 캐스팅하는 경우가 있습니다.  
  
 식 계산기는 잘림을 발생시킬 수 있는 명시적 캐스트를 식별하고 식을 구문 분석할 때 경고를 표시합니다. 예를 들어 30자 문자열을 20자 문자열로 캐스팅하면 식 계산기가 경고를 표시합니다.  
  
> [!NOTE]  
>  런타임에는 잘림을 확인하지 않으므로 경고 없이 데이터가 잘립니다. 그러나 대부분의 데이터 어댑터와 변환은 오류 행 처리를 수행할 수 있는 오류 출력을 지원합니다. 데이터 잘림 처리에 대 한 자세한 내용은 참조 하세요. [데이터 오류 처리](../data-flow/error-handling-in-data.md)합니다.  
  
  
