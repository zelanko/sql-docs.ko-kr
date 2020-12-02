---
description: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 826403e2edaee6c891a55f31ccad88469a8411cb
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506137"
---
# <a name="localdb_error_too_many_shared_instances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>세부 정보  
  
| attribute | 값 |
| --------- | ----- |
|제품 이름|SQL Server|  
|이벤트 ID|287|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|공유 인스턴스가 너무 많아 고유한 사용자 인스턴스 이름을 생성할 수 없습니다. 기존 공유 인스턴스 중 일부의 공유를 해제하십시오.|  
  
## <a name="explanation"></a>설명  
 공유 인스턴스가 너무 많아 고유한 사용자 인스턴스 이름을 생성할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 하나 이상의 공유 로컬 데이터베이스 런타임 인스턴스의 공유를 해제하고 다시 시도하십시오.  
  
  
