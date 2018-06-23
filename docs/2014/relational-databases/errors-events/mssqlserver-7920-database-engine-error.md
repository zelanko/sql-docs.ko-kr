---
title: MSSQLSERVER_7920 | Microsoft 문서
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
- 7920 (Database Engine error)
ms.assetid: d16290ea-3875-4148-8d53-057bfee00438
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bcb388953f3795fb8f654107a414ca4c7587df8d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184284"
---
# <a name="mssqlserver7920"></a>MSSQLSERVER_7920
    
## <a name="details"></a>설명  
  
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
  
  