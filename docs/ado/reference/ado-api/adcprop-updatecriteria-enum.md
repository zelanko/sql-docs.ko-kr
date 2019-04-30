---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b4d64095c02fbf3f969248fc78d375a191fe72
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065279"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
사용 하 여 데이터 소스 행의 낙관적 업데이트 하는 동안 충돌을 검색 하는 필드를 사용할 수 있습니다 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체.  
  
 사용 하 여 이러한 상수를 사용 하 여는 **레코드 집합** "**업데이트 기준을**"에서 참조 하는 동적 속성을 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 는에설명되어있습니다[ OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 설명서.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|데이터 원본 행의 모든 열이 변경 된 경우 충돌을 검색 합니다.|  
|**adCriteriaKey**|0|키 열 데이터의 원본 행이 변경 된 경우 충돌, 행이 삭제 된 것을 의미 하는 것을 검색 합니다.|  
|**adCriteriaTimeStamp**|3|충돌 데이터의 타임 스탬프 원본 행 하는 경우 변경 된 후 행에 액세스 하는 의미를 감지 합니다 **레코드 집합** 가져온 합니다.|  
|**adCriteriaUpdCols**|2|업데이트 된 필드에 해당 하는 데이터 원본 열의 모든 행 하는 경우 충돌을 감지 합니다 **레코드 집합** 변경 되었습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
