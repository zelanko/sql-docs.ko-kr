---
description: ConnectOptionEnum
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
ms.openlocfilehash: 73fb0218b9a4a9437dbe8c103c8496f0a209e9b1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775812"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
[연결 개체](./connection-object-ado.md) 의 [Open](./open-method-ado-connection.md) 메서드가 연결이 설정 된 후 (동기적) 또는 before (비동기적으로) 반환 되어야 하는지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|연결을 비동기적으로 엽니다. [Connectcomplete](./connectcomplete-and-disconnect-events-ado.md) 이벤트는 연결을 사용할 수 있는 시기를 결정 하는 데 사용할 수 있습니다.|  
|**adConnectUnspecified**|-1|기본값 연결을 동기적으로 엽니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums 연결을 선택 합니다.|  
|AdoEnums CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 연결)](./open-method-ado-connection.md)