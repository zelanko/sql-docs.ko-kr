---
title: 스냅샷 속성 구성(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: b03dd7f886cee5816d591034d1be63ece45d8d1d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63021334"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>스냅샷 속성 구성(복제 Transact-SQL 프로그래밍)
  복제 저장 프로시저를 사용하여 스냅샷 속성을 프로그래밍 방식으로 정의 및 수정할 수 있습니다. 사용되는 저장 프로시저는 게시 유형에 따라 달라집니다.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시를 만들 때 스냅샷 속성을 구성하려면  
  
1.  게시자에서 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)을 실행합니다. 에 **@publication**게시 이름을 지정 하 고, **스냅숏** 또는 **연속** 값을 지정 하 **@repl_freq**고, 다음 스냅숏 관련 매개 변수 중 하나 이상을 지정 합니다.  
  
    -   **@alt_snapshot_folder**-이 게시에 대 한 스냅숏이 스냅숏 기본 폴더 대신 또는 해당 위치에서 액세스 되는 경우 경로를 지정 합니다.  
  
    -   **@compress_snapshot**-대체 스냅숏 폴더의 **true** 스냅숏 파일이 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB 파일 형식으로 압축 되는 경우 true 값을 지정 합니다.  
  
    -   **@pre_snapshot_script**-초기 스냅숏을 적용 하기 전에 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정 합니다.  
  
    -   **@post_snapshot_script**-초기 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정 합니다.  
  
    -   **@snapshot_in_defaultfolder**-스냅숏이 기본 위치가 아닌 위치 에서만 사용 가능한 경우 **false** 값을 지정 합니다.  
  
     게시를 만드는 방법은 [Create a Publication](create-a-publication.md)를 참조하세요.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>병합 게시를 만들 때 스냅샷 속성을 구성하려면  
  
1.  게시자에서 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)을 실행합니다. 에 **@publication**게시 이름을 지정 하 고, **스냅숏** 또는 **연속** 값을 지정 하 **@repl_freq**고, 다음 스냅숏 관련 매개 변수 중 하나 이상을 지정 합니다.  
  
    -   **@alt_snapshot_folder**-이 게시에 대 한 스냅숏이 스냅숏 기본 폴더 대신 또는 해당 위치에서 액세스 되는 경우 경로를 지정 합니다.  
  
    -   **@compress_snapshot**-대체 스냅숏 폴더의 스냅숏 파일이 CAB 파일 형식으로 압축 되는 경우 **true** 값을 지정 합니다.  
  
    -   **@pre_snapshot_script**-초기 스냅숏을 적용 하기 전에 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정 합니다.  
  
    -   **@post_snapshot_script**-초기 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 이름 및 전체 경로를 지정 합니다.  
  
    -   **@snapshot_in_defaultfolder**-스냅숏이 기본 위치가 아닌 위치 에서만 사용 가능한 경우 **false** 값을 지정 합니다.  
  
2.  게시를 만드는 방법은 [Create a Publication](create-a-publication.md)를 참조하세요.  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>기존 스냅샷 또는 트랜잭션 게시의 스냅샷 속성을 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 실행합니다. 에 **@force_invalidate_snapshot** 값 **@property** **1** 을 지정 하 고에 다음 값 중 하나를 지정 합니다.  
  
    -   **alt_snapshot_folder** -에 대 한 **@value**대체 스냅숏 폴더의 새 경로를 지정 합니다.  
  
    -   **compress_snapshot** -대체 스냅숏 폴더의 스냅숏 파일이 CAB 파일 형식으로 **@value** 압축 되는지 여부를 나타내기 위해에 **true** 또는 **false** 값을 지정 합니다.  
  
    -   **pre_snapshot_script** -초기 스냅숏을 **@value** 적용 하기 전에 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 파일 이름 및 전체 경로를 지정 합니다.  
  
    -   **post_snapshot_script** -또한 초기 **@value** 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 파일 이름 및 전체 경로를 지정 합니다.  
  
    -   **snapshot_in_defaultfolder** - 마찬가지로 스냅샷을 기본 위치 이외 위치에서만 사용할 수 있는지 여부를 나타내는 **true** 또는 **false** 값을 지정합니다.  
  
2.  (옵션) 게시 데이터베이스의 게시자에서 [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)을 실행합니다. 및 **@publication** 하나 이상의 일정 또는 보안 자격 증명 매개 변수를 지정 합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
3.  명령 프롬프트에서 [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) 를 실행하거나 스냅샷 에이전트 작업을 시작하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>기존 병합 게시의 스냅샷 속성을 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)을 실행합니다. 에 **@force_invalidate_snapshot** 값 **@property** **1** 을 지정 하 고에 다음 값 중 하나를 지정 합니다.  
  
    -   **alt_snapshot_folder** -에 대 한 **@value**대체 스냅숏 폴더의 새 경로를 지정 합니다.  
  
    -   **compress_snapshot** -대체 스냅숏 폴더의 스냅숏 파일이 CAB 파일 형식으로 **@value** 압축 되는지 여부를 나타내기 위해에 **true** 또는 **false** 값을 지정 합니다.  
  
    -   **pre_snapshot_script** -초기 스냅숏을 **@value** 적용 하기 전에 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 파일 이름 및 전체 경로를 지정 합니다.  
  
    -   **post_snapshot_script** -또한 초기 **@value** 스냅숏을 적용 한 후 초기화 하는 동안 구독자에서 실행할 **.sql** 파일의 파일 이름 및 전체 경로를 지정 합니다.  
  
    -   **snapshot_in_defaultfolder** - 마찬가지로 스냅샷을 기본 위치 이외 위치에서만 사용할 수 있는지 여부를 나타내는 **true** 또는 **false** 값을 지정합니다.  
  
2.  명령 프롬프트에서 [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) 를 실행하거나 스냅샷 에이전트 작업을 시작하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 이 예제에서는 대체 스냅샷 폴더 및 압축 스냅샷을 사용하는 게시를 만듭니다.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>참고 항목  
 [대체 스냅숏 폴더 위치](../alternate-snapshot-folder-locations.md)   
 [압축 스냅숏](../compressed-snapshots.md)   
 [스냅샷 적용 전후에 스크립트 실행](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [FTP를 통해 스냅샷 전송](../transfer-snapshots-through-ftp.md)   
 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)  
  
  
