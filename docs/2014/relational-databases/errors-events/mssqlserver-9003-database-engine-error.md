---
title: MSSQLSERVER_9003 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6f67e4184ea54be6bcd5c2a74d3c0e0711b702f2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031424"
---
# <a name="mssqlserver_9003"></a>MSSQLSERVER_9003
    
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
  
  
