---
title: StreamOpenOptionsEnum | Microsoft Docs
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
f1_keywords: StreamOpenOptionsEnum
helpviewer_keywords: StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44e21fbed203effb3262ed2af84340856c4af8be
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
여는 옵션을 지정는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다. 값은 OR 연산으로 결합할 수 있습니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1.|열립니다는 **스트림** 비동기 모드의 개체입니다.|  
|**adOpenStreamFromRecord**|4|내용을 식별 하는 *소스* 매개 변수를 이미 열려 있는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다. 기본 동작은 처리할 *소스* 직접 트리 구조에서 노드를 가리키는 URL로 합니다. 해당 노드와 연결 된 기본 스트림이 열립니다.|  
|**adOpenStreamUnspecified**|-1|기본. Opening 지정는 **스트림** 기본 옵션으로는 개체입니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)
