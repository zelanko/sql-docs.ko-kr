---
title: sp_mergecleanupmetadata (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0196993f863d973e14834f7eb3b93b797a825ac4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907331"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_update_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서비스 팩 1 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 이전 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행 하는 서버가 포함 된 복제 토폴로지에서만 사용 해야 합니다. **sp_mergecleanupmetadata** 를 사용 하면 관리자가 **MSmerge_genhistory**, **MSmerge_contents** 및 **MSmerge_tombstone** 시스템 테이블의 메타 데이터를 정리할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "토픽 링크 아이콘") [Transact-sql 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 모든 게시에 대 한 메타 데이터를 정리 하는 **%** 입니다. 명시적으로 지정된 경우에는 반드시 게시가 이미 존재하고 있어야 합니다.  
  
구독자를 다시 초기화할 지 여부를 지정 `[ @reinitialize_subscriber = ] 'subscriber'` 합니다. *구독자* 는 **nvarchar (5)** 이며 **true** 또는 **FALSE**일 수 있으며 기본값은 **true**입니다. **TRUE**이면 구독을 다시 초기화 하도록 표시 합니다. **FALSE**이면 구독을 다시 초기화 하도록 표시 하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_mergecleanupmetadata** 는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 이전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 실행 하는 서버가 포함 된 복제 토폴로지에서만 사용 해야 합니다. [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 1 이상 버전만 포함하는 토폴로지는 자동 보존 기반 메타데이터 정리를 사용해야 합니다. 이 저장 프로시저를 실행할 때는 저장 프로시저가 실행되는 컴퓨터에서 로그 파일이 크게 증가할 가능성이 있다는 점에 주의해야 합니다.  
  
> [!CAUTION]
>  **Sp_mergecleanupmetadata** 를 실행 한 후에는 기본적으로 **MSmerge_genhistory**, **MSmerge_contents** 및 **MSmerge_tombstone** 에 저장 된 메타 데이터가 있는 게시 구독자의 모든 구독이에 대해로 표시 됩니다. 다시 초기화 하면 구독자에서 보류 중인 변경 내용이 손실 되 고 현재 스냅숏은 더 이상 사용 되지 않는 것으로 표시 됩니다.  
> 
> [!NOTE]
>  데이터베이스에 게시가 여러 개 있고 이러한 게시 중 하나가 무한 게시 보존 기간 ( **\@보존**=**0**)을 사용 하는 경우 **sp_mergecleanupmetadata** 를 실행 하면 병합이 정리 되지 않습니다. 데이터베이스에 대 한 복제 변경 내용 추적 메타 데이터입니다. 그러므로 무한 게시 보존은 신중히 사용하십시오.  
  
 이 저장 프로시저를 실행할 때 **\@reinitialize_subscriber** 매개 변수를 **TRUE** (기본값) 또는 **FALSE**로 설정 하 여 구독자를 다시 초기화할 지 여부를 선택할 수 있습니다. **\@reinitialize_subscriber** 매개 변수를 **TRUE**로 설정 하 여 **sp_mergecleanupmetadata** 를 실행 하는 경우 초기 스냅숏 없이 구독을 만든 경우에도 스냅숏이 구독자에서 다시 적용 됩니다 (예: 스냅숏 데이터 및 스키마가 수동으로 적용 되었거나 구독자에 이미 존재 합니다. 게시를 다시 초기화 하지 않을 경우 게시자 및 구독자의 데이터가 동기화 되도록 하려면 매개 변수를 **FALSE** 로 설정 해야 합니다.  
  
 **\@reinitialize_subscriber**의 값에 관계 없이 저장 된 시간에 게시자 또는 재게시 구독자에 변경 내용을 업로드 하려고 하는 진행 중인 병합 프로세스가 있는 경우 **sp_mergecleanupmetadata** 는 실패 합니다. 프로시저를 호출 합니다.  
  
 **\@reinitialize_subscriber = TRUE를 사용 하 여 sp_mergecleanupmetadata를 실행 합니다.**  
  
1.  필수는 아니지만 게시 및 구독 데이터베이스에 대한 모든 업데이트를 중지하는 것이 좋습니다. 업데이트가 계속될 경우 게시를 다시 초기화할 때 마지막 병합 이후 구독자에 업데이트된 내용이 모두 손실되지만 데이터 일치성은 유지됩니다.  
  
2.  병합 에이전트를 실행하여 병합을 실행합니다. 병합 에이전트를 실행할 때 각 구독자에서 **-Validate** agent 명령줄 옵션을 사용 하는 것이 좋습니다. 연속 모드 병합을 실행 하는 경우이 섹션의 뒷부분에 나오는 *연속 모드 병합에 대 한 특별 고려 사항* 을 참조 하세요.  
  
3.  모든 병합이 완료 되 면 **sp_mergecleanupmetadata**를 실행 합니다.  
  
4.  명명 된 끌어오기 또는 익명 끌어오기 구독을 사용 하 여 모든 구독자에서 **sp_reinitmergepullsubscription** 을 실행 하 여 데이터 일치성을 보장 합니다.  
  
5.  연속 모드 병합을 실행 하는 경우이 섹션의 뒷부분에 나오는 *연속 모드 병합에 대 한 특별 고려 사항* 을 참조 하세요.  
  
6.  모든 수준에 관련된 모든 병합 게시에 대해 스냅샷 파일을 다시 생성합니다. 스냅샷을 먼저 다시 생성하지 않고 병합을 시도하면 스냅샷을 다시 생성하라는 메시지가 표시됩니다.  
  
7.  게시 데이터베이스를 백업합니다. 그렇게 하지 않으면 게시 데이터베이스 복원 후 병합이 실패할 수도 있습니다.  
  
 **\@reinitialize_subscriber = FALSE 인 sp_mergecleanupmetadata를 실행 합니다.**  
  
1.  게시 및 구독 데이터베이스에 대 한 **모든** 업데이트를 중지 합니다.  
  
2.  병합 에이전트를 실행하여 병합을 실행합니다. 병합 에이전트를 실행할 때 각 구독자에서 **-Validate** agent 명령줄 옵션을 사용 하는 것이 좋습니다. 연속 모드 병합을 실행 하는 경우이 섹션의 뒷부분에 나오는 *연속 모드 병합에 대 한 특별 고려 사항* 을 참조 하세요.  
  
3.  모든 병합이 완료 되 면 **sp_mergecleanupmetadata**를 실행 합니다.  
  
4.  연속 모드 병합을 실행 하는 경우이 섹션의 뒷부분에 나오는 *연속 모드 병합에 대 한 특별 고려 사항* 을 참조 하세요.  
  
5.  모든 수준에 관련된 모든 병합 게시에 대해 스냅샷 파일을 다시 생성합니다. 스냅샷을 먼저 다시 생성하지 않고 병합을 시도하면 스냅샷을 다시 생성하라는 메시지가 표시됩니다.  
  
6.  게시 데이터베이스를 백업합니다. 그렇게 하지 않으면 게시 데이터베이스 복원 후 병합이 실패할 수도 있습니다.  

 **연속 모드 병합에 대 한 특별 고려 사항**  
  
 연속 모드 병합을 실행하는 경우 다음 중 하나를 실행해야 합니다.  
  
-   병합 에이전트를 중지 하 고 **-연속** 매개 변수를 지정 하지 않고 다른 병합을 수행 합니다.  
  
-   **Sp_changemergepublication** 을 사용 하 여 게시를 비활성화 하 여 게시 상태를 폴링하는 연속 모드 병합이 실패 하는지 확인 합니다.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 **Sp_mergecleanupmetadata**실행 중 3 단계를 완료 한 후에는 중지 된 방법에 따라 연속 모드 병합을 다시 시작 합니다. 다음 중 하나를 실행하십시오.  
  
-   병합 에이전트에 대 한 **연속** 매개 변수를 다시 추가 합니다.  
  
-   Sp_changemergepublication을 사용 하 여 게시를 다시 활성화 **합니다.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_mergecleanupmetadata**을 실행할 수 있습니다.  
  
 이 저장 프로시저를 사용하려면 게시자는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]을 실행해야 합니다. 구독자는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, 서비스 팩 2 중 하나를 실행 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MSmerge_genhistory &#40;transact-sql&#41; ](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;transact-sql&#41; ](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
