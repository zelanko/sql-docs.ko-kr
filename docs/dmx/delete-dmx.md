---
title: DELETE (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DELETE
dev_langs:
- DMX
helpviewer_keywords:
- DELETE statement [DMX]
- mining structures [DMX], clearing
- clearing mining models
- deleting mining models
- mining models [Analysis Services], clearing
- deleting mining structures
ms.assetid: 5a8204c3-a3df-4d97-9c1d-d997d24c70e3
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 00be9b52e652e2a2456cdbcd589f048d8a971d47
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="delete-dmx"></a>DELETE(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용할 DMX(Data Mining Extensions) 절에 따라 마이닝 모델, 마이닝 구조, 또는 마이닝 구조 및 연결된 모든 마이닝 모델을 지웁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>인수  
 *모델*  
 모델 식별자입니다.  
  
 *구조*  
 구조 식별자입니다.  
  
## <a name="remarks"></a>주의  
 지정 하지 않으면 **마이닝 모델** 또는 **마이닝 구조**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 이름 뒤에 개체 유형을 검색 하 고 올바른 개체를 처리 합니다. 서버에 이름이 서로 동일한 마이닝 구조 및 마이닝 모델이 있는 경우에는 오류가 반환됩니다.  
  
 다음 표에서는 다른 형식의 구문을 사용한 결과를 설명합니다.  
  
|문|결과|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE*\<구조 >*<br /><br /> 또는<br /><br /> DELETE FROM MINING STRUCTURE*\<구조 >*합니다. 콘텐츠|마이닝 구조에 ProcessClear를 수행합니다. 마이닝 구조 및 연결된 마이닝 모델에서 모든 내용이 지워집니다.|  
|DELETE FROM MINING STRUCTURE*\<구조 >*합니다. 경우|마이닝 구조에 ProcessClearStructureOnly를 수행합니다. 마이닝 구조에서 모든 내용이 지워지고 연결된 마이닝 모델은 그대로 유지됩니다. 마이닝 구조를 지운 후에는 연결된 마이닝 모델에서 드릴스루가 실행되지 않습니다.|  
|마이닝 모델에서 삭제*\<모델 >*<br /><br /> 또는<br /><br /> 마이닝 모델에서 삭제*\<모델 >*합니다. 콘텐츠|마이닝 모델에서 ProcessClear를 수행 하지만 상태 값을 그대로 둡니다. 상태 값은 열에서 가능한 상태입니다. 예를 들어 Gender 열의 상태 값은 Male 및 Female입니다.|  
  
 처리 유형에 대 한 자세한 내용은 참조 [Type 요소 &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md).  
  
## <a name="examples"></a>예  
 다음 예에서는 NB_Sample 모델에서 모든 내용을 제거합니다.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

