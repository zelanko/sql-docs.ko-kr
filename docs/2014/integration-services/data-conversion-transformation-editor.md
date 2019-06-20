---
title: 데이터 변환 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5346c808c7d724ae630bb3dd25016a9977af363e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060048"
---
# <a name="data-conversion-transformation-editor"></a>데이터 변환 편집기
  **데이터 변환 편집기** 대화 상자를 사용하여 변환할 열을 선택하고, 열이 변환될 데이터 형식을 선택하고, 변환 특성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  `FastParse` 데이터 변환 출력 열의 속성을 사용할 수 없습니다는 **데이터 변환 편집기**를 사용 하 여 설정할 수 있습니다를 **고급 편집기**합니다. 이 속성에 대한 자세한 내용은 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)의 데이터 변환 섹션을 참조하십시오.  
  
 데이터 변환에 대한 자세한 내용은 [Data Conversion Transformation](data-flow/transformations/data-conversion-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **사용 가능한 입력 열**  
 확인란을 사용하여 변환할 열을 선택합니다. 선택한 항목은 아래의 입력 열에 추가됩니다.  
  
 **입력 열**  
 사용 가능한 입력 열 목록에서 변환할 열을 선택합니다. 선택 내용에 따라 위의 확인란이 달라집니다.  
  
 **출력 별칭**  
 각 새 열의 별칭을 입력합니다. 기본값은 `Copy of` 뒤에 입력 열 이름이 오는 형식이지만 설명이 포함된 고유 이름을 선택할 수 있습니다.  
  
 **데이터 형식**  
 목록에서 사용 가능한 데이터 형식을 선택합니다. 자세한 내용은 [Integration Services Data Types](data-flow/integration-services-data-types.md)을 참조하세요.  
  
 **길이**  
 문자열 데이터의 열 길이를 설정합니다.  
  
 **전체 자릿수**  
 숫자 데이터의 전체 자릿수를 설정합니다.  
  
 **소수 자릿수**  
 숫자 데이터의 소수 자릿수를 설정합니다.  
  
 **코드 페이지**  
 DT_STR 유형의 열에 적절한 코드 페이지를 선택합니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](../../2014/integration-services/configure-error-output.md) 대화 상자를 사용하여 하위 수준 오류를 처리하는 방법을 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [데이터 변환을 사용하여 데이터를 다른 데이터 형식으로 변환](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  
