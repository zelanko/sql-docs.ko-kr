---
title: 커서 및 잠금 특성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3a206a21cf7c6680a656c89c48b8f52d1069d78
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702121"
---
# <a name="cursor-and-lock-characteristics"></a>커서 및 잠금 특성
커서의 특징은 공급자의 기능에 종속 하는 동안 다음과 같은 장점 및 단점 일반적으로 적용할 다양 한 유형의 커서 및 잠금.  
  
|커서 또는 잠금 유형|장점|단점|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-낮은 리소스 요구 사항|-뒤로 스크롤 없습니다.<br />-데이터 동시성|  
|**adOpenStatic**|스크롤할 수 있는|-데이터 동시성|  
|**adOpenKeyset**|-일부 데이터 동시성<br />스크롤할 수 있는|상위 리소스 요구 사항<br />-연결이 끊긴된 시나리오에서 사용할 수 없음|  
|**adOpenDynamic**|-높은 데이터 동시성<br />스크롤할 수 있는|최상위 리소스 요구 사항<br />-연결이 끊긴된 시나리오에서 사용할 수 없음|  
|**adLockReadOnly**|-낮은 리소스 요구 사항<br />높은 확장성|-데이터 커서를 통해 업데이트할 수 없음|  
|**adLockBatchOptimistic**|일괄 처리 업데이트<br />--연결이 끊긴된 시나리오를 허용 하는 중<br />-다른 사용자 데이터에 액세스할 수|여러 사용자가 한 번에 데이터를 변경할 수 있습니다.|  
|**adLockPessimistic**|잠겨 있는 동안 다른 사용자가 데이터를 변경할 수 없습니다.|-다른 사용자가 잠겨 있는 동안 데이터에 액세스 하지 못하도록 방지|  
|**adLockOptimistic**|-다른 사용자 데이터에 액세스할 수|여러 사용자가 한 번에 데이터를 변경할 수 있습니다.|
