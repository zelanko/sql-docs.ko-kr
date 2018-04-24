---
title: RecordCreateOptionsEnum | Microsoft Docs
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
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cc41adb9ab24afb357ce7d1528ffdd5b9fbed5b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
지정 기존 여부 **레코드** opened 또는 새 **레코드** 에 대해 생성는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체 [열려](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드. 값은 AND 연산자로 결합할 수 있습니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|새 **레코드** 로 지정 된 노드에서 *소스* 매개 변수는 기존을 여는 대신 **레코드**합니다. 소스를 가리키는 경우 기존 노드에 런타임 오류가 발생 하지 않는 한 **adCreateCollection** 결합 된 **adOpenIfExists** 또는 **adCreateOverwrite**합니다.|  
|**adCreateNonCollection**|0|새 **레코드** 형식의 [adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)합니다.|  
|**adCreateOverwrite**|0x4000000|생성 플래그가 수정 **adCreateCollection**, **adCreateNonCollection**, 및 **adCreateStructDoc**합니다. 때 소스 URL 기존 노드를 가리키는 경우이 값과 생성 플래그 값 중 하나를 사용 하거나 또는 **레코드**, 기존 다음 **레코드** 덮어쓴 및 그 자리에 만들어질 새는 합니다. 이 값과 함께 사용할 수 없습니다 **adOpenIfExists**합니다.|  
|**adCreateStructDoc**|0x80000000|새 **레코드** 형식의 [adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md), 기존을 여는 대신 **레코드**합니다.|  
|**adFailIfNotExists**|-1|기본. 런타임 오류가 발생 하는 경우 *소스* 존재 하지 않는 노드를 가리킵니다.|  
|**adOpenIfExists**|0x2000000|생성 플래그가 수정 **adCreateCollection**, **adCreateNonCollection**, 및 **adCreateStructDoc**합니다. 때 소스 URL 기존 노드를 가리키는 경우이 값과 생성 플래그 값 중 하나를 사용 하거나 또는 **레코드** 개체를 기존 공급자 열어야 **레코드** 새로 만드는 대신 하나입니다. 이 값과 함께 사용할 수 없습니다 **adCreateOverwrite**합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)
