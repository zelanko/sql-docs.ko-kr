---
title: 식 작성기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 199c6a433523fed4a4cb164669529b2426df37f7
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275189"
---
# <a name="expression-builder"></a>식 작성기
  **식 작성기** 대화 상자를 사용하여 변수를 나열하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 언어에 포함된 함수, 유형 변환 및 연산자에 대한 참조를 기본적으로 제공하는 그래픽 사용자 인터페이스로 변수 값을 설정하는 식을 작성하거나 속성 식을 생성 및 편집할 수 있습니다.  
  
 속성 식은 속성에 할당된 식입니다. 식을 평가하면 속성이 식의 평가 결과를 사용하도록 동적으로 업데이트됩니다. 마찬가지로 변수에 사용된 식을 통해 식의 평가 결과로 변수 값을 업데이트할 수 있습니다.  
  
 여러 가지 방법으로 식을 사용할 수 있습니다.  
  
-   **태스크** 변수에 저장된 메일 주소를 삽입하여 메일 보내기 태스크에 사용되는 받는 사람 줄을 업데이트하거나 "Sales for:" 등의 문자열과 GETDATE 함수에서 반환된 현재 날짜를 연결하여 제목 줄을 업데이트합니다.  
  
-   **변수**`DATEPART("mm",GETDATE())`와 같은 식을 사용하여 변수 값을 현재 월로 설정하거나 `"Today's date is " + (DT_WSTR,30)(GETDATE())` 식을 사용하여 문자열 리터럴과 현재 날짜를 연결하여 문자열 값을 설정합니다.  
  
-   **연결 관리자** 다른 코드 페이지 식별자가 포함된 변수를 사용하여 플랫 파일 연결 관리자의 코드 페이지를 설정하거나 식에 3과 같은 양의 정수를 입력하여 데이터 파일의 행 수를 지정합니다.  
  
 속성 식에 대한 자세한 내용과 식을 작성하는 방법에 대한 자세한 내용은 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**변수**|**변수** 폴더를 확장한 다음 변수를 **식** 상자로 끕니다.|  
|**수치 연산 함수**<br /><br /> **문자열 함수**<br /><br /> **날짜/시간 함수**<br /><br /> **NULL 함수**<br /><br /> **유형 변환**<br /><br /> **연산자**|폴더를 확장한 다음 함수, 유형 변환 및 연산자를 **식** 상자로 끕니다.|  
|**식**|식을 편집하거나 입력합니다.|  
|**평가 값**|식의 평가 결과를 나열합니다.|  
|**식 계산**|식의 계산 결과를 보려면 **식 계산** 을 클릭합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [식 페이지](../../integration-services/expressions/expressions-page.md)   
 [속성 식 편집기](../../integration-services/expressions/property-expressions-editor.md)   
 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)   
 [시스템 변수](../../integration-services/system-variables.md)  
  
  
