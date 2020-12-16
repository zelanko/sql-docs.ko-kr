---
description: MSSQL_ENG021798
title: MSSQL_ENG021798 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021798 error
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: dc233cde39917a65a946b1c4e112fdc0833c48cd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469064"
---
# <a name="mssql_eng021798"></a>MSSQL_ENG021798
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21798|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|계속하려면 먼저 '%s'을(를) 통해 '%s' 에이전트 작업을 추가해야 합니다. '%s'에 대한 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 게시를 만들려면 게시자의 **sysadmin** 고정 서버 역할의 멤버 또는 게시 데이터베이스의 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다. **db_owner** 역할의 멤버인 경우 다음과 같은 상황에서 이 오류가 발생합니다.  
  
-   [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서 스크립트를 실행하십시오. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 보안 모델이 변경되었으므로 이러한 스크립트를 업데이트해야 합니다.  
  
-   저장 프로시저 **sp_addpublication** 은 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)가 실행되기 전에 실행됩니다. 이 조건은 모든 트랜잭션 게시에 적용됩니다.  
  
-   저장 프로시저 **sp_addpublication** 은 [sp_addqreader_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)가 실행되기 전에 실행됩니다. 이 조건은 지연 업데이트 구독에 사용하도록 설정된 트랜잭션 게시에 적용됩니다(**sp_addpublication** 의 `@allow_queued_tran` 매개 변수에 TRUE 값 지정).  
  
 저장 프로시저 **sp_addlogreader_agent** 와 **sp_addqreader_agent** 는 각각 에이전트 작업을 만들고 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정을 지정할 수 있게 해줍니다. **sysadmin** 역할의 사용자인 경우 **sp_addlogreader_agent** 와 **sp_addqreader_agent** 가 실행되지 않으면 에이전트 작업이 암시적으로 생성됩니다. 에이전트는 배포자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 컨텍스트에서 실행됩니다. **sysadmin** 역할의 사용자에 **sp_addlogreader_agent** 와 **sp_addqreader_agent** 가 필요한 것은 아니지만 에이전트에 대해 별도의 계정을 지정하는 것이 보안을 위한 최선의 구현 방법입니다. 자세한 내용은 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
 프로시저를 올바른 순서로 실행하십시오. 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가져온 복제 스크립트를 사용할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에 필요한 저장 프로시저와 매개 변수를 포함하도록 스크립트를 업데이트합니다. 자세한 내용은 [복제 스크립트 업그레이드&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
