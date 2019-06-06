---
title: RecordCreateOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d57f1bc241e5e27618a9598895ea7be089ce20dd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712018"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
지정 기존 여부를 **레코드** 열거나 새 해야 **레코드** 에 대해 생성 합니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체 [열기](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드. AND 연산자를 사용 하 여 값을 결합할 수 있습니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|만듭니다 **레코드** 로 지정 된 노드에서 *원본* 매개 변수를 기존를 여는 대신 **레코드**합니다. 소스를 가리키는 경우 기존 노드를 다음 런타임 오류가 발생 하는 경우가 아니면 **adCreateCollection** 와 결합 됩니다 **adOpenIfExists** 하거나 **adCreateOverwrite**합니다.|  
|**adCreateNonCollection**|0|새로 만듭니다 **레코드** 형식의 [adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)합니다.|  
|**adCreateOverwrite**|0x4000000|생성 플래그를 수정 **adCreateCollection**하십시오 **adCreateNonCollection**, 및 **adCreateStructDoc**합니다. 때 소스 URL을 기존 노드를 가리키는 경우이 값과 생성 플래그 값 중 하나는 또는 또는 **레코드**, 다음 기존 **레코드** 덮어쓸 나타내며 새 해당 위치에 만들어집니다. 이 값과 함께 사용할 수 없습니다 **adOpenIfExists**합니다.|  
|**adCreateStructDoc**|0x80000000|새로 만듭니다 **레코드** 형식의 [adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md), 기존를 여는 대신 **레코드**합니다.|  
|**adFailIfNotExists**|-1|기본. 런타임 오류가 발생 하는 경우 *원본* 존재 하지 않는 노드를 가리킵니다.|  
|**adOpenIfExists**|0x2000000|생성 플래그를 수정 **adCreateCollection**하십시오 **adCreateNonCollection**, 및 **adCreateStructDoc**합니다. 경우는 소스 URL을 기존 노드를 가리키는 경우이 값 및 생성 플래그 값 중 하나에 사용 하거나 또는 **레코드** 개체를 기존 공급자 열어야 **레코드** 새로 만드는 대신 하나입니다. 이 값과 함께 사용할 수 없습니다 **adCreateOverwrite**합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)
