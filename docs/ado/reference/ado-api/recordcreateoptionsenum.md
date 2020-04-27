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
ms.openlocfilehash: 65fe33b73cf77a27fcd69743ffb09cb05e197797
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917339"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
[Record](../../../ado/reference/ado-api/record-object-ado.md) object [Open](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드에 대해 기존 **레코드** 를 열지 아니면 새 **레코드** 를 만들지를 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|기존 **레코드**를 열지 않고 *원본* 매개 변수로 지정 된 노드에 새 **레코드** 를 만듭니다. 소스가 기존 노드를 가리키는 경우에는 **Adcreatecollection** 이 **AdOpenIfExists** 또는 **adcreatecollection**와 결합 되지 않는 한 런타임 오류가 발생 합니다.|  
|**adCreateNonCollection**|0|[AdSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md)형식의 새 **레코드** 를 만듭니다.|  
|**adCreateOverwrite**|0x4000000|생성 플래그 **Adcreatecollection**, **adCreateNonCollection**및 **adCreateStructDoc**를 수정 합니다. 또는를이 값과 함께 사용 하 고 생성 플래그 값 중 하나를 사용 하는 경우 원본 URL이 기존 노드나 **레코드**를 가리키면 기존 레코드를 덮어쓰고 해당 위치에 새 **레코드** 를 만듭니다. 이 값은 **adOpenIfExists**와 함께 사용할 수 없습니다.|  
|**adCreateStructDoc**|0x80000000|기존 **레코드**를 여는 대신 [AdStructDoc](../../../ado/reference/ado-api/recordtypeenum.md)형식의 새 **레코드** 를 만듭니다.|  
|**adFailIfNotExists**|-1|기본값 *소스가* 존재 하지 않는 노드를 가리키는 경우 런타임 오류가 발생 합니다.|  
|**adOpenIfExists**|0x2000000|생성 플래그 **Adcreatecollection**, **adCreateNonCollection**및 **adCreateStructDoc**를 수정 합니다. 이 값과 생성 플래그 값 중 하나에서 또는을 사용 하는 경우 원본 URL이 기존 노드나 **record** 개체를 가리키는 경우 공급자는 새 레코드를 만드는 대신 기존 **레코드** 를 열어야 합니다. 이 값은 **Adcreateoverwrite**와 함께 사용할 수 없습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)
