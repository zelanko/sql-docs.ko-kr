---
title: "MSSQLSERVER_9003 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 27d2fbf1bed8445eb8d3fd42000128741d2ee377
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9003|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LOG_INVALID_LSN|  
|메시지 텍스트|데이터베이스 '%.*ls'의 로그 검색으로 전달된 로그 검색 번호 %S_LSN이(가) 잘못되었습니다. 데이터가 손상되었거나 로그 파일(.ldf)과 데이터 파일(.mdf)이 일치하지 않음을 나타냅니다. 복제하는 동안 이 오류가 발생한 경우 게시를 다시 만드십시오. 그 외의 경우 이 문제로 인해 시작하는 동안 오류가 발생하면 백업을 사용하여 복원하십시오.|  
  
## <a name="explanation"></a>설명  
구성 요소가 데이터베이스의 로그 관리자에 잘못된 로그 시퀀스 번호를 전달했습니다. 이는 복제, 손상 또는 주 데이터 파일과 로그 간의 불일치일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
복제하는 동안 이 오류가 발생한 경우 게시를 다시 만듭니다. 그렇지 않으면 백업에서 복원합니다.  
  

