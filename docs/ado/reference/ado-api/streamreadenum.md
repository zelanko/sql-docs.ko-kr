---
description: StreamReadEnum
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: rothja
ms.author: jroth
ms.openlocfilehash: d9f685a80d822950a159ddb3fbc9f148489a723e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988474"
---
# <a name="streamreadenum"></a>StreamReadEnum
[스트림](./stream-object-ado.md) 개체에서 전체 스트림 또는 다음 줄을 읽어야 하는지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|기본값 현재 위치부터 [EOS](./eos-property.md) 표식까지 스트림에서 모든 바이트를 읽습니다. 이는 이진 스트림이 있는 유일 하 게 유효한 **Streamreadenum** 값 이며,이 값은 **Adtypebinary**[형식](./type-property-ado-stream.md) 입니다.|  
|**adReadLine**|-2|[LineSeparator](./lineseparator-property-ado.md) 속성으로 지정 된 스트림에서 다음 줄을 읽습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Read 메서드](./read-method.md)  
    :::column-end:::
    :::column:::
        [ReadText 메서드](./readtext-method.md)  
    :::column-end:::
:::row-end:::