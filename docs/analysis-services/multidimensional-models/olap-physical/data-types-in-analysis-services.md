---
title: Analysis Services의 데이터 형식 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea192588186f69adbc04ab6a56123206e1fb7817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208616"
---
# <a name="data-types-in-analysis-services"></a>Analysis Services의 데이터 형식
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  모든 <xref:Microsoft.AnalysisServices.DataItem> 개체를 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 다음 하위 집합을 지 원하는 **System.Data.OleDb.OleDbType**합니다. 를 설정 하거나 데이터 형식의 읽을 [DataItem 데이터 형식 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl)합니다.  
  
## <a name="supported-data-types"></a>지원되는 데이터 형식  
  
|||  
|-|-|  
|BigInt|부호 있는 64비트 정수입니다. 합니다 *BigInt* 값 형식은 음수 9,223,372,036,854,775,808에서 양수 9,223,372,036,854,775,807 까지의 값을 사용 하 여 정수를 나타냅니다.|  
|Binary|이진 데이터 스트림을 **바이트** 형식입니다. **바이트** 0에서 255 범위의 값을 가진 부호 없는 정수를 나타내는 값 형식입니다.|  
|Boolean|이 형식의 인스턴스 값을 갖습니다 **true** 하거나 **false**합니다.|  
|Currency|A *통화* -214,748.3648 (네 개의 소수 자릿수로)가 통화 단위의 정확도 사용 하 여-922,337,203,685,477.5808에서 + 922,337,203,685,477.5807 사이의 값입니다.|  
|Date|double로 저장된 날짜 및 시간 데이터입니다. 정수 부분은 1899년 12월 30일 이후의 일수이고, 소수 부분은 하루 또는 하루의 시간을 분수로 표시한 수입니다.|  
|Double|-1.79769313486232E +308에서 1.79769313486232E +308까지의 부동 소수점 숫자입니다. Double 값은 전체 자릿수가 최대 15자리인 숫자 정보를 저장합니다.|  
|정수|음수 2,147,483,648에서 양수 2,147,483,647까지의 값을 가진 32비트 부호 있는 정수입니다.|  
|Single|-3.4028235E +38에서 3.4028235E +38까지의 부동 소수점 숫자입니다. Single 값은 전체 자릿수가 최대 7자리인 숫자 정보를 저장합니다.|  
|Smallint|16비트 부호 있는 정수입니다. 합니다 *Smallint* 값 형식은 음수 32768에서 양수 32767 까지의 값을 가진 부호 있는 정수를 나타냅니다.|  
|Tinyint|부호 있는 8비트 정수입니다. Tinyint 값 형식은 음수 128에서 양수 127까지의 값을 가진 정수를 나타냅니다.|  
|UnsignedBigInt|64비트 부호 없는 정수입니다. 합니다 *UnsignedBigInt* 값 형식은 0에서 18446744073709551615 까지의 값을 가진 부호 없는 정수를 나타냅니다.|  
|UnsignedInt|32비트 부호 없는 정수입니다. 합니다 *UnsignedInt* 값 형식은 0에서 4294967295 까지의 값을 가진 부호 없는 정수를 나타냅니다.|  
|UnsignedSmallInt|부호 없는 16비트 정수입니다. 합니다 *UnsignedSmallInt* 값 형식은 0에서 65535 까지의 값을 가진 부호 없는 정수를 나타냅니다.|  
|UnsignedTinyInt|8비트 부호 없는 정수입니다. 합니다 *UnsignedTinyInt* 값 형식은 0에서 255 범위의 값을 가진 부호 없는 정수를 나타냅니다.|  
|WChar|유니코드 문자의 Null로 끝나는 스트림입니다. A *WChar* 는 텍스트를 나타내는 데 사용 되는 유니코드 문자의 순차적인 컬렉션입니다.|  
  
## <a name="amo-validations-on-data-types"></a>데이터 형식에 대한 AMO 유효성 검사  
 다음 표에서는 특정 바인딩에 대한 AMO(Analysis Management Objects)의 추가 유효성 검사를 보여 줍니다.  
  
|Object|바인딩|허용되는 데이터 형식|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Binary를 제외한 모든 데이터 형식|  
||NameColumn|WChar만|  
||SkippedLevelsColumn|정수 유형만: BigInt, Integer, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
||CustomRollupColumn|WChar만|  
||CustomRollupPropertiesColumn|WChar만|  
||UnaryOperatorColumn|WChar만|  
||ValueColumn|All|  
|AttributeTranslation|CaptionColumn|WChar만|  
|ScalarMiningStructureColumn|KeyColumns|Binary를 제외한 모든 데이터 형식|  
||NameColumn|WChar만|  
|TableMiningStructureColumn|ForeignKeyColumns|Binary를 제외한 모든 데이터 형식|  
|MeasureGroupAttribute|KeyColumns|Binary를 제외한 모든 데이터 형식|  
|고유 카운트 측정값|Source|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  
