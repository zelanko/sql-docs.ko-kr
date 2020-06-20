---
title: MSSQL_ENG021385 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021385 error
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2d137fceaed44ebe79ca1e5d3735681539e3a462
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010081"
---
# <a name="mssql_eng021385"></a>MSSQL_ENG021385
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21385|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|스냅샷이 게시 '%s'을(를) 처리하지 못했습니다. 활성 스키마 변경 작업 또는 추가 중인 새 아티클 때문인 것 같습니다.|  
  
## <a name="explanation"></a>설명  
 아티클 추가 또는 삭제 및 게시된 개체의 스키마 변경 등 게시 데이터베이스에 진행 중인 변경 내용이 있을 때 스냅샷 에이전트가 실행되면 이 오류가 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 게시 데이터베이스에 대한 변경이 완료된 후에 스냅샷 에이전트를 다시 시작합니다. 자세한 내용은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
