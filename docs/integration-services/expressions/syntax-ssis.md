---
description: 구문(SSIS)
title: 구문(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], syntax
- syntax [Integration Services]
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ad0ccea1ed870f09b9d9fc15e12730ff67c6475
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195278"
---
# <a name="syntax-ssis"></a>구문(SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 구문은 C 언어와 C# 언어에서 사용하는 구문과 유사합니다. 식별자(열과 변수), 리터럴, 연산자, 함수 등의 요소가 식에 포함됩니다. 이 항목에서는 각 식 요소에 적용되는 식 계산기 구문의 고유 요구 사항을 요약해서 보여 줍니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 결과에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] DT_WSTR 또는 DT_STR 데이터 형식이 있는 경우 식의 계산 결과에 대해 4000자 제한이 있었습니다. 이제 이 제한이 제거되었습니다.  
  
 특정 연산자와 함수를 사용하는 샘플 식은 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md) 및 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md) 항목에서 각 연산자와 함수에 대한 항목을 참조하세요.  
  
 여러 개의 연산자 및 함수뿐만 아니라 식별자와 리터럴도 사용하는 샘플 식은 [고급 Integration Services 식의 예](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)를 참조하세요.  
  
 속성 식에서 사용할 샘플 식은 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
## <a name="identifiers"></a>식별자  
 식은 열 식별자와 변수 식별자를 포함할 수 있습니다. 열은 데이터 원본에서 시작되거나 데이터 흐름에서 변환으로 만들어질 수 있습니다. 식은 계보 식별자를 사용하여 열을 참조할 수 있습니다. 계보 식별자는 패키지 요소를 고유하게 식별하는 번호입니다. 식에서 참조된 계보 식별자는 파운드(#) 접두사를 포함해야 합니다. 예를 들어 계보 식별자 138은 #138을 사용하여 참조합니다.  
  
 식은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 에서 제공하는 시스템 변수와 사용자 지정 변수를 포함할 수 있습니다. 식에서 참조된 변수는 \@ 접두사를 포함해야 합니다. 예를 들어 `Counter` 변수는 \@Counter를 사용하여 참조합니다. \@ 문자는 변수 이름의 일부가 아니라 식 계산기에 해당 변수를 식별하는 역할만 합니다. 자세한 내용은 [식별자&#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)를 참조하세요.  
  
## <a name="literals"></a>리터럴  
 식은 숫자, 문자열 및 부울 리터럴을 포함할 수 있습니다. 식에 사용된 문자열 리터럴은 따옴표로 묶어야 합니다. 숫자 및 부울 리터럴은 따옴표를 사용하지 않습니다. 식 언어에는 자주 이스케이프되는 문자에 대한 이스케이프 시퀀스가 포함되어 있습니다. 자세한 내용은 [리터럴&#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)을 참조하세요.  
  
## <a name="operators"></a>연산자  
 식 계산기는 Transact-SQL, C++ 및 C#과 같은 언어의 연산자 집합과 유사한 기능을 제공하는 연산자 집합을 제공합니다. 그러나 식 언어에는 추가 연산자가 포함되어 있으며 일반적인 기호가 아닌 다른 기호를 사용합니다. 자세한 내용은 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)를 참조하세요.  
  
### <a name="namespace-resolution-operator"></a>네임스페이스 확인 연산자  
 식은 네임스페이스 확인 연산자(::)를 사용하여 동일한 이름을 가진 변수를 명확하게 구분합니다. 네임스페이스 확인 연산자를 사용하면 해당 네임스페이스로 변수를 정규화하여 동일한 이름을 가진 여러 개의 변수를 한 패키지에서 사용할 수 있습니다.  
  
#### <a name="cast-operator"></a>캐스트 연산자  
 캐스트 연산자는 식 결과, 열 값, 변수 값 및 상수를 다른 데이터 형식으로 변환합니다. 식 언어에서 제공하는 캐스트 연산자는 C 언어와 C# 언어에서 제공하는 것과 유사합니다. Transact-SQL에서는 CAST 함수와 CONVERT 함수가 이 기능을 제공합니다. 캐스트 연산자 구문과 CAST 및 CONVERT에 사용되는 구문의 차이점은 다음과 같습니다.  
  
-   캐스트 연산자는 식을 인수로 사용할 수 있습니다.  
  
-   캐스트 연산자 구문에는 CAST 키워드가 포함되지 않습니다.  
  
-   캐스트 연산자 구문에는 AS 키워드가 포함되지 않습니다.  
  
##### <a name="conditional-operator"></a>조건부 연산자  
 조건부 연산자는 부울 식의 계산에 따라 두 식 중 하나를 반환합니다. 식 언어에서 제공하는 조건부 연산자는 C 언어와 C# 언어에서 제공하는 것과 유사합니다. MDX(Multidimensional Expressions)에서는 IIF 함수가 이와 유사한 기능을 제공합니다.  
  
###### <a name="logical-operators"></a>논리 연산자  
 식 언어는 논리적 NOT 연산자를 나타내는 ! 문자를 지원합니다. Transact-SQL에서는 ! 연산자가 관계형 연산자 집합에 포함되어 있습니다. 예를 들어 Transact-SQL은 > 및 !> 연산자를 제공합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 식 언어는 ! 연산자와 다른 연산자의 조합을 지원하지 않습니다. 예를 들어 ! 연산자와 > 연산자를 !> 연산자로 결합할 수 없습니다. 그러나 식 언어는 같지 않음 비교를 나타내는 != 문자 조합을 기본적으로 지원합니다.  
  
###### <a name="equality-operators"></a>같음 연산자  
 식 계산기 문법에서는 == 등가 연산자를 제공합니다. 이 연산자는 Transact-SQL의 = 연산자 및 C#의 == 연산자에 해당합니다.  
  
## <a name="functions"></a>Functions  
 식 언어에는 Transact-SQL 함수 및 C# 메서드와 유사한 날짜 및 시간 함수, 수치 연산 함수 및 문자열 함수가 포함되어 있습니다.  
  
 몇몇 함수는 Transact-SQL 함수와 이름이 같지만 식 계산기에서 조금 다른 기능을 수행합니다.  
  
-   Transact-SQL의 ISNULL 함수는 Null 값을 지정한 값으로 바꾸는 반면 식 계산기의 ISNULL 함수는 식의 Null 여부에 따라 부울을 반환합니다.  
  
-   Transact-SQL의 ROUND 함수에는 결과 집합을 자르는 옵션이 있지만 식 계산기의 ROUND 함수에는 이 옵션이 없습니다.  
  
 자세한 내용은 [함수&#40;SSIS 식&#41;](../../integration-services/expressions/functions-ssis-expression.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소에서 식 사용](/previous-versions/sql/sql-server-2016/ms141007(v=sql.130))  
  
## <a name="related-content"></a>관련 내용  
  
-   pragmaticworks.com의 기술 문서 - [SSIS 식 치트 시트](https://go.microsoft.com/fwlink/?LinkId=746575)  
  
-   social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
