---
description: DELETE(DMX)
title: 삭제 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6050a387af893e984b95c036181b7f16a269dc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491559"
---
# <a name="delete-dmx"></a>DELETE(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  사용할 DMX(Data Mining Extensions) 절에 따라 마이닝 모델, 마이닝 구조, 또는 마이닝 구조 및 연결된 모든 마이닝 모델을 지웁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>인수  
 *model*  
 모델 식별자입니다.  
  
 *구조체나*  
 구조 식별자입니다.  
  
## <a name="remarks"></a>설명  
 **마이닝 모델** 또는 **마이닝 구조**를 지정 하지 않으면에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이름을 기준으로 개체 유형을 검색 하 고 올바른 개체를 처리 합니다. 서버에 이름이 서로 동일한 마이닝 구조 및 마이닝 모델이 있는 경우에는 오류가 반환됩니다.  
  
 다음 표에서는 다른 형식의 구문을 사용한 결과를 설명합니다.  
  
|인수를 제거합니다.|결과|  
|---------------|------------|  
|마이닝 구조에서 삭제*\<structure>*<br /><br /> 또는<br /><br /> 마이닝 구조에서 삭제 *\<structure>* 합니다. 콘텐트가|마이닝 구조에서 ProcessClear를 수행 합니다. 마이닝 구조 및 연결된 마이닝 모델에서 모든 내용이 지워집니다.|  
|마이닝 구조에서 삭제 *\<structure>* 합니다. 경우|마이닝 구조에 대해 ProcessClearStructureOnly를 수행 합니다. 마이닝 구조에서 모든 내용이 지워지고 연결된 마이닝 모델은 그대로 유지됩니다. 마이닝 구조를 지운 후에는 연결된 마이닝 모델에서 드릴스루가 실행되지 않습니다.|  
|마이닝 모델에서 삭제*\<model>*<br /><br /> 또는<br /><br /> 마이닝 모델에서 삭제 *\<model>* 합니다. 콘텐트가|마이닝 모델에서 ProcessClear를 수행 하지만 상태 값은 그대로 유지 합니다. 상태 값은 열에서 가능한 상태입니다. 예를 들어 Gender 열의 상태 값은 Male 및 Female입니다.|  
  
 형식을 처리 하는 방법에 대 한 자세한 내용은 [형식 요소 &#40;XMLA&#41;](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/type-element-xmla)를 참조 하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 NB_Sample 모델에서 모든 내용을 제거합니다.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
