---
title: 데이터 흐름의 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fdc7a7922668efb8e83ecb19c1e89107b1e764f5
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334397"
---
# <a name="data-in-data-flows"></a>데이터 흐름의 데이터
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 데이터 흐름에 사용되는 데이터 형식 집합이 제공됩니다.  
  
## <a name="data-type-conversion"></a>데이터 형식 변환  
 데이터 흐름에 추가하는 원본은 원본 데이터를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환합니다. 이후의 변환에서는 데이터를 다른 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환할 수 있으며, 데이터가 로드되는 데이터 저장소 유형에 따라 대상에서 최종 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식을 대상 데이터 저장소에 필요한 데이터 형식으로 변환할 수 있습니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 데이터를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환하기 위해 데이터 흐름 구성 요소는 해당 데이터를 구문 분석합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 빠른 구문 분석과 표준 구문 분석이라는 두 가지 유형의 구문 분석을 제공합니다. 대부분의 데이터 흐름 구성 요소에서는 표준 구문 분석만 사용할 수 있지만, 플랫 파일 원본과 데이터 변환에서는 빠른 구문 분석이나 표준 구문 분석을 사용할 수 있습니다. 자세한 내용은 [Parsing Data](../../integration-services/data-flow/parsing-data.md)을 참조하세요.  
  
## <a name="data-type-comparison"></a>데이터 형식 압축  
 여러 변환에서는 데이터 값을 비교합니다. 예를 들어 집계 변환은 일련의 데이터 행에서 값을 집계하기 위해 값을 비교하고, 정렬 변환에서는 값을 정렬하기 위해 비교하고, 조회 변환에서는 값을 별개의 참조 테이블에 있는 값과 비교합니다. 문자열의 비교 방법을 지정하기 위해 변환에는 대/소문자 구분 무시 여부, 일본어 텍스트에서의 가나 형식 취급 방법 및 문자열의 공백 문자 무시 여부와 같은 일련의 비교 옵션이 포함됩니다. 자세한 내용은 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.  
  
 또한 식 계산기는 변수, 선행 제약 조건 및 변환에서 사용되는 식이 계산될 때 데이터 값을 비교합니다.  
  
## <a name="data-flow-troubleshooting"></a>데이터 흐름 문제 해결  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 패키지를 배포한 후 실행 중에 데이터 흐름을 분석하여 성능을 검사하거나 다른 문제를 확인할 수 있습니다. 패키지 상태 및 기록을 볼 수 있는 표준 보고서를 사용할 수 있으며, 패키지 실행에 대한 세부 정보를 제공하는 데이터베이스 뷰를 쿼리할 수 있습니다. 실행 중에 데이터 탭을 동적으로 추가 및 제거하여 패키지의 특정 구성 요소를 대상으로 지정할 수도 있습니다. 자세한 내용은 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)을 참조하세요.  
  
  
