---
description: XactAttributeEnum
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c7ea7ccbf1a588458db9e213bfa57837e89898f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776822"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
[Connection](./connection-object-ado.md) 개체의 트랜잭션 특성을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|[RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 를 호출 하 여 자동으로 새 트랜잭션을 시작 하 여 중단을 유지 합니다. 일부 공급자는이 동작을 지원 하지 않습니다.|  
|**adXactCommitRetaining**|131072|[CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 를 호출 하 여 새 트랜잭션을 자동으로 시작 하도록 커밋을 유지 합니다. 일부 공급자는이 동작을 지원 하지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums. XactAttribute|  
  
## <a name="applies-to"></a>적용 대상  
 [Attributes 속성(ADO)](./attributes-property-ado.md)