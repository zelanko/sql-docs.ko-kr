---
title: "문자열 데이터 비교 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a706839de5dd4981e09c4bc1384ee45f86c0dcb
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="comparing-string-data"></a>문자열 데이터 비교
  문자열 비교는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 수행되는 여러 변환에서 중요한 부분이며, 변수의 식 및 속성 식 평가에도 사용됩니다. 예를 들어 정렬 변환에서는 데이터 집합의 값을 비교하여 데이터를 오름차순 또는 내림차순으로 정렬합니다.  
  
## <a name="configuring-transformations-for-string-comparisons"></a>문자열 비교를 위한 변환 구성  
 정렬, 집계, 유사 항목 그룹화, 유사 항목 조회 변환을 사용자 지정하여 열 수준에서 문자열이 비교되는 방식을 변경할 수 있습니다. 예를 들어 비교 시 대/소문자를 무시하여 대문자와 소문자가 모두 동일한 문자로 취급되도록 지정할 수 있습니다.  
  
 다음 변환에서는 문자열 비교를 포함할 수 있는 식이 사용됩니다.  
  
-   조건부 분할 변환에서는 식에서 문자열 비교를 사용하여 데이터 행을 전송할 출력을 결정할 수 있습니다. 자세한 내용은 [Conditional Split Transformation](../../integration-services/data-flow/transformations/conditional-split-transformation.md)을 참조하세요.  
  
-   파생 열 변환에서는 식에서 문자열 비교를 사용하여 새 열 값을 생성할 수 있습니다. 자세한 내용은 [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md)을 참조하세요.  
  
 또한 변수, 변수 매핑 및 선행 제약 조건에서는 문자열 비교가 포함될 수 있는 식이 사용됩니다. 식에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
## <a name="processing-during-string-comparison"></a>문자열 비교 시 수행되는 처리  
 데이터 및 변환 구성에 따라 문자열 데이터 비교 중에 다음 처리 작업이 발생할 수 있습니다.  
  
-   데이터를 유니코드로 변환합니다. 원본 데이터가 아직 유니코드가 아닌 경우 비교가 발생하기 전에 데이터가 자동으로 유니코드로 변환됩니다.  
  
-   로캘을 사용하여 날짜, 시간, 숫자 데이터 및 정렬 순서를 해석하기 위한 로캘 특정 규칙을 적용합니다.  
  
-   열 수준에서 비교 옵션을 적용하여 비교 시 대/소문자 구분 여부를 변경합니다.  
  
## <a name="converting-string-data-to-unicode"></a>문자열 데이터를 유니코드로 변환  
 변환에서 수행되는 작업 및 변환 구성에 따라 문자열 데이터를 문자열의 유니코드 표현인 DT_WSTR 데이터 형식으로 변환할 수 있습니다.  
  
 데이터 형식이 DT_STR인 문자열 데이터는 열의 코드 페이지를 사용하여 유니코드로 변환됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 열 수준의 코드 페이지가 지원되며 각 열은 다른 코드 페이지를 사용하여 변환될 수 있습니다.  
  
 대부분의 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 데이터 원본의 올바른 코드 페이지를 식별할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 및 열 수준의 데이터 정렬을 설정할 수 있습니다. 코드 페이지는 Windows 또는 SQL 데이터 정렬 중 하나일 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬로부터 파생됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 예기치 않은 코드 페이지가 제공되는 경우 또는 패키지에서 올바른 코드 페이지를 확인하는 데 필요한 정보가 충분하지 않은 공급자를 사용하여 데이터 원본에 액세스하는 경우에는 OLE DB 원본과 OLE DB 대상의 기본 코드 페이지를 지정할 수 있습니다. 기본 코드 페이지는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공되는 코드 페이지 대신 사용됩니다.  
  
 파일에는 코드 페이지가 없습니다. 대신 패키지에서 파일 데이터에 연결하기 위해 사용하는 플랫 파일과 다중 플랫 파일 연결 관리자에는 파일의 코드 페이지를 지정하기 위한 속성이 포함됩니다. 코드 페이지는 열 수준이 아닌 파일 수준에서만 설정될 수 있습니다.  
  
