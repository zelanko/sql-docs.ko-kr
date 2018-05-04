---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a95040a932e35d96a7b2a384da1a910ada118349
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
지정 된 데이터 원본의 행의 낙관적 업데이트 하는 동안 충돌을 검색 하는 필드를 사용할 수 있습니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
 이러한 상수를 사용 하 여는 **레코드 집합** "**업데이트 조건**"에서 참조 되는 동적 속성은 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 는에설명되어[ OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 설명서입니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1.|데이터 원본 행의 모든 열이 변경 된 경우 충돌을 검색 합니다.|  
|**adCriteriaKey**|0|키 열 데이터의 원본 행이 변경 된 경우 충돌, 즉, 해당 행이 삭제를 검색 합니다.|  
|**adCriteriaTimeStamp**|3|원본 행 데이터의 타임 스탬프가 경우 변경 된 경우 충돌을 의미 하는 행에 액세스 한 후 검색는 **레코드 집합** 을 받았습니다.|  
|**adCriteriaUpdCols**|2|업데이트 된 필드에 해당 하는 행의 데이터 원본의 열 경우 충돌 감지는 **레코드 집합** 변경 되었습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
