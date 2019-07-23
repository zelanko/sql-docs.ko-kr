---
title: 리터럴(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- string literals
- numeric literals [Integration Services]
- Boolean literals
- expressions [Integration Services], literals
- literals [Integration Services]
- mapping literals [Integration Services]
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1e24da5c7cf22cd0f192d29a063e2aa7d20746cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968056"
---
# <a name="numeric-string-and-boolean-literals"></a>숫자, 문자열 및 부울 리터럴

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 식은 숫자, 문자열 및 부울 리터럴을 포함할 수 있습니다. 식 계산기는 정수, 10진수 및 부동 소수점 상수와 같은 다양한 숫자 리터럴을 지원합니다. 또한 식 계산기의 값 처리 방법을 지정하는 long 및 float 접미사와 숫자 리터럴의 과학적 표기법을 지원합니다.  
  
## <a name="numeric-literals"></a>숫자 리터럴  
 식 계산기는 정수 및 비정수 숫자 데이터 형식을 지원합니다. 또한 계보 식별자(패키지 요소의 고유 숫자 식별자)를 지원합니다. 계보 식별자는 숫자이지만 수치 연산에 사용할 수 없습니다.  
  
 식 계산기는 식 계산기의 숫자 리터럴 처리 방법을 나타내는 데 사용할 수 있는 접미사를 지원합니다. 예를 들어 37L 또는 37l을 써서 정수 37이 정수(Long)로 처리되도록 나타낼 수 있습니다.  
  
 다음 표에서는 숫자 리터럴의 접미사를 보여 줍니다.  
  
|접미사|설명|  
|------------|-----------------|  
|L 또는 l|숫자 리터럴(Long)|  
|U 또는 u|부호 없는 숫자 리터럴|  
|E 또는 e|과학적 표기법의 지수|  
  
 다음 표에서는 숫자 식 요소와 해당 정규식을 나열합니다.  
  
|식 요소|정규식|설명|  
|------------------------|------------------------|-----------------|  
|D로 표현된 자릿수|[0-9]|모든 자릿수|  
|E로 표현된 과학적 표기법|[Ee][+-]?{D}+|대문자 또는 소문자 e, 선택적 + 또는 -, D로 정의된 하나 이상의 자릿수|  
|IS로 표현된 정수 접미사|(([lL]?[uU]?)&#124;([uU]?[lL]?))|대문자 또는 소문자 u와 l 또는 u와 l의 모든 조합(옵션). U 또는 u는 부호 없는 값을 나타냅니다. L 또는 l은 Long 값을 나타냅니다.|  
|FS로 표현된 부동 접미사|([f&#124;F]&#124;[l&#124;L])|f 또는 l의 대문자 또는 소문자. F 또는 f는 float 값(DT_R4 데이터 형식)을 나타냅니다. L 또는 l은 Long 값(DT_R8 데이터 형식)을 나타냅니다.|  
|H로 표현된 16진수|[a-fA-F0-9]|모든 16진수|  
  
 다음 표에서는 정규식 언어를 사용한 유효한 숫자 리터럴을 설명합니다.  
  
|정규식|설명|  
|------------------------|-----------------|  
|{D}+{IS}|한 자릿수 이상의 정수 숫자 리터럴(D) 및 선택적인 Long 및/또는 부호 없는 접미사(IS).  예: 457, 785u, 986L, 7945ul.|  
|{D}+{E}{FS}|한 자릿수 이상의 비정수 숫자 리터럴(D), 과학적 표기법 및 Long 또는 float 접미사.  예: 4E8l, 13e-2f, 5E+L.|  
|{D}*"."{D}+{E}?{FS}|소수 자릿수가 있는 비정수 숫자 리터럴, 한 자릿수 이상의 소수 부분, 선택적 지수(E) 및 한 개의 float 또는 한 개의 Long 식별자(FS). 이 숫자 리터럴은 DT_R4 또는 DT_R8 데이터 형식을 갖습니다.  예: 6.45E3f, .89E-2l, 1.05E+7F.|  
|{D}+"."{D}*{E}?{FS}|한 자릿수 이상의 유효 자릿수가 있는 비정수 숫자 리터럴(D), 소수 자릿수, 지수(E) 및 한 개의 float 또는 한 개의 Long 식별자(FS). 이 숫자 리터럴은 DT_R4 또는 DT_R8 데이터 형식을 갖습니다.  예: 1.E-4f, 4.6E6L, 8.365E+2f.|  
|{D}*.{D}+|전체 자릿수와 소수 자릿수를 갖는 비정수 숫자 리터럴. 소수 자릿수와 한 자릿수 이상의 소수 부분(D)이 있습니다. 이 숫자 리터럴은 DT_NUMERIC 데이터 형식을 갖습니다.  예: .9, 5.8, 0.346|  
|{D}+.{D}*|전체 자릿수와 소수 자릿수를 갖는 비정수 숫자 리터럴. 한 자릿수 이상의 유효 자릿수(D)와 소수 자릿수가 있습니다. 이 숫자 리터럴은 DT_NUMERIC 데이터 형식을 갖습니다.  예: 6., 0.2, 8.0.|  
|#{D}+|계보 식별자. 파운드(#) 문자와 한 자릿수(D) 이상으로 구성됩니다. 예: #123|  
|0[xX]{H}+{uU}|16진수 형식의 숫자 리터럴. 0, 대문자 또는 소문자 x, 하나 이상의 대문자 H, 선택적으로 부호 없는 접미사가 포함됩니다. 예: 0xFF0A, 0X000010000U.|  
  
 식 계산기에 사용되는 데이터 형식에 대한 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 식은 여러 데이터 형식의 숫자 리터럴을 포함할 수 있습니다. 식 계산기는 이러한 식을 계산할 때 데이터를 호환 가능한 형식으로 변환합니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
 그러나 일부 데이터 형식 간의 변환에는 명시적 캐스트가 필요합니다. 식 계산기는 명시적 데이터 형식 변환을 위한 캐스트 연산자를 제공합니다. 자세한 내용은 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>숫자 리터럴을 Integration Services 데이터 형식으로 매핑  
 식 계산기는 숫자 리터럴을 계산할 때 다음 변환을 수행합니다.  
  
-   정수 숫자 리터럴은 다음과 같이 정수 데이터 형식으로 매핑됩니다.  
  
    |접미사|결과 형식|  
    |------------|-----------------|  
    |없음|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > **중요!!** Long(L 또는 l) 접미사가 없으면 식 계산기는 값이 데이터 형식을 오버플로하는 경우에도 부호 있는 값을 DT_I4 데이터 형식으로 매핑하고 부호 없는 값을 DT_UI4 데이터 형식으로 매핑합니다.  
  
-   지수가 포함된 숫자 리터럴은 DT_R4 또는 DT_R8 데이터 형식으로 변환됩니다. 식에 Long 접미사가 있으면 DT_R8 데이터 형식으로 변환되고 float 접미사가 있으면 DT_R4 데이터 형식으로 변환됩니다.  
  
-   비정수 숫자 리터럴에 F 또는 f가 있으면 DT_R4 데이터 형식으로 매핑됩니다. L 또는 l을 포함하고 숫자가 정수이면 DT_I8 데이터 형식으로 매핑됩니다. 실수이면 DT_R8 데이터 형식으로 매핑됩니다. Long 접미사가 있으면 DT_R8 데이터 형식으로 변환됩니다.  
  
-   전체 자릿수와 소수 자릿수가 있는 비정수 숫자 리터럴은 DT_NUMERIC 데이터 형식으로 매핑됩니다.  
  
## <a name="string-literals"></a>문자열 리터럴  
 문자열 리터럴은 따옴표로 묶어야 합니다. 식 언어는 인쇄할 수 없는 문자 및 따옴표와 같이 일반적으로 이스케이프되는 문자의 이스케이프 시퀀스 집합을 제공합니다.  
  
 문자열 리터럴은 따옴표로 묶인 0개 이상의 문자로 구성됩니다. 문자열에 따옴표가 있으면 식이 구문 분석될 수 있도록 따옴표를 이스케이프해야 합니다. \x0000을 제외한 모든 2바이트 문자를 문자열에 사용할 수 있습니다. \x0000 문자는 문자열의 Null 종결자입니다.  
  
 이스케이프 시퀀스가 필요한 다른 문자가 문자열에 포함될 수 있습니다. 다음 표에서는 문자열 리터럴의 이스케이프 시퀀스를 보여 줍니다.  
  
|이스케이프 시퀀스|설명|  
|---------------------|-----------------|  
|\a|경고|  
|\b|백스페이스|  
|\f|용지 공급|  
|\n|줄 바꿈|  
|\r|캐리지 리턴|  
|\t|가로 탭|  
|\v|세로 탭|  
|\\"|물음표|  
|\\\|백슬래시|  
|\xhhhh|16진수 표기법의 유니코드 문자|  
  
## <a name="boolean-literals"></a>부울 리터럴  
 식 계산기는 일반적인 부울 리터럴 **True**와 **False**를 지원합니다. 식 계산기는 대/소문자를 구분하지 않으며 대문자와 소문자의 모든 조합이 허용됩니다. 예를 들어 TRUE는 True와 같습니다.  
  
> **참고:** 식에서 부울 리터럴은 공백으로 구분해야 합니다.  
  
  
