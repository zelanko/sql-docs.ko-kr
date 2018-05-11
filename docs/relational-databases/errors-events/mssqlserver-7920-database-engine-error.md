---
title: MSSQLSERVER_7920 | Microsoft 문서
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
- 7920 (Database Engine error)
ms.assetid: d16290ea-3875-4148-8d53-057bfee00438
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2fab1d56794ae72d1e7122bfd2ca48d181181a6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver7920"></a>MSSQLSERVER_7920
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7920|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_SUMMARY_ENTRIES|  
|메시지 텍스트|데이터베이스 ID D_ID의 시스템 카탈로그에서 ENTRY_COUNT개 항목을 처리했습니다.|  
  
## <a name="explanation"></a>설명  
DBCC CHECKALLOC을 제외한 모든 DBCC CHECK 명령에서 반환하는 정보 메시지입니다. 반환되는 값은 검사 대상 행 집합의 총 개수입니다.  
  
## <a name="user-action"></a>사용자 동작  
InclusionThresholdSetting  
  
