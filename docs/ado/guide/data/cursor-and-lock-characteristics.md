---
title: "커서와 잠금 특성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84f06591c70a42701ca264c99af00e4f072aadd0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="cursor-and-lock-characteristics"></a>커서와 잠금 특성
커서의 특징 공급자의 기능에 따라 다르지만, 하는 동안 다음과 같은 장점 및 단점 일반적으로 적용에 다양 한 유형의 커서 및 잠금.  
  
|커서 또는 잠금 유형|장점|단점|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-낮은 리소스 요구 사항|-뒤로 스크롤할 수 없음<br />-데이터 동시성|  
|**adOpenStatic**|스크롤할 수|-데이터 동시성|  
|**adOpenKeyset**|-일부 데이터 동시성<br />스크롤할 수|-높은 리소스 요구 사항<br />-연결이 끊긴된 시나리오에서 사용할 수 없음|  
|**adOpenDynamic**|-높은 데이터 동시성<br />스크롤할 수|-가장 높은 리소스 요구 사항<br />-연결이 끊긴된 시나리오에서 사용할 수 없음|  
|**adLockReadOnly**|-낮은 리소스 요구 사항<br />-확장성|-데이터 커서를 통해 업데이트할 수 없음|  
|**adLockBatchOptimistic**|일괄 처리 업데이트<br />-연결이 끊긴된 시나리오를 허용합니다.<br />-다른 사용자가 데이터에 액세스할 수|여러 사용자가 한 번에 데이터를 변경할 수 있습니다.|  
|**adLockPessimistic**|잠겨 있는 동안 다른 사용자가 데이터를 변경할 수 없습니다.|-잠겨 있는 동안에 데이터에 액세스 하지 못하도록 다른 사용자가 방지 합니다.|  
|**adLockOptimistic**|-다른 사용자가 데이터에 액세스할 수|여러 사용자가 한 번에 데이터를 변경할 수 있습니다.|
