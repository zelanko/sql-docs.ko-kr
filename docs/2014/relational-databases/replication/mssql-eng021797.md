---
title: MSSQL_ENG021797 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021797 error
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 88f9fff576b52e83073bbf917a43edf0a7648086
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63023584"
---
# <a name="mssql_eng021797"></a>MSSQL_ENG021797
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21797|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%s'은(는) '컴퓨터\\로그인' 또는 '도메인\\로그인' 형식의 올바른 Windows 로그인이어야 합니다. '%s'에 대한 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 이 오류는 **@job_login** 매개 변수에 지정 된 값이 null 이거나 잘못 된 경우 다음 복제 저장 프로시저에 의해 발생 합니다. 이 오류는 **db_owner** 고정 데이터베이스 역할의 멤버가 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 스크립트를 실행하는 경우 발생할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 보안 모델이 변경되었으므로 이러한 스크립트를 업데이트해야 합니다.  
  
-   [sp_addlogreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)  
  
-   [sp_addqreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)  
  
-   [sp_addpublication_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)  
  
-   [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)  
  
-   [sp_addpullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)  
  
-   [sp_addmergepushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)  
  
-   [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)  
  
 이러한 저장 프로시저는 적절한 서버의 **sysadmin** 고정 서버 역할의 멤버나 적절한 데이터베이스의 **db_owner** 고정 데이터베이스 역할의 멤버만 실행할 수 있습니다. 저장 프로시저는 각각 에이전트 작업을 만들어 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정을 지정할 수 있게 해줍니다. 역할이 **sysadmin** 인 사용자의 경우 Windows 계정이 지정되어 있지 않더라도(계정이 지정된 경우에는 올바른 계정이어야 함) 에이전트 작업이 암시적으로 생성됩니다. 에이전트는 적절한 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정 컨텍스트 아래에서 실행됩니다. 계정이 반드시 필요한 것은 아니지만 에이전트에 대해 별도의 계정을 지정하는 것은 보안을 위한 최선의 구현 방법입니다. 자세한 내용은 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)을 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
 각 프로시저의 **@job_login** 매개 변수에 대해 올바른 Windows 계정을 지정 해야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가져온 복제 스크립트를 사용할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 필요한 저장 프로시저와 매개 변수를 포함하도록 스크립트를 업데이트합니다. 자세한 내용은 [복제 스크립트 업그레이드&#40;복제 Transact-SQL 프로그래밍&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
