---
title: MSSQL_ENG014120 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eb15b59a86b60d12d65716341062d6c670ad4a5f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299903"
---
# <a name="mssqleng014120"></a>MSSQL_ENG014120
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14120|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|배포 데이터베이스 '%s'을(를) 삭제할 수 없습니다. 이 배포자 데이터베이스가 게시자와 연관되어 있습니다.|  
  
## <a name="explanation"></a>설명  
 배포 데이터베이스는 트랜잭션 복제에 대한 모든 유형의 복제 및 트랜잭션에 대한 메타데이터와 기록 데이터를 저장합니다. 이 오류는 하나 이상의 게시자와 연결된 배포 데이터베이스를 삭제하려고 할 때 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 배포 데이터베이스를 삭제하려면 먼저 배포자와 게시자 간 연결을 삭제해야 합니다. 자세한 내용은 [sp_dropdistpublisher&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [배포 구성](configure-distribution.md)  
  
  
