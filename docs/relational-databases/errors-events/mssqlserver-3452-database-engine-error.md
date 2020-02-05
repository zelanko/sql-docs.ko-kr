---
title: MSSQLSERVER_3452 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a11f78e1ef38e432ba2b999877e6e5384ac1f386
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68043662"
---
# <a name="mssqlserver_3452"></a>MSSQLSERVER_3452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
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
  
