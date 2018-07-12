---
title: MSSQLSERVER_2593 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316228d2dffa4cfcaba0bd3e6356999d4052d21a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427442"
---
# <a name="mssqlserver2593"></a>MSSQLSERVER_2593
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2593|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_OBJECT_ROW_PAGE_SUMMARY|  
|메시지 텍스트|PAGECOUNT개 페이지에 개체 'OBJECT'에 대한 행이 ROWCOUNT개 있습니다.|  
  
## <a name="explanation"></a>설명  
 이 메시지는 DBCC CHECKALLOC을 제외한 모든 DBCC 검사에서 반환하는 출력 정보의 일부이며 지정된 개체의 행과 페이지 수를 나타냅니다.  
  
## <a name="user-action"></a>사용자 동작  
 InclusionThresholdSetting  
  
  
