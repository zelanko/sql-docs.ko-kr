---
title: 데이터 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb7639f027a66e424d554a074a82a7ea2d08a827
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726183"
---
# <a name="data-conversion-transformation"></a>데이터 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  데이터 변환은 입력 열의 데이터를 다른 데이터 형식으로 변환한 다음 새 출력 열에 복사합니다. 예를 들어 패키지는 여러 개의 원본에서 데이터를 추출한 다음 이 변환을 사용하여 대상 데이터 저장소에 필요한 데이터 형식으로 열을 변환할 수 있습니다. 단일 입력 열에 여러 개의 변환을 적용할 수 있습니다.  
  
 이 변환을 사용하면 패키지가 다음 유형의 데이터 변환을 수행할 수 있습니다.  
  
-   데이터 형식을 변경합니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
    > [!NOTE]  
    >  데이터를 날짜 또는 datetime 데이터 형식으로 변환하는 경우 출력 열의 날짜는 로캘 기본 설정에서 다른 형식을 지정해도 ISO 형식으로 표시됩니다.  
  
-   문자열 데이터의 열 길이와 숫자 데이터의 전체 자릿수 및 소수 자릿수를 설정합니다. 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
-   코드 페이지를 지정합니다. 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.  
  
    > [!NOTE]  
    >  문자열 데이터 형식의 열을 다른 문자열 데이터 형식의 열로 복사하는 경우 두 열이 동일한 코드 페이지를 사용해야 합니다.  
  
 문자열 데이터의 출력 열 길이가 해당 입력 열의 길이보다 짧으면 출력 데이터가 잘립니다. 자세한 내용은 [데이터 오류 처리](../../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다. SSIS 디자이너에서 데이터 변환을 사용하는 방법은 [데이터 변환을 사용하여 데이터를 다른 데이터 형식으로 변환](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)을 참조하세요. 이 변환의 속성을 프로그래밍 방식으로 설정하는 방법은 [공용 속성](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 blogs.msdn.com의 블로그 항목 - [SSIS 2008의 데이터 형식 변환 기술 간 성능 비교](https://go.microsoft.com/fwlink/?LinkId=220823)  
  
## <a name="data-conversion-transformation-editor"></a>데이터 변환 편집기
  **데이터 변환 편집기** 대화 상자를 사용하여 변환할 열을 선택하고, 열이 변환될 데이터 형식을 선택하고, 변환 특성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  데이터 변환 출력 열의 **FastParse** 속성은 **데이터 변환 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이 속성에 대한 자세한 내용은 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)의 데이터 변환 섹션을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 확인란을 사용하여 변환할 열을 선택합니다. 선택한 항목은 아래의 입력 열에 추가됩니다.  
  
 **입력 열**  
 사용 가능한 입력 열 목록에서 변환할 열을 선택합니다. 선택 내용에 따라 위의 확인란이 달라집니다.  
  
 **출력 별칭**  
 각 새 열의 별칭을 입력합니다. 기본값은 **Copy of** 뒤에 입력 열 이름이 오는 형식이지만 설명이 포함된 고유 이름을 선택할 수 있습니다.  
  
 **데이터 형식**  
 목록에서 사용 가능한 데이터 형식을 선택합니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 **길이**  
 문자열 데이터의 열 길이를 설정합니다.  
  
 **정밀도**  
 숫자 데이터의 전체 자릿수를 설정합니다.  
  
 **소수 자릿수**  
 숫자 데이터의 소수 자릿수를 설정합니다.  
  
 **코드 페이지**  
 DT_STR 유형의 열에 적절한 코드 페이지를 선택합니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 하위 수준 오류를 처리하는 방법을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [빠른 구문 분석](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
