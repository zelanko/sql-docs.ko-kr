---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85ee3a7833a0c2bffc95ae21b44295d234ee8d5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047961"
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 행 집합
  서버의 알고리즘 매개 변수에 대해 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DMSCHEMA_MINING_SERVICE_PARAMETERS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||알고리즘의 이름입니다.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`||매개 변수의 이름입니다.|  
|`PARAMETER_TYPE`|`DBTYPE_WSTR`||매개 변수의 유형입니다.|  
|`IS_REQUIRED`|`DBTYPE_BOOL`||필수 매개 변수인 경우 `TRUE`를 반환하는 부울입니다.|  
|`PARAMETER_FLAGS`|`DBTYPE_UI4`||매개 변수의 특징을 설명하는 비트 마스크입니다.<br /><br /> -   `DM_PARAMETER_TRAINING` (`0x0000001`) 매개 변수는 학습에 사용 됨을 나타냅니다<br />-   `DM_PARAMETER_PREDICTION` (`0x00000002`) 매개 변수 예측에 사용 됨을 나타냅니다<br />-   `DM_PARAMETER_CONTENT` (`0x00000003`) 매개 변수가 콘텐츠 제한에 사용 됨을 나타냅니다|  
|`DESCRIPTION`|`DBTYPE_WSTR`||매개 변수에 대한 알기 쉬운 설명입니다.|  
|`DEFAULT_VALUE`|`DBTYPE_WSTR`||매개 변수의 기본값입니다. 기본값이 단순한 데이터 형식이 아니면 `NULL`을 반환합니다.|  
|`VALUE_ENUMERATION`|`DBTYPE_WSTR`||매개 변수에 사용할 수 있는 값에 대한 열거자입니다.|  
|`HELP_FILE`|`DBTYPE_WSTR`||이 매개 변수의 설명서가 있는 파일의 이름입니다.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||이 함수에 대한 도움말 컨텍스트 ID입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 `DMSCHEMA_MINING_SERVICE_PARAMETERS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 스키마 행 집합](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
