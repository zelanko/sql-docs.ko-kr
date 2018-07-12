---
title: MSSQLSERVER_2539 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b470cdf2ae08029d92467a93e9df9adb83f95c43
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417872"
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
  
  
