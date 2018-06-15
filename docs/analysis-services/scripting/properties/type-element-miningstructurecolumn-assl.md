---
title: 요소 (MiningStructureColumn) (ASSL)를 입력 합니다. | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bcb7cec0d968e1320bdafc4bf53d25d6efdabc6f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040424"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Type 요소(MiningStructureColumn)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  유형을 포함 된 [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Long*|부호 있는 64비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **Int64** 데이터 형식에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB의.NET Framework 및 DBTYPE_I8 데이터 형식입니다.|  
|*Boolean*|부울 값입니다. 이 데이터 형식에 매핑됩니다는 **부울** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_BOOL 데이터 형식입니다.|  
|*텍스트*|유니코드 문자의 Null로 끝나는 스트림입니다. 이 데이터 형식에 매핑됩니다는 **문자열** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_WSTR 데이터 형식입니다.|  
|*Double*|-1.79E+308부터 1.79E+308 사이의 배정밀도 부동 소수점 숫자입니다. 이 데이터 형식에 매핑됩니다는 **Double** .NET Framework 및 OLE DB의 DBTYPE_R8 데이터 형식에 대 한 데이터 형식입니다.|  
|*날짜*|배정밀도 부동 소수점 숫자로 저장되는 날짜 데이터입니다. 정수 부분은 1899년 12월 30일 이후의 날짜 수이고, 소수 부분은 하루를 분수로 표시한 수입니다. 이 데이터 형식에 매핑됩니다는 **DateTime** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_DATE 데이터 형식입니다.|  
|*테이블*|중첩 테이블입니다. 이 데이터 형식은 OLE DB의 DBTYPE_HCHAPTER 데이터 형식에 매핑됩니다.<br /><br /> 참고:.NET Framework의 테이블 열은 이와 동일한 기본 데이터 형식을 가지 지 않으므로 있지만 대신에서 지원 되는 **DataReader** 클래스입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>합니다.  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
