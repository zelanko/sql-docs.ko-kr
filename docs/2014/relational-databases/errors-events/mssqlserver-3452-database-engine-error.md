---
title: MSSQLSERVER_3452 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e811d36160cf0a4477452acec336c61bf52e793
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868070"
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3452|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|REC_CHECKIDENTITY|  
|메시지 텍스트|데이터베이스 '%.*ls'(%d)을(를) 복구하는 동안 테이블 ID %d에서 ID 값이 일치하지 않습니다. DBCC CHECKIDENT('%.\*ls')를 실행하세요.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하는 동안 데이터베이스의 ID 값을 복구하기 위한 프로세스에서 메타데이터의 불일치를 발견했습니다.  
  
## <a name="user-action"></a>사용자 동작  
 DBCC CHECKIDENT를 실행하십시오.  
  
  
