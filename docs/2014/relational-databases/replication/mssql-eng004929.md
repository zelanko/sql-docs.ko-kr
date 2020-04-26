---
title: MSSQL_ENG004929 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 526c5b0bb1b7c5dd0d7cf1485f7e399b6f1fbff9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62666978"
---
# <a name="mssql_eng004929"></a>MSSQL_ENG004929
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|4929|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|%S_MSG '%.*ls'은(는) 복제용으로 게시 중이므로 변경할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 일반적으로 트랜잭션 복제용으로 게시되는 테이블의 PRIMARY KEY 제약 조건을 삭제하려고 할 때 발생합니다. 트랜잭션 복제를 사용하려면 게시된 각 테이블의 기본 키가 필요하므로 이 제약 조건은 삭제할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 제약 조건을 삭제하려면 해당 테이블과 연결된 아티클을 먼저 삭제합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요. 복제되지 않은 데이터베이스에서 오류가 발생한 경우 [sp_removedbreplication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)을 실행하여 데이터베이스의 개체가 복제된 것으로 표시되지 않도록 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
