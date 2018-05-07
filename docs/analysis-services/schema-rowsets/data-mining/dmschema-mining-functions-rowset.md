---
title: DMSCHEMA_MINING_FUNCTIONS 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f92a3028f9397283f8d5820c54d823e40b8fdc3d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]를 실행 중인 서버에서 사용할 수 있는 데이터 마이닝 알고리즘이 지원하는 데이터 마이닝 함수에 대해 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DMSCHEMA_MINING_FUNCTIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**||알고리즘의 이름입니다.|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**||함수의 이름입니다.|  
|**T E R**|**DBTYPE_WSTR**||함수의 서명입니다.|  
|**RETURNS_TABLE**|**DBTYPE_BOOL**||함수에서 문자 인수 길이와 같은 스칼라 콘텐츠를 반환하면**FALSE** 이고, 히스토그램 테이블과 같은 테이블을 반환하면 **TRUE** 입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||함수에 대한 알기 쉬운 설명입니다.|  
|**HELP_FILE**|**DBTYPE_WSTR**||이 함수의 설명서가 있는 파일의 이름입니다.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||이 함수에 대한 도움말 컨텍스트 ID입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 **DMSCHEMA_MINING_FUNCTIONS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 스키마 행 집합](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
