---
title: MSSQLSERVER_17132 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 98adeaf240768a3ff7753796718cb6ddd6b233a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62645177"
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17132|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|INIT_NODESSPACE|  
|메시지 텍스트|설명자에 대한 메모리가 부족하여 서버를 시작하지 못했습니다. 불필요한 메모리 로드를 줄이거나 시스템 메모리를 늘리십시오.|  
  
## <a name="explanation"></a>설명  
서버 내부 설명자를 저장할 충분한 메모리를 할당하는 데 실패했습니다.  
  
## <a name="user-action"></a>사용자 동작  
시스템에 메모리를 더 많이 추가합니다. 일반적인 메모리 문제 해결 단계가 유용할 수 있습니다.  
  
