---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: rothja
ms.author: jroth
ms.openlocfilehash: fa372f05a80290e907298a0969d9eb9f14355f90
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762604"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
[연결 개체](../../../ado/reference/ado-api/connection-object-ado.md) 의 [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드가 연결이 설정 된 후 (동기적) 또는 before (비동기적으로) 반환 되어야 하는지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|연결을 비동기적으로 엽니다. [Connectcomplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) 이벤트는 연결을 사용할 수 있는 시기를 결정 하는 데 사용할 수 있습니다.|  
|**adConnectUnspecified**|-1|기본값 연결을 동기적으로 엽니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums 연결을 선택 합니다.|  
|AdoEnums CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)
