---
title: "MSSQL_ENG020596 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31988681a6777be1de8dae137968c9837860aaf7
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
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
 익명 구독에 대한 에이전트를 삭제할 권한이 없습니다. [sp_dropanonymousagent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md)를 호출할 때 사용된 로그인은 배포자의 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스의 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다. 또는 사용자가 에이전트를 처음 실행한 사용자여야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
 올바른 자격 증명으로 로그인하고 **sp_dropanonymousagent**를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
