---
title: MSSQLSERVER_17128 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e3a2d500a16a90ce997273fad3eb7c2d8a82c1d6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553678"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17128|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|INIT_NOBUFSPACE|  
|메시지 텍스트|initdata: 커널 버퍼용 메모리가 없습니다.|  
  
## <a name="explanation"></a>설명  
 버퍼 풀의 초기 메모리 할당 또는 예약이 실패하여 SQL Server가 종료됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 일반적으로 이 오류는 최소 시스템 요구 사항보다 훨씬 작은 머신에서 SQL Server를 시작하는 경우에 발생합니다.  
  
  
