---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 268d495d2163d03244a6bec57762b93a26ab32ea
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
