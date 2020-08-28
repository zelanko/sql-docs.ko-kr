---
description: StreamOpenOptionsEnum
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f3865a3b0e550e7e3fe4887fb948bca72eadf1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988504"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
[Stream](./stream-object-ado.md) 개체를 여는 옵션을 지정 합니다. 값은 또는 작업과 함께 사용할 수 있습니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|비동기 모드에서 **Stream** 개체를 엽니다.|  
|**adOpenStreamFromRecord**|4|이미 열려 있는 [Record](./record-object-ado.md) 개체가 될 *소스* 매개 변수의 내용을 식별 합니다. 기본 동작은 트리 구조에서 노드를 직접 가리키는 URL로 *소스* 를 처리 하는 것입니다. 해당 노드와 연결 된 기본 스트림이 열립니다.|  
|**adOpenStreamUnspecified 되지 않음**|-1|기본값 기본 옵션을 사용 하 여 **스트림** 개체 열기를 지정 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 스트림)](./open-method-ado-stream.md)