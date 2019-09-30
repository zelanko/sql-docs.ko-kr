---
title: 데이터 잘림(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 03b521f06925ad21847cf588b27c211167dbd425
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297649"
---
# <a name="data-truncation-ssis"></a>데이터 잘림(SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  값의 데이터 형식을 변환하면 값이 잘릴 수 있습니다.  
  
 값이 잘릴 수 있는 경우는 다음과 같습니다.  
  
-   원본 문자열에 더블바이트 문자가 포함되어 있을 때 문자열 데이터를 *DT_WSTR* 에서 길이가 같은 *DT_STR* 로 변환하는 경우  
  
-   정수를 *DT_I4* 에서 *DT_I2* 로 캐스팅하는 경우(많은 숫자가 손실될 수 있음)  
  
-   부호 없는 정수를 부호 있는 정수로 캐스팅하는 경우(많은 숫자가 손실될 수 있음)  
  
-   실수를 *DT_R8* 에서 *DT_R4* 로 캐스팅하는 경우(많은 숫자가 손실될 수 있음)  
  
-   정수를 *DT_I4* 에서 *DT_R4* 로 캐스팅하는 경우(많은 숫자가 손실될 수 있음)  
  
 식 계산기는 잘림을 발생시킬 수 있는 명시적 캐스트를 식별하고 식을 구문 분석할 때 경고를 표시합니다. 예를 들어 30자 문자열을 20자 문자열로 캐스팅하면 식 계산기가 경고를 표시합니다.  
  
 그러나 런타임에는 잘림을 확인하지 않습니다. 런타임에는 경고 없이 데이터가 잘립니다. 대부분의 데이터 어댑터와 변환은 오류 행 처리를 수행할 수 있는 오류 출력을 지원합니다.  
  
 데이터 잘림 처리 방법에 대한 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.  
  
  
