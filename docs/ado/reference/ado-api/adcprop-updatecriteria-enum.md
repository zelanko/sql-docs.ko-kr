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
ms.openlocfilehash: 12d960e8fcd5e1f27ea8198ce52e080f6fddf7c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921413"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 사용 하 여 데이터 원본 행의 낙관적 업데이트를 수행 하는 동안 충돌을 검색 하는 데 사용할 수 있는 필드를 지정 합니다.  
  
 이러한 상수는 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 에서 참조 되 고 [OLE DB 문서에 대 한 Microsoft Cursor Service](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 에 설명 된 **레코드 집합** "**업데이트 조건**" 동적 속성에 사용 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**Adcriteria Aallcols**|1|데이터 원본 행의 열이 변경 된 경우 충돌을 검색 합니다.|  
|**Adcriteria Akey**|0|는 데이터 원본 행의 키 열이 변경 된 경우 충돌을 검색 합니다. 즉, 행이 삭제 된 것입니다.|  
|**Adcriteria Atimestamp**|3|는 데이터 원본 행의 타임 스탬프가 변경 된 경우 충돌을 검색 합니다. 즉, **레코드 집합** 을 가져온 후 행에 액세스 한 것입니다.|  
|**adCriteriaUpdCols**|2|는 **레코드 집합** 의 업데이트 된 필드에 해당 하는 데이터 원본 행의 열이 변경 된 경우 충돌을 검색 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. AdcPropUpdateCriteria|  
|AdoEnums. AdcPropUpdateCriteria|  
|AdoEnums. AdcPropUpdateCriteria|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