## <a name="setting-locale"></a>로캘 설정  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 코드 페이지를 사용하여 데이터 정렬 또는 날짜, 시간 및 숫자 데이터 해석을 위한 로캘 특정 규칙을 유추하지 않습니다. 그 대신 변환이 데이터 흐름 구성 요소, 데이터 흐름 태스크, 컨테이너 또는 패키지의 LocaleId 속성으로 설정된 로캘을 읽습니다. 기본적으로 변환의 로캘은 해당 데이터 흐름 태스크로부터 상속되며, 이 작업은 패키지로부터 상속됩니다. 데이터 흐름 태스크가 For 루프 컨테이너와 같은 컨테이너에 포함되는 경우 이 태스크는 컨테이너의 로캘을 상속합니다.  
  
 또한 플랫 파일 연결 관리자와 다중 플랫 파일 연결 관리자에 대한 로캘을 지정할 수 있습니다.  
  
## <a name="setting-comparison-options"></a>비교 옵션 설정  
 로캘은 문자열 데이터 비교를 위한 기본 규칙을 제공합니다. 예를 들어 로캘은 영문자의 각 문자에 대한 정렬 위치를 지정합니다. 하지만 이러한 규칙만으로는 일부 변환에서 수행되는 비교 시 충분하지 않을 수 있으며, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 로캘의 비교 규칙 이외에도 일련의 고급 비교 옵션이 지원됩니다. 이러한 비교 옵션은 열 수준에서 설정됩니다. 예를 들어 비교 옵션 중 하나를 사용하면 비공백 문자를 무시할 수 있습니다. 이 옵션을 설정하면 악센트와 같은 분음 부호를 무시하여 비교 시 "a"와 "á"가 동일하게 인식됩니다.  
  
 다음 표에서는 비교 옵션과 정렬 스타일에 대해 설명합니다.  
  
|비교 옵션|Description|  
|-----------------------|-----------------|  
|대/소문자 무시|비교 시 대문자와 소문자를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 대/소문자가 무시됩니다. 예를 들어 "ABC"는 "abc"와 동일하게 인식됩니다.|  
|가나 형식 무시|비교 시 두 가지 형식의 일본어 가나 문자인 히라가나와 가타가나를 구분합니다. 이 옵션을 설정하면 문자열 비교 시 가나 형식이 무시됩니다.|  
|문자 너비 무시|비교 시 싱글바이트 문자와 동일 문자의 더블바이트 문자 표현을 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 동일 문자에 대한 싱글바이트 표현과 더블바이트 표현이 동일하게 인식됩니다.|  
|비공백 문자 무시|비교 시 공백 문자와 분음 기호를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 비교 시 분음 기호가 무시됩니다. 예를 들어 "å"와 "a"는 동일합니다.|  
|기호 무시|비교 시 글자 문자와 공백 문자, 문장 부호, 통화 기호 및 수학 기호와 같은 기호를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 기호가 무시됩니다. 예를 들어 " New York"은 "New York"과 동일하며 "*ABC"는 "ABC"와 동일합니다.|  
|문장 부호를 기호로 정렬|비교 시 영숫자 문자 앞에서 하이픈과 아포스트로피를 제외한 모든 문장 부호를 정렬할지 여부를 지정합니다. 예를 들어 이 옵션을 설정하면 ".ABC"가 "ABC" 앞에 정렬됩니다.|  
  
 정렬, 집계, 유사 항목 그룹화 및 유사 항목 조회 변환에는 데이터 비교를 위한 이러한 옵션이 포함됩니다.  
  
 **FullySensitive** 비교 플래그는 유사 항목 그룹화 및 유사 항목 조회 변환을 위해 **고급 편집기** 대화 상자에 표시됩니다. **FullySensitive** 비교 플래그를 선택하면 모든 비교 옵션이 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)   
 [빠른 구문 분석](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [표준 구문 분석](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)  
  
  
