---
title: ResyncEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ResyncEnum
helpviewer_keywords: ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f7ad5525f2f9e7ce7e915b97d397d3d7d372a27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="resyncenum"></a>ResyncEnum
호출 하 여 원본 값을 덮어쓸지 여부를 지정 [Resync](../../../ado/reference/ado-api/resync-method.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|기본. 데이터를 덮어쓰고 보류 중인 업데이트가 취소 됩니다.|  
|**adResyncUnderlyingValues**|1.|데이터를 덮어쓰지 않습니다 및 보류 중인 업데이트를 취소 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>적용 대상  
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)
