---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 562e79590a2a5f1f5e9bb609b9a0ad0ea8b2bfd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928682"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
열기에 대 한 옵션을 지정 하는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다. OR 연산을 사용 하 여 값을 결합할 수 있습니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|열립니다는 **Stream** 비동기 모드의 개체입니다.|  
|**adOpenStreamFromRecord**|4|콘텐츠를 식별 하는 *소스* 매개 변수는 이미 열려 있어야 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다. 기본 동작을 처리 하는 것 *원본* 트리 구조에서 노드로 직접 가리키는 url입니다. 해당 노드와 연결 된 기본 스트림이 열려 있습니다.|  
|**adOpenStreamUnspecified**|-1|기본. 열기를 지정 합니다 **Stream** 기본 옵션이 포함 된 개체입니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)
