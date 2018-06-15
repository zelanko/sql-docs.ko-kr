---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c99e449171b347290f832950f265c6579ba6a630
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283212"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
트랜잭션 특성을 지정 하는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|호출 하 여 고정 중단 수행 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 을 자동으로 새 트랜잭션을 시작 합니다. 이 동작을 지원 하지 않는 공급자입니다.|  
|**adXactCommitRetaining**|131072|호출 하 여 커밋을 수행 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 을 자동으로 새 트랜잭션을 시작 합니다. 이 동작을 지원 하지 않는 공급자입니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>적용 대상  
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
