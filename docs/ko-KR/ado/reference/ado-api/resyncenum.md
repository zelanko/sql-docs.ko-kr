---
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c755c31e055429c220742f35cef5f49ba8459870
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="resyncenum"></a>ResyncEnum
호출 하 여 원본 값을 덮어쓸지 여부를 지정 [Resync](../../../ado/reference/ado-api/resync-method.md)합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|기본. 데이터를 덮어쓰고 보류 중인 업데이트가 취소 됩니다.|  
|**adResyncUnderlyingValues**|1.|데이터를 덮어쓰지 않습니다 및 보류 중인 업데이트를 취소 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>적용 대상  
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)
