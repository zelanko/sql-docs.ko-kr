---
title: MSSQLSERVER_2538 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bc66239e7147d7701303fde2ddaa6506b07bba2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431832"
---
# <a name="mssqlserver2538"></a>MSSQLSERVER_2538
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2538|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|메시지 텍스트|파일 FILE. 익스텐트 수 = EXTENTS, 사용된 페이지 = USED_PAGES, 예약된 페이지 = RESERVED_PAGES.|  
  
## <a name="explanation"></a>설명  
 이 정보는 DBCC CHECKALLOC 명령에 대한 출력의 일부로, 지정된 데이터베이스에 대해 할당된 익스텐트, 사용된 페이지 및 예약된 페이지를 파일별로 요약하여 보여 줍니다.  
  
## <a name="user-action"></a>사용자 동작  
 InclusionThresholdSetting  
  
  
