---
title: sp_mergecleanupmetadata (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 026675528003028ffd3fd73301f47f75bcab0575
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33002160"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_update_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  버전을 실행 하는 서버가 포함 된 복제 토폴로지에서 사용 해야 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전에 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 1. **sp_mergecleanupmetadata** 관리자 사용에 대 한 메타 데이터를 정리할 수 있습니다는 **MSmerge_genhistory**, **MSmerge_contents** 및 **MSmerge_tombstone** 시스템 테이블입니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication =** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 **%**, 모든 게시에 대 한 메타 데이터를 정리 하는 합니다. 명시적으로 지정된 경우에는 반드시 게시가 이미 존재하고 있어야 합니다.  
  
 [  **@reinitialize_subscriber =** ] **'***구독자***'**  
 구독자를 다시 초기화할지 여부를 지정합니다. *구독자* 은 **nvarchar (5)**, 수 **TRUE** 또는 **FALSE**, 기본값은 **TRUE**합니다. 경우 **TRUE**, 구독 다시 초기화 되도록 표시 됩니다. 경우 **FALSE**, 구독 다시 초기화 되도록 표시 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_mergecleanupmetadata** 의 버전을 실행 하는 서버가 포함 된 복제 토폴로지에서 사용 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전에 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 1입니다. [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 1 이상 버전만 포함하는 토폴로지는 자동 보존 기반 메타데이터 정리를 사용해야 합니다. 이 저장 프로시저를 실행할 때는 저장 프로시저가 실행되는 컴퓨터에서 로그 파일이 크게 증가할 가능성이 있다는 점에 주의해야 합니다.  
  
> [!CAUTION]  
>  후 **sp_mergecleanupmetadata** 실행 되는 기본적으로 메타 데이터에 저장 된 게시의 구독자에서 모든 구독 **MSmerge_genhistory**, **MSmerge_contents**  및 **MSmerge_tombstone** 표시 되어 다시 초기화에 대 한 구독자에서 보류 중인 변경 내용이 손실 되 고 현재 스냅숏에 것으로 표시 됩니다.  
  
> [!NOTE]  
>  데이터베이스에 게시가 여러 개 및 이러한 게시 중 하나가 무한 게시 보존 기간을 사용 하는 경우 (**@retention**=**0**)에서 실행 되며,  **sp_mergecleanupmetadata** 병합 복제 변경 내용 추적 데이터베이스에 대 한 메타 데이터 정리 하지 않습니다. 그러므로 무한 게시 보존은 신중히 사용하십시오.  
  
 이 저장 프로시저 실행 시를 설정 하 여 구독자를 다시 초기화할 지 여부를 선택할 수 있습니다는 **@reinitialize_subscriber** 매개 변수를 **TRUE** (기본값) 또는 **FALSE**. 경우 **sp_mergecleanupmetadata** 로 실행 되는 **@reinitialize_subscriber** 매개 변수 설정 **TRUE**, 구독 된 경우에 구독자에서 스냅숏을 다시 적용 됩니다 초기 스냅숏 (예를 들어 경우 스냅숏 데이터와 스키마 수동으로 적용 되었거나 이미 구독자에 존재 됩니다) 없이 만들어집니다. 이 매개 변수 설정 **FALSE** 게시가 다시 초기화 되지 않습니다 경우 게시자와 구독자의 데이터가 동기화 되었는지 확인 해야 하기 때문에, 주의 해 서 사용 해야 합니다.  
  
 값에 관계 없이 **@reinitialize_subscriber**, **sp_mergecleanupmetadata** 병합 게시자 또는 재게시 구독자에서 변경 내용을 업로드 하는 프로세스 실패 작업이 진행 중 저장된 프로시저가 호출 되는 시간입니다.  
  
 **Sp_mergecleanupmetadata를 실행 @reinitialize_subscriber = TRUE.**  
  
1.  필수는 아니지만 게시 및 구독 데이터베이스에 대한 모든 업데이트를 중지하는 것이 좋습니다. 업데이트가 계속될 경우 게시를 다시 초기화할 때 마지막 병합 이후 구독자에 업데이트된 내용이 모두 손실되지만 데이터 일치성은 유지됩니다.  
  
2.  병합 에이전트를 실행하여 병합을 실행합니다. 사용 하는 것이 좋습니다는 **– 유효성 검사** 병합 에이전트를 실행할 때 각 구독자에서 에이전트 명령줄 옵션입니다. 연속 모드 병합을 실행 하는 경우 참조 *연속 모드 병합에 대 한 특별 고려 사항* 이 섹션의 뒷부분에 나오는 합니다.  
  
3.  모든 병합을 완료 한 후에 실행 **sp_mergecleanupmetadata**합니다.  
  
4.  실행 **sp_reinitmergepullsubscription** 익명 또는 명명 된 끌어오기 구독을 사용 하 여 데이터 일치성을 유지 하는 모든 구독자에 있습니다.  
  
5.  연속 모드 병합을 실행 하는 경우 참조 *연속 모드 병합에 대 한 특별 고려 사항* 이 섹션의 뒷부분에 나오는 합니다.  
  
6.  모든 수준에 관련된 모든 병합 게시에 대해 스냅숏 파일을 다시 생성합니다. 스냅숏을 먼저 다시 생성하지 않고 병합을 시도하면 스냅숏을 다시 생성하라는 메시지가 표시됩니다.  
  
7.  게시 데이터베이스를 백업합니다. 그렇게 하지 않으면 게시 데이터베이스 복원 후 병합이 실패할 수도 있습니다.  
  
 **Sp_mergecleanupmetadata를 실행 @reinitialize_subscriber = FALSE.**  
  
1.  중지 **모든** 게시 및 구독 데이터베이스에 대 한 업데이트 합니다.  
  
2.  병합 에이전트를 실행하여 병합을 실행합니다. 사용 하는 것이 좋습니다는 **– 유효성 검사** 병합 에이전트를 실행할 때 각 구독자에서 에이전트 명령줄 옵션입니다. 연속 모드 병합을 실행 하는 경우 참조 *연속 모드 병합에 대 한 특별 고려 사항* 이 섹션의 뒷부분에 나오는 합니다.  
  
3.  모든 병합을 완료 한 후에 실행 **sp_mergecleanupmetadata**합니다.  
  
4.  연속 모드 병합을 실행 하는 경우 참조 *연속 모드 병합에 대 한 특별 고려 사항* 이 섹션의 뒷부분에 나오는 합니다.  
  
5.  모든 수준에 관련된 모든 병합 게시에 대해 스냅숏 파일을 다시 생성합니다. 스냅숏을 먼저 다시 생성하지 않고 병합을 시도하면 스냅숏을 다시 생성하라는 메시지가 표시됩니다.  
  
6.  게시 데이터베이스를 백업합니다. 그렇게 하지 않으면 게시 데이터베이스 복원 후 병합이 실패할 수도 있습니다.  
  
 **연속 모드 병합에 대 한 특별 고려 사항**  
  
 연속 모드 병합을 실행하는 경우 다음 중 하나를 실행해야 합니다.  
  
-   병합 에이전트를 중지 한 다음 하지 않고 다른 병합을 수행 하는 **-연속** 매개 변수를 지정 합니다.  
  
-   사용 하 여 게시를 비활성화 **sp_changemergepublication** 게시 상태를 폴링하고 모든 연속 모드 병합에 실패 하도록 합니다.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 완료 했을 때 실행의 3 단계 **sp_mergecleanupmetadata**, 연속 모드 병합을 중단 한 방법에 따라 다시 시작 합니다. 다음 중 하나를 실행하십시오.  
  
-   추가 **-Continuous** 병합 에이전트에 대 한 다시 매개 변수입니다.  
  
-   사용 하 여 게시를 다시 활성화 **sp_changemergepublication 합니다.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_mergecleanupmetadata**합니다.  
  
 이 저장 프로시저를 사용하려면 게시자는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]을 실행해야 합니다. 구독자에서 실행 해야 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, 서비스 팩 2입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MSmerge_genhistory &#40;Transact SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
