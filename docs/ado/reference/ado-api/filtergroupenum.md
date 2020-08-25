---
description: FilterGroupEnum
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: rothja
ms.author: jroth
ms.openlocfilehash: 7552eb4b069b2cd2adc33e0bff25f23d918468c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775292"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
레코드 [집합](./recordset-object-ado.md)에서 필터링 할 레코드 그룹을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|마지막 [삭제](./delete-method-ado-recordset.md), 다시 [동기화](./resync-method.md), [UpdateBatch](./updatebatch-method.md)또는 [CancelBatch](./cancelbatch-method-ado.md) 호출의 영향을 받는 레코드만 볼 필터입니다.|  
|**adFilterConflictingRecords**|5|마지막 일괄 업데이트에 실패 한 레코드를 보기 위한 필터입니다.|  
|**adFilterFetchedRecords**|3|현재 캐시의 레코드 (즉, 데이터베이스에서 레코드를 검색 하는 마지막 호출의 결과)를 보기 위한 필터입니다.|  
|**adFilterNone**|0|현재 필터를 제거 하 고 보기 위해 모든 레코드를 복원 합니다.|  
|**adFilterPendingRecords**|1|변경 되었지만 아직 서버에 전송 되지 않은 레코드만 볼 수 있는 필터입니다. 일괄 처리 업데이트 모드에만 적용할 수 있습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums AFFECTEDRECORDS|  
|AdoEnums CONFLICTINGRECORDS|  
|AdoEnums-FETCHEDRECORDS|  
|AdoEnums.|  
|AdoEnums 레코드|  
  
## <a name="applies-to"></a>적용 대상  
 [Filter 속성](./filter-property.md)