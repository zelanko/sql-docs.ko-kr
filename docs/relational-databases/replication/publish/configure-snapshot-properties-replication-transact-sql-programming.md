---
title: 스냅샷 속성 구성(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b454197982685882610fc808d9319835053e21bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62661097"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>스냅샷 속성 구성(복제 Transact-SQL 프로그래밍)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  복제 저장 프로시저를 사용하여 스냅샷 속성을 프로그래밍 방식으로 정의 및 수정할 수 있습니다. 사용되는 저장 프로시저는 게시 유형에 따라 달라집니다.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시를 만들 때 스냅샷 속성을 구성하려면  
  
1.  게시자에서 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)을 실행합니다. 이때 **@publication** 에 게시 이름을 지정하고 **@repl_freq** 에 **snapshot** 또는 **@repl_freq** 를 지정하며 다음과 같은 스냅샷 관련 매개 변수를 하나 이상 지정합니다.  
  
    -   **@alt_snapshot_folder** - 이 게시에 대한 스냅숏을 기본 스냅숏 폴더 이외 위치 또는 기본 스냅숏 폴더에 추가된 위치에서 액세스하는 경우 경로를 지정합니다.    
    -   **@compress_snapshot** - 대체 스냅숏 폴더의 스냅숏 파일이 **CAB 파일 형식으로 압축되는 경우** true [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 값을 지정합니다.    
    -   **@pre_snapshot_script** - 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **@post_snapshot_script** - 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **@snapshot_in_defaultfolder** - 대체 스냅숏 폴더의 스냅숏 파일이 **false** 값을 지정합니다.  
  
     게시를 만드는 방법은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>병합 게시를 만들 때 스냅샷 속성을 구성하려면  
  
1.  게시자에서 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행합니다. 이때 **@publication** 에 게시 이름을 지정하고 **@repl_freq** 에 **snapshot** 또는 **@repl_freq** 를 지정하며 다음과 같은 스냅샷 관련 매개 변수를 하나 이상 지정합니다.  
  
    -   **@alt_snapshot_folder** - 이 게시에 대한 스냅숏을 기본 스냅숏 폴더 이외 위치 또는 기본 스냅숏 폴더에 추가된 위치에서 액세스하는 경우 경로를 지정합니다.    
    -   **@compress_snapshot** - 대체 스냅숏 폴더의 스냅숏 파일이 **CAB 파일 형식으로 압축되는 경우** 값을 지정합니다.   
    -   **@pre_snapshot_script** - 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **@post_snapshot_script** - 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **@snapshot_in_defaultfolder** - 대체 스냅숏 폴더의 스냅숏 파일이 **false** 값을 지정합니다.  
  
2.  게시를 만드는 방법은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>기존 스냅샷 또는 트랜잭션 게시의 스냅샷 속성을 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다. 이때 **@force_invalidate_snapshot** 또는 **@force_invalidate_snapshot** 을 지정하고 **@property** 에 다음 값 중 하나를 지정합니다.  
  
    -   **alt_snapshot_folder** - **@value** 을 실행합니다.    
    -   **compress_snapshot** - **CAB 파일 형식으로 압축되는 경우** 에 **false** 또는 **@value** 값을 지정합니다.    
    -   **pre_snapshot_script** - **@value** 에도 마찬가지로 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **post_snapshot_script** - **@value** 에도 마찬가지로 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **snapshot_in_defaultfolder** - 마찬가지로 스냅숏을 기본 위치 이외 위치에서만 사용할 수 있는지 여부를 나타내는 **true** 또는 **false** 값을 지정합니다.  
  
2.  (옵션) 게시 데이터베이스의 게시자에서 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)을 실행합니다. 이때 변경할 **@publication** 및 하나 이상의 일정 또는 보안 자격 증명 매개 변수를 지정합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
3.  명령 프롬프트에서 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 를 실행하거나 스냅샷 에이전트 작업을 시작하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>기존 병합 게시의 스냅샷 속성을 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 실행합니다. 이때 **@force_invalidate_snapshot** 또는 **@force_invalidate_snapshot** 을 지정하고 **@property** 에 다음 값 중 하나를 지정합니다.  
  
    -   **alt_snapshot_folder** - **@value** 을 실행합니다.    
    -   **compress_snapshot** - **CAB 파일 형식으로 압축되는 경우** 에 **false** 또는 **@value** 값을 지정합니다.    
    -   **pre_snapshot_script** - **@value** 에도 마찬가지로 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **post_snapshot_script** - **@value** 에도 마찬가지로 초기 스냅숏을 적용하기 전에 초기화하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정합니다.    
    -   **snapshot_in_defaultfolder** - 마찬가지로 스냅숏을 기본 위치 이외 위치에서만 사용할 수 있는지 여부를 나타내는 **true** 또는 **false** 값을 지정합니다.  
  
2.  명령 프롬프트에서 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 를 실행하거나 스냅샷 에이전트 작업을 시작하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 이 예제에서는 대체 스냅샷 폴더 및 압축 스냅샷을 사용하는 게시를 만듭니다.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [스냅숏 옵션 수정](../../../relational-databases/replication/snapshot-options.md)   
 [스냅숏 적용 전후에 스크립트 실행](../../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [FTP를 통해 스냅숏 전송](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  
