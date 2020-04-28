---
title: Analysis Services의 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 910be4f4-3010-41cd-9fdc-f0a79a0ce823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ecdc64918e582f25f0e017d263c66e78c0d1bee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62725387"
---
# <a name="data-types-in-analysis-services"></a>Analysis Services의 데이터 형식
  모든 <xref:Microsoft.AnalysisServices.DataItem> 개체에 대해 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는의 `System.Data.OleDb.OleDbType`다음 하위 집합을 지원 합니다. 데이터 형식을 설정 하거나 읽으려면 [DataItem 데이터 형식 &#40;&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl)를 사용 합니다.  
  
## <a name="supported-data-types"></a>지원되는 데이터 형식  
  
|||  
|-|-|  
|BigInt|부호 있는 64비트 정수입니다. *BigInt* 값 형식은 음수 9223372036854775808에서 양수 9223372036854775807 범위의 값을 갖는 정수를 나타냅니다.|  
|이진|**바이트** 형식의 이진 데이터 스트림입니다. **Byte** 는 0에서 255 사이의 값을 가진 부호 없는 정수를 나타내는 값 형식입니다.|  
|부울|이 형식의 인스턴스 값은 `true` 또는 `false`입니다.|  
|Currency|정확도가-922337203685477.5808에서 + 922337203685477.5807 까지인 통화 단위 (소수점 네 자리)의 10 분의 *통화* 값입니다.|  
|날짜|double로 저장된 날짜 및 시간 데이터입니다. 정수 부분은 1899년 12월 30일 이후의 일수이고, 소수 부분은 하루 또는 하루의 시간을 분수로 표시한 수입니다.|  
|Double|-1.79769313486232E +308에서 1.79769313486232E +308까지의 부동 소수점 숫자입니다. Double 값은 전체 자릿수가 최대 15자리인 숫자 정보를 저장합니다.|  
|정수|음수 2,147,483,648에서 양수 2,147,483,647까지의 값을 가진 32비트 부호 있는 정수입니다.|  
|Single|-3.4028235E +38에서 3.4028235E +38까지의 부동 소수점 숫자입니다. Single 값은 전체 자릿수가 최대 7자리인 숫자 정보를 저장합니다.|  
|Smallint|부호 있는 16비트 정수입니다. *Smallint* 값 형식은 음수 32768에서 양수 32767 범위의 값을 가진 부호 있는 정수를 나타냅니다.|  
|Tinyint|부호 있는 8비트 정수입니다. Tinyint 값 형식은 음수 128에서 양수 127까지의 값을 가진 정수를 나타냅니다.|  
|UnsignedBigInt|부호 없는 64비트 정수입니다. *UnsignedBigInt* 값 형식은 0에서 18446744073709551615 사이의 값을 가진 부호 없는 정수를 나타냅니다.|  
|UnsignedInt|부호 없는 32비트 정수입니다. *Unsignedint* 값 형식은 0에서 4294967295 사이의 값을 가진 부호 없는 정수를 나타냅니다.|  
|UnsignedSmallInt|부호 없는 16비트 정수입니다. *Un미확인 smallint* 값 형식은 0에서 65535 사이의 값을 가진 부호 없는 정수를 나타냅니다.|  
|UnsignedTinyInt|부호 없는 8비트 정수입니다. *UnsignedTinyInt* 값 형식은 0에서 255 사이의 값을 가진 부호 없는 정수를 나타냅니다.|  
|WChar|유니코드 문자의 Null로 끝나는 스트림입니다. *WChar* 는 텍스트를 나타내는 데 사용 되는 유니코드 문자의 순차적인 컬렉션입니다.|  
  
## <a name="amo-validations-on-data-types"></a>데이터 형식에 대한 AMO 유효성 검사  
 다음 표에서는 특정 바인딩에 대한 AMO(Analysis Management Objects)의 추가 유효성 검사를 보여 줍니다.  
  
|Object|바인딩|허용되는 데이터 형식|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Binary를 제외한 모든 데이터 형식|  
||NameColumn|WChar만|  
||SkippedLevelsColumn|정수 형식 (BigInt, Integer, SmallInt, TinyInt, UnsignedBigInt, Un Int, Unsignedint, UnsignedTinyInt)만|  
||CustomRollupColumn|WChar만|  
||CustomRollupPropertiesColumn|WChar만|  
||UnaryOperatorColumn|WChar만|  
||ValueColumn|모두|  
|AttributeTranslation|CaptionColumn|WChar만|  
|ScalarMiningStructureColumn|KeyColumns|Binary를 제외한 모든 데이터 형식|  
||NameColumn|WChar만|  
|TableMiningStructureColumn|ForeignKeyColumns|Binary를 제외한 모든 데이터 형식|  
|MeasureGroupAttribute|KeyColumns|Binary를 제외한 모든 데이터 형식|  
|고유 카운트 측정값|원본|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  
