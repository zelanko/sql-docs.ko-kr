---
title: DMSCHEMA_MINING_FUNCTIONS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b726c81df5a6085ee52b177d95b4917d7cb8be1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169651"
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 행 집합
  실행 중인 서버에서 사용할 데이터 마이닝 알고리즘에서 지원 되는 데이터 마이닝 함수에 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DMSCHEMA_MINING_FUNCTIONS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||알고리즘의 이름입니다.|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`||함수의 이름입니다.|  
|`FUNCTION_SIGNATURE`|`DBTYPE_WSTR`||함수의 서명입니다.|  
|`RETURNS_TABLE`|`DBTYPE_BOOL`||함수에서 문자 인수 길이와 같은 스칼라 콘텐츠를 반환하면 `FALSE`이고, 히스토그램 테이블과 같은 테이블을 반환하면 `TRUE`입니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||함수에 대한 알기 쉬운 설명입니다.|  
|`HELP_FILE`|`DBTYPE_WSTR`||이 함수의 설명서가 있는 파일의 이름입니다.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||이 함수에 대한 도움말 컨텍스트 ID입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 `DMSCHEMA_MINING_FUNCTIONS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 스키마 행 집합](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
