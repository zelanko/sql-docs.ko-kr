---
description: 커서 및 잠금 특성
title: 커서 및 잠금 특성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: rothja
ms.author: jroth
ms.openlocfilehash: 4bd8b88ab3a90669982a752023d8a983c188dcbf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991464"
---
# <a name="cursor-and-lock-characteristics"></a>커서 및 잠금 특성
커서의 특성은 공급자의 기능에 따라 달라 지지만 일반적으로 다양 한 유형의 커서 및 잠금에 적용 되는 다음과 같은 장점과 단점이 있습니다.  
  
|커서 또는 잠금 유형|장점|단점|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-리소스 요구 사항 부족|-뒤로 스크롤할 수 없습니다.<br />-데이터 동시성 없음|  
|**adOpenStatic**|-스크롤 가능|-데이터 동시성 없음|  
|**adOpenKeyset**|-일부 데이터 동시성<br />-스크롤 가능|-높은 리소스 요구 사항<br />-연결 되지 않은 시나리오에서 사용할 수 없음|  
|**adOpenDynamic**|-높은 데이터 동시성<br />-스크롤 가능|-최고 리소스 요구 사항<br />-연결 되지 않은 시나리오에서 사용할 수 없음|  
|**adLockReadOnly**|-리소스 요구 사항 부족<br />-확장성이 매우 뛰어납니다.|-커서를 통해 데이터를 업데이트할 수 없음|  
|**adLockBatchOptimistic**|-Batch 업데이트<br />-연결 되지 않은 시나리오 허용<br />-데이터에 액세스할 수 있는 다른 사용자|-한 번에 여러 사용자가 데이터를 변경할 수 있습니다.|  
|**adLockPessimistic**|-잠겨 있는 동안 다른 사용자가 데이터를 변경할 수 없습니다.|-잠겨 있는 동안 다른 사용자가 데이터에 액세스 하지 못하게 합니다.|  
|**adLockOptimistic**|-데이터에 액세스할 수 있는 다른 사용자|-한 번에 여러 사용자가 데이터를 변경할 수 있습니다.|
