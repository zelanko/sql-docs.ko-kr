---
title: 데이터 구문 분석 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 98d03e601846d3b9656240aad3f161841ff5597f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125903"
---
# <a name="parsing-data"></a>데이터 구문 분석
  패키지의 데이터 흐름에서는 다양한 표준 및 사용자 지정 데이터 형식이 사용될 수 있는 다른 유형의 데이터 저장소 간의 데이터가 추출 및 로드됩니다. 데이터 흐름에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본은 데이터를 추출하고, 문자열 데이터를 구문 분석하고, 데이터를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환하는 작업을 수행합니다. 이후의 변환에서는 데이터를 다른 데이터 형식으로 변환하기 위해 데이터를 구문 분석하거나 다른 데이터 형식이 포함된 열 복사본을 만들 수 있습니다. 구성 요소에 사용된 식에서는 인수와 피연산자를 다른 데이터 형식으로 캐스팅할 수도 있습니다. 마지막으로, 데이터가 데이터 저장소에 로드될 때 대상에서는 대상에 사용되는 데이터 형식으로 데이터를 변환하기 위해 데이터를 구문 분석할 수 있습니다. 자세한 내용은 [Integration Services Data Types](integration-services-data-types.md)을 참조하세요.  
  
## <a name="types-of-parsing"></a>구문 분석 유형  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 데이터 변환을 위해 빠른 구문 분석과 표준 구문 분석이라는 두 가지 유형의 구문 분석을 제공합니다.  
  
-   빠른 구문 분석은 신속하고 간단한 구문 분석 루틴이지만 로캘 특정 데이터 형식 변환을 지원하지 않으며 가장 자주 사용되는 날짜 및 시간 형식만 지원합니다. 자세한 내용은 [Fast Parse](../fast-parse.md)을 참조하세요.  
  
-   표준 구문 분석은 다양한 기능이 포함된 구문 분석 루틴이며 Oleaut32.dll 및 Ole2dsip.dll에서 사용할 수 있는 자동 데이터 형식 변환 API에 제공되는 모든 데이터 형식 변환을 지원합니다. 자세한 내용은 [Standard Parse](../standard-parse.md)을 참조하세요.  
  
  
