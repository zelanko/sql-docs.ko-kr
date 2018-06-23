---
title: MSSQL_ENG020596 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c512a34d2eacd44c6f03e5bc9b72f48f5f1676d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183215"
---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20596|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%s' 또는 db_owner의 멤버만 익명 에이전트를 삭제할 수 있습니다.|  
  
## <a name="explanation"></a>설명  
 익명 구독에 대한 에이전트를 삭제할 권한이 없습니다. [sp_dropanonymousagent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql)를 호출할 때 사용된 로그인은 배포자의 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스의 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다. 또는 사용자가 에이전트를 처음 실행한 사용자여야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
 올바른 자격 증명으로 로그인하고 **sp_dropanonymousagent**를 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
