---
title: PersistFormatEnum | Microsoft Docs
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
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4d0c825f6f1cd8f1d6040e1752f21a4a10f48f42
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="persistformatenum"></a>PersistFormatEnum
저장 하는 형식을 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Microsoft Advanced 데이터 테이블 그램 (ADTG) 형식을 나타냅니다.|  
|**adPersistADO**|1.|ADO의 Extensible Markup Language (XML) 형식 사용될지를 나타냅니다. 이 값 adPersistXML 동일 이며 이전 버전과 호환성에 대 한 포함 합니다.|  
|**adPersistXML**|1.|Extensible Markup Language (XML) 형식을 나타냅니다.|  
|**adPersistProviderSpecific**|2|공급자가 유지할 나타냅니다는 **레코드 집합** 자체 형식을 사용 하 여 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>적용 대상  
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
