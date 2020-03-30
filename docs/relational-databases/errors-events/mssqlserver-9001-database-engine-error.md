---
title: MSSQLSERVER_9001 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 22767609a0281cc21a38d51716661ac98a8ffc24
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68118373"
---
# <a name="mssqlserver_9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9001|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LOG_NOT_AVAIL|  
|메시지 텍스트|데이터베이스 '%.*ls'의 로그를 사용할 수 없습니다. 관련 오류 메시지의 이벤트 로그를 확인하십시오. 모든 오류를 해결하고 데이터베이스를 다시 시작하십시오.|  
  
## <a name="explanation"></a>설명  
데이터베이스 로그가 오프라인 상태가 되었습니다. 일반적으로 이 상태는 데이터베이스를 다시 시작해야 하는 치명적인 오류가 발생했음을 나타냅니다.  
  
## <a name="user-action"></a>사용자 동작  
다른 오류를 진단하고 SQL Server 인스턴스가 아직 다시 시작되지 않은 경우 이를 다시 시작합니다.  
  
