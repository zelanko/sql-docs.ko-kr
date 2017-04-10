---
title: "스냅숏 속성 구성(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "스냅숏 [SQL Server 복제], 속성"
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 스냅숏 속성 구성(복제 Transact-SQL 프로그래밍)
  복제 저장 프로시저를 사용하여 스냅숏 속성을 프로그래밍 방식으로 정의 및 수정할 수 있습니다. 사용되는 저장 프로시저는 게시 유형에 따라 달라집니다.  
  
### 스냅숏 또는 트랜잭션 게시를 만들 때 스냅숏 속성을 구성하려면  
  
1.  게시자에서 실행 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)합니다. 에 대 한 게시 이름 **@publication**, 값 **스냅숏** 또는 **연속** 에 대 한 **@repl_freq**, 하나 이상의 다음 스냅숏 관련 매개 변수 중:  
  
    -   **@alt_snapshot_folder** -이 게시에 대 한 스냅숏 대신 또는 기본 스냅숏 폴더 외에도 해당 위치에서 액세스 하는 경우 경로 지정 합니다.  
  
    -   **@compress_snapshot** -값을 지정 **true** 대체 스냅숏 폴더에 있는 스냅숏 파일의 압축 되는 경우는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB 파일 형식입니다.  
  
    -   **@pre_snapshot_script** -의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏이 적용 되기 전에 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **@post_snapshot_script** -의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **@snapshot_in_defaultfolder** -값을 지정 **false** 경우 스냅숏에 기본이 아닌 위치 에서만에서 사용할 수 있습니다.  
  
     게시를 만드는 방법은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
### 병합 게시를 만들 때 스냅숏 속성을 구성하려면  
  
1.  게시자에서 실행 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. 에 대 한 게시 이름 **@publication**, 값 **스냅숏** 또는 **연속** 에 대 한 **@repl_freq**, 하나 이상의 다음 스냅숏 관련 매개 변수 중:  
  
    -   **@alt_snapshot_folder** -이 게시에 대 한 스냅숏 대신 또는 기본 스냅숏 폴더 외에도 해당 위치에서 액세스 하는 경우 경로 지정 합니다.  
  
    -   **@compress_snapshot** -값을 지정 **true** 대체 스냅숏 폴더의 스냅숏 파일이 CAB 파일 형식으로 압축 되는 경우.  
  
    -   **@pre_snapshot_script** -의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏이 적용 되기 전에 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **@post_snapshot_script** -의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **@snapshot_in_defaultfolder** -값을 지정 **false** 경우 스냅숏에 기본이 아닌 위치 에서만에서 사용할 수 있습니다.  
  
2.  게시를 만드는 방법은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
### 기존 스냅숏 또는 트랜잭션 게시의 스냅숏 속성을 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 는 다음 값 중 하나에 대 한 고 **@property**:  
  
    -   **alt_snapshot_folder** -새 경로 대 한 대체 스냅숏 폴더를 지정할 수도 **@value**합니다.  
  
    -   **compress_snapshot** -의 값도 지정 **true** 또는 **false** 에 대 한 **@value** 대체 스냅숏 폴더의 스냅숏 파일이 CAB 파일 형식으로 압축 됩니다 있는지 여부를 나타냅니다.  
  
    -   **pre_snapshot_script** - **@value** 의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏이 적용 되기 전에 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **post_snapshot_script** - **@value** 의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **snapshot_in_defaultfolder** -의 값도 지정 **true** 또는 **false** 스냅숏에 기본이 아닌 위치 에서만에서 사용할 수 있는지 여부를 나타냅니다.  
  
2.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)합니다. 이때 변경할 **@publication** 및 하나 이상의 일정 또는 보안 자격 증명 매개 변수를 지정합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
3.  명령 프롬프트에서 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 를 실행하거나 스냅숏 에이전트 작업을 시작하여 새 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
### 기존 병합 게시의 스냅숏 속성을 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)합니다. 값을 지정 **1** 에 대 한 **@force_invalidate_snapshot** 는 다음 값 중 하나에 대 한 고 **@property**:  
  
    -   **alt_snapshot_folder** -새 경로 대 한 대체 스냅숏 폴더를 지정할 수도 **@value**합니다.  
  
    -   **compress_snapshot** -의 값도 지정 **true** 또는 **false** 에 대 한 **@value** 대체 스냅숏 폴더의 스냅숏 파일이 CAB 파일 형식으로 압축 됩니다 있는지 여부를 나타냅니다.  
  
    -   **pre_snapshot_script** - **@value** 의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏이 적용 되기 전에 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **post_snapshot_script** - **@value** 의 전체 경로 파일 이름을 지정는 **.sql** 파일을 초기 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행 됩니다.  
  
    -   **snapshot_in_defaultfolder** -의 값도 지정 **true** 또는 **false** 스냅숏에 기본이 아닌 위치 에서만에서 사용할 수 있는지 여부를 나타냅니다.  
  
2.  명령 프롬프트에서 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 를 실행하거나 스냅숏 에이전트 작업을 시작하여 새 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
## 예제  
 이 예제에서는 대체 스냅숏 폴더 및 압축 스냅숏을 사용하는 게시를 만듭니다.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## 참고 항목  
 [대체 스냅숏 폴더 위치](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [압축 스냅숏](../../../relational-databases/replication/compressed-snapshots.md)   
 [스냅숏 적용 전후에 스크립트 실행](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [FTP를 통해 스냅숏 전송](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  