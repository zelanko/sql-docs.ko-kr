---
title: MSSQLSERVER_9001 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c1b57637cee601cde328bc079ab907629591b5f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092008"
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
    
## <a name="details"></a>설명  
  
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
  
  