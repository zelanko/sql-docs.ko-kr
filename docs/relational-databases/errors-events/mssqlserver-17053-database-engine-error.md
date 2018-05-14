---
title: MSSQLSERVER_17053 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 50ab0081458e3d370741a46e8ab65b51ea61357a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17053|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|OS_ERROR|  
|메시지 텍스트|%ls: 운영 체제 오류 %ls이(가) 발생했습니다.|  
  
## <a name="explanation"></a>설명  
일반적인 운영 체제 오류가 발생했습니다.  결과 상태가 분명하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
일반적으로 이 오류는 다른 오류와 함께 발생하며 해당 오류를 진단하는 데 사용되어야 합니다. 이러한 오류의 예로는 데이터 또는 로그 파일 읽기/쓰기 실패, 레지스트리 읽기/쓰기 작업, 예기치 않은 Win32API 오류 등이 있습니다.  
  
