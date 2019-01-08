---
title: Create an Updatable Subscription to a Transactional Publication (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updateable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1fd84d8be6fc99a29ade2ee258b45e5b080d9bd9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749366"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-management-studio"></a>트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio)

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
**새 구독 마법사**의 **업데이트할 수 있는 구독** 페이지에서 업데이트할 수 있는 구독을 구성할 수 있습니다. 이 페이지는 업데이트할 수 있는 구독에 대해 트랜잭션 게시를 설정한 경우에만 사용할 수 있습니다. 업데이트할 수 있는 구독을 사용하도록 설정하는 방법에 대한 자세한 내용은 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](enable-updating-subscriptions-for-transactional-publications.md)을 참조하세요.   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>게시자에서 업데이트할 수 있는 구독을 구성하려면  

1. Microsoft SQL Server Management Studio에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.

2. **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.

3. 구독 업데이트에 대해 설정된 트랜잭션 게시를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.

4. 마법사의 페이지에 따라 배포 에이전트의 실행 위치 같은 구독 옵션을 지정합니다.

5. **새 구독 마법사**의 **업데이트할 수 있는 구독** 페이지에서 **복제**가 선택되었는지 확인합니다.

6. **게시자에서 커밋** 드롭다운 목록에서 옵션을 선택합니다.

    * 즉시 업데이트 구독을 사용하려면 **동시에 변경 내용 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 지연 업데이트 구독을 허용하면(새 게시 마법사로 만든 게시의 기본 설정) 구독 속성 **update_mode**가 **failover**로 설정됩니다. 이 모드에서는 필요하면 나중에 지연 업데이트로 전환할 수 있습니다.

    * 지연 업데이트 구독을 사용하려면 **변경 내용 대기 및 가능 시 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 즉시 업데이트 구독을 허용하며(새 게시 마법사로 만든 게시의 기본 설정) 구독자에서 SQL Server 2005 이상 버전이 실행될 경우 구독 속성 **update_mode**가 queued failover로 설정됩니다. 이 모드에서는 나중에 필요에 맞게 즉시 업데이트로 전환할 수 있습니다.

    업데이트 모드를 전환하는 방법에 대한 자세한 내용은 [업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)을 참조하세요.

7. 즉시 업데이트를 사용하거나 **update_mode**가 **queued failover**로 설정된 구독에 대해 **업데이트할 수 있는 구독에 대한 로그인** 페이지가 표시됩니다. **업데이트할 수 있는 구독에 대한 로그인** 페이지에서 즉시 업데이트 구독을 위해 게시자로의 연결이 설정된 연결된 서버를 지정합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 다음 옵션 중 하나를 선택합니다.

    * **다음 SQL Server 인증을 사용하여 연결되는 연결된 서버 만들기.** 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.

    * **이미 정의한 연결된 서버나 원격 서버 사용** [sp_addserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), SQL Server Management Studio 또는 다른 메서드를 사용하여 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의한 경우 이 옵션을 선택합니다.

    연결된 서버 계정에 필요한 사용 권한에 대한 자세한 내용은 [여기에 링크 설명 입력](../security/secure-the-subscriber.md)의 **지연 업데이트 구독**을 참조하세요.

8. 마법사를 완료합니다.

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>구독자에서 업데이트할 수 있는 구독을 구성하려면


1. SQL Server Management Studio에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.

2. **복제** 폴더를 확장합니다.

3. **로컬 구독** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.

4. **새 구독 마법사**의 **게시** 페이지에 있는 **게시자** 드롭다운 목록에서 **SQL Server 게시자 찾기**를 선택합니다.

5. **서버에 연결** 대화 상자에서 게시자에 연결합니다.

6. **게시** 페이지에서 구독 업데이트에 대해 설정된 트랜잭션 게시를 선택합니다.

7. 마법사의 페이지에 따라 배포 에이전트의 실행 위치 같은 구독 옵션을 지정합니다.

8. 새 구독 마법사의 **업데이트할 수 있는 구독** 페이지에서 **복제**가 선택되었는지 확인합니다.

9. **게시자에서 커밋** 드롭다운 목록에서 옵션을 선택합니다.

    * 즉시 업데이트 구독을 사용하려면 **동시에 변경 내용 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 지연 업데이트 구독을 허용하면(새 게시 마법사로 만든 게시의 기본 설정) 구독 속성 **update_mode**가 **failover**로 설정됩니다. 이 모드에서는 필요하면 나중에 지연 업데이트로 전환할 수 있습니다.

    * 지연 업데이트 구독을 사용하려면 **변경 내용 대기 및 가능 시 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 즉시 업데이트 구독을 허용하며(새 게시 마법사로 만든 게시의 기본 설정) 구독자에서 SQL Server 2005 이상 버전이 실행될 경우 구독 속성 **update_mode**가 queued **failover**로 설정됩니다. 이 모드에서는 나중에 필요에 맞게 즉시 업데이트로 전환할 수 있습니다.

    업데이트 모드를 전환하는 방법에 대한 자세한 내용은 [업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)을 참조하세요.

10. 즉시 업데이트를 사용하거나 **update_mode**가 **queued failover**로 설정된 구독에 대해 **업데이트할 수 있는 구독에 대한 로그인** 페이지가 표시됩니다. **업데이트할 수 있는 구독에 대한 로그인** 페이지에서 즉시 업데이트 구독을 위해 게시자로의 연결이 설정된 연결된 서버를 지정합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 다음 옵션 중 하나를 선택합니다.

    * **다음 SQL Server 인증을 사용하여 연결되는 연결된 서버 만들기.** 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.

    * **이미 정의한 연결된 서버나 원격 서버 사용** [sp_addserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), SQL Server Management Studio 또는 다른 메서드를 사용하여 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의한 경우 이 옵션을 선택합니다.

    연결된 서버 계정에 필요한 사용 권한에 대한 자세한 내용은 [여기에 링크 설명 입력](../security/secure-the-subscriber.md)의 **지연 업데이트 구독**을 참조하세요.

11. 마법사를 완료합니다.

## <a name="see-also"></a>관련 항목:

[Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](create-a-publication.md)

[Transact-SQL을 사용하여 트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](../create-updatable-subscription-transactional-publication-transact-sql.md) 
 
  
