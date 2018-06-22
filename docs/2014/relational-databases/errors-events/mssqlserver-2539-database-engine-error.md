---
title: MSSQLSERVER_2539 | Microsoft 문서
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
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9d346c85523bdcfd6e5ebd9f4aec5ba044b7d3b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088862"
---
# <a name="mssqlserver2539"></a>MSSQLSERVER_2539
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2539|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|메시지 텍스트|이 데이터베이스의 총 익스텐트 수 = EXTENTS, 사용된 페이지 = USED_PAGES, 예약된 페이지 = RESERVED_PAGES.|  
  
## <a name="explanation"></a>설명  
 이 정보는 DBCC CHECKALLOC 명령에 대한 출력의 일부로, 할당된 익스텐트, 사용된 페이지 및 지정된 데이터베이스에 대해 예약된 페이지를 요약해서 보여 줍니다.  
  
## <a name="user-action"></a>사용자 동작  
 InclusionThresholdSetting  
  
  