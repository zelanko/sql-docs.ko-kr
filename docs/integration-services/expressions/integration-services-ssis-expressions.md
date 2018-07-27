---
title: Integration Services(SSIS) 식 | Microsoft Docs
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
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0a9a404de670421850f985f5db7be2efc9d6d58d
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084905"
---
# <a name="integration-services-ssis-expressions"></a>Integration Services(SSIS) 식
  식은 하나의 데이터 값으로 계산되는 기호(식별자, 리터럴, 함수 및 연산자)의 조합입니다. 간단한 식으로는 단일 상수, 변수 또는 함수가 있습니다. 그러나 식이 여러 개의 연산자와 함수를 사용하고 여러 개의 열과 변수를 참조하는 경우가 더 많습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 식은 CASE 문의 조건 정의, 데이터 열의 값 만들기 및 업데이트, 변수에 값 할당, 런타임에 속성 업데이트 또는 채우기, 선행 제약 조건에 제약 조건 정의, For Loop 컨테이너에 사용되는 식 제공 등에 사용할 수 있습니다.  
  
 식은 식 언어 및 식 계산기를 기반으로 합니다. 식 계산기는 식을 구분 분석하고 식이 식 언어의 규칙을 따를지 여부를 결정합니다. 식 구문과 지원되는 리터럴 및 식별자에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [구문&#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md)  
  
-   [리터럴&#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)  
  
-   [식별자&#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>식을 사용하는 구성 요소  
 식을 사용할 수 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 요소는 다음과 같습니다.  
  
-   식을 기반으로 데이터 행을 여러 대상으로 보내는 결정 구조를 구현하는 조건부 분할 변환. 조건부 분할 변환에 사용된 식은 **true** 또는 **false**로 계산되어야 합니다. 예를 들어 "Column1 > Column2" 식의 조건에 맞는 행을 별도의 출력으로 보낼 수 있습니다.  
  
-   식에서 생성한 값을 사용하여 데이터 흐름에 새 열을 채우거나 기존 열을 업데이트하는 파생 열 변환. 예를 들어 Column1 + " ABC" 식은 값을 업데이트하거나 연결 문자열을 포함하는 새 값을 만드는 데 사용할 수 있습니다.  
  
-   식을 사용하여 값이 설정되는 변수. 예를 들어 GETDATE()는 변수의 값을 현재 날짜로 설정합니다.  
  
-   식을 사용하여 패키지에서 제약된 태스크 또는 컨테이너의 실행 여부를 결정을 위한 조건을 지정하는 선행 제약 조건. 선행 제약 조건에 사용된 식은 **true** 또는 **false**로 계산 되어야 합니다. 예를 들어 \@A > \@B 식은 두 개의 사용자 정의 변수를 비교하여 제약된 태스크를 실행할지 여부를 결정합니다.  
  
-   식을 사용하여 루프 구조의 초기값, 비교값 및 증가값 문을 작성하는 For Loop 컨테이너. 예를 들어 \@Counter = 1 식은 루프 카운터를 초기화합니다.  
  
 또한 패키지의 속성 값, For Loop 및 Foreach Loop와 같은 컨테이너, 태스크, 패키지 및 프로젝트 수준의 연결 관리자, 로그 공급자, Foreach 열거자를 업데이트하는 데 식을 사용할 수 있습니다. 예를 들어 속성 식을 사용하여 "Localhost.AdventureWorks" 문자열을 SQL 실행 태스크의 ConnectionName 속성에 할당할 수 있습니다. 자세한 내용은 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
## <a name="icon-markers-for-expressions"></a>식에 대한 아이콘 표식  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 식이 설정되어 있는 태스크, 연결 관리자 및 변수 옆에 특수 아이콘 표식이 표시됩니다. **HasExpressions** 속성은 변수를 제외하고 식을 지원하는 모든 SSIS 개체에서 사용할 수 있습니다. 이 속성을 사용하면 식이 있는 개체를 쉽게 식별할 수 있습니다.  
  
## <a name="expression-builder"></a>식 작성기  
 식 작성기는 식을 작성하는 그래픽 도구입니다. **조건부 분할 변환 편집기**, **파생 열 변환 편집기** 대화 상자, **식 작성기** 대화 상자에서 사용할 수 있는 식 작성기는 식을 작성하는 그래픽 도구입니다.  
  
 식 작성기는 패키지 관련 요소를 포함하는 폴더, 함수를 포함하는 폴더, 유형 변환 및 식 언어가 제공하는 연산자를 제공합니다. 패키지 관련 요소에는 시스템 변수 및 사용자 정의 변수가 포함됩니다. **조건부 분할 변환 편집기** 및 **파생 열 변환 편집기** 대화 상자에도 데이터 열이 있습니다. 변환을 위한 식을 작성하기 위해 항목을 폴더에서 **조건** 또는 **식** 열로 끌어다 놓거나 해당 열에 직접 식을 입력할 수 있습니다. 식 작성기가 변수 이름의 \@ 접두사와 같은 필요한 구문 요소를 자동으로 추가합니다.  
  
> [!NOTE]  
>  사용자 정의 변수 및 시스템 변수의 이름은 대/소문자를 구분합니다.  
  
 변수에는 범위가 있으며 식 작성기의 **변수** 폴더에는 범위 내에 있고 사용할 수 있는 변수만 나열됩니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소에서 식 사용](http://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>관련 내용  
 social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](http://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
