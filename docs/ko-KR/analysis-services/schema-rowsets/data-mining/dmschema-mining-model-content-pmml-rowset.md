---
title: DMSCHEMA_MINING_MODEL_CONTENT_PMML 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML rowset
ms.assetid: fa05bb08-a955-4c8d-b57f-ffcd82470220
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 153624dce91c2b94707170e94c9da3c497da02e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT_PMML 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  마이닝 모델의 XML 구조를 반환합니다. XML 문자열 형식은 PMML(Predictive Model Markup Language) 2.1 표준을 따릅니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DMSCHEMA_MINING_MODEL_CONTENT_PMML** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||모델이 멤버인 데이터베이스 이름으로 채워지는 카탈로그 이름입니다.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||정규화되지 않은 스키마 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**모델 이름**|**DBTYPE_WSTR**||모델 이름입니다. 이 열에는 **NULL**이 포함될 수 없습니다.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||모델 유형입니다. 공급자별 문자열입니다. **NULL**일 수 있습니다.|  
|**MODEL_GUID**|**DBTYPE_GUID**||모델을 식별하는 GUID입니다. GUID를 사용하여 테이블을 식별하지 않는 공급자는 **NULL**을 반환합니다.|  
|**MODEL_PMML**|**DBTYPE_WSTR**||PMML 형식으로 된 모델 내용의 XML 표현입니다.|  
|**SIZE**|**DBTYPE_UI4**||XML 문자열의 바이트 수입니다.|  
|**위치**|**DBTYPE_WSTR**||XML 파일의 위치입니다. 사용할 수 있는 위치가 없으면 **NULL** 입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DMSCHEMA_MINING_MODEL_CONTENT_PMML** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|(선택 사항)|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|(선택 사항)|  
|**모델 이름**|**DBTYPE_WSTR**|(선택 사항)|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 스키마 행 집합](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
