---
description: MSSQLSERVER_17128
title: MSSQLSERVER_17128 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1902d498a93555957b0c240d349a951327086382
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88410989"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
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
  
