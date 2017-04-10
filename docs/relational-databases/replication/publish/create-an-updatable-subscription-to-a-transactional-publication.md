---
title: "트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "업데이트 가능한 트랜잭션 구독"
  - "업데이트 가능한 트랜잭션 구독 SSMS"
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# 트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio)

> [!NOTE]  
>  이 기능은 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012부터 2016 버전에서 계속 지원됩니다.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
업데이트할 수 있는 구독을 구성 된 **업데이트할 수 있는 구독** 의 페이지는 **새 구독 마법사**합니다. 이 페이지는 업데이트할 수 있는 구독에 대해 트랜잭션 게시를 설정한 경우에만 사용할 수 있습니다. 업데이트할 수 있는 구독을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [트랜잭션 게시에 대 한 업데이트 구독을 사용 하도록 설정](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)합니다.   
  
## 게시자에서 업데이트할 수 있는 구독을 구성하려면  

1. Microsoft SQL Server Management Studio에서 게시자에 연결 하 고 해당 서버 노드를 확장 한 다음 키를 누릅니다.

2. **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.

3. 구독을 업데이트에 대해 설정 된 트랜잭션 게시를 마우스 오른쪽 단추로 누른 **새 구독**합니다.

4. 마법사의 페이지에 따라 배포 에이전트의 실행 위치 같은 구독 옵션을 지정합니다.

5. 에 **업데이트할 수 있는 구독** 의 페이지는 **새 구독 마법사**, 확인 **복제** 을 선택 합니다.

6. 옵션을 선택 된 **게시자에서 커밋** 드롭 다운 목록:

    * 즉시 업데이트 구독을 사용 하려면 선택 **동시에 변경 내용 커밋**합니다. 이 옵션을 선택 하 고 게시 (새 게시 마법사를 사용 하 여 만든 게시에 대 한 기본값) 이면 지연된 업데이트 구독을 허용 하는 경우 구독 속성 **update_mode** 로 설정 된 **장애 조치**합니다. 이 모드에서는 필요하면 나중에 지연 업데이트로 전환할 수 있습니다.

    * 지연된 업데이트 구독을 사용 하려면 선택 **변경 내용 대기 및 가능 시 커밋**합니다. 이 옵션을 선택 하 고 게시 허용 즉시 업데이트 구독 (새 게시 마법사를 사용 하 여 만든 게시에 대 한 기본값), SQL Server 2005 또는 이후 버전을 구독 속성 구독자에서 실행 중인 경우 **update_mode** 지연된 장애 조치로 설정 됩니다. 이 모드에서는 나중에 필요에 맞게 즉시 업데이트로 전환할 수 있습니다.

    업데이트 모드를 전환 하는 방법에 대 한 정보를 참조 하십시오. [모드 사이 전환 업데이트 가능한 트랜잭션 구독에 대 한](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)합니다.

7. **업데이트할 수 있는 구독에 대 한 로그인** 즉시 업데이트를 사용 하는 구독에 대 한 페이지는 **update_mode** 로 설정 **장애 조치 대기**합니다. 에 **업데이트할 수 있는 구독에 대 한 로그인** 페이지는 게시자에 연결 된 즉시 업데이트 구독에 연결된 된 서버를 지정 합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 다음 옵션 중 하나를 선택합니다.

    * **SQL Server 인증을 사용 하 여 연결 하는 연결된 된 서버를 만듭니다.** 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.

    * **이미 정의한 연결된 서버나 원격 서버 사용** 원격 서버 또는 사용 하 여 게시자와 구독자 간의 연결 된 서버를 정의 하는 경우이 옵션을 선택 합니다, [sp_addserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio 나 다른 방법입니다.

    연결 된 서버 계정에 필요한 사용 권한에 대 한 정보를 참조 하십시오.는 **지연 업데이트 구독이** 의 [링크 여기에 설명을 입력](../../../relational-databases/replication/security/secure-the-subscriber.md)합니다.

8. 마법사를 완료합니다.

## 구독자에서 업데이트할 수 있는 구독을 구성하려면


1. SQL Server Management Studio에서 구독자에 연결 하 고 해당 서버 노드를 확장 한 다음 키를 누릅니다.

2. **복제** 폴더를 확장합니다.

3. 마우스 오른쪽 단추로 클릭는 **로컬 구독** 폴더를 마우스 클릭 한 다음 **새 구독**합니다.

4. 에 **게시** 의 페이지는 **새 구독 마법사**, 선택, **SQL Server 게시자 찾기** 에서 **게시자** 드롭 다운 목록입니다.

5. **서버에 연결** 대화 상자에서 게시자에 연결합니다.

6. 구독 업데이트에 대해 설정 된 트랜잭션 게시를 선택 된 **게시** 페이지입니다.

7. 마법사의 페이지에 따라 배포 에이전트의 실행 위치 같은 구독 옵션을 지정합니다.

8. 에 **업데이트할 수 있는 구독** 페이지는 새 구독 마법사의 확인 **복제** 을 선택 합니다.

9. 옵션을 선택 된 **게시자에서 커밋** 드롭 다운 목록:

    * 즉시 업데이트 구독을 사용 하려면 선택 **동시에 변경 내용 커밋**합니다. 이 옵션을 선택 하 고 게시 (새 게시 마법사를 사용 하 여 만든 게시에 대 한 기본값) 이면 지연된 업데이트 구독을 허용 하는 경우 구독 속성 **update_mode** 로 설정 된 **장애 조치**합니다. 이 모드에서는 필요하면 나중에 지연 업데이트로 전환할 수 있습니다.

    * 지연된 업데이트 구독을 사용 하려면 선택 **변경 내용 대기 및 가능 시 커밋**합니다. 이 옵션을 선택 하 고 게시 허용 즉시 업데이트 구독 (새 게시 마법사를 사용 하 여 만든 게시에 대 한 기본값), SQL Server 2005 또는 이후 버전을 구독 속성 구독자에서 실행 중인 경우 **update_mode** 에 대기 중인 설정 된 **장애 조치**합니다. 이 모드에서는 나중에 필요에 맞게 즉시 업데이트로 전환할 수 있습니다.

    업데이트 모드를 전환 하는 방법에 대 한 정보를 참조 하십시오. [모드 사이 전환 업데이트 가능한 트랜잭션 구독에 대 한](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)합니다.

10. **업데이트할 수 있는 구독에 대 한 로그인** 즉시 업데이트를 사용 하는 구독에 대 한 페이지는 **update_mode** 에 대기 중인 설정 **장애 조치**합니다. 에 **업데이트할 수 있는 구독에 대 한 로그인** 페이지는 게시자에 연결 된 즉시 업데이트 구독에 연결된 된 서버를 지정 합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 다음 옵션 중 하나를 선택합니다.

    * **SQL Server 인증을 사용 하 여 연결 하는 연결된 된 서버를 만듭니다.** 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.

    * **이미 정의한 연결된 서버나 원격 서버 사용** 원격 서버 또는 사용 하 여 게시자와 구독자 간의 연결 된 서버를 정의 하는 경우이 옵션을 선택 합니다, [sp_addserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio 나 다른 방법입니다.

    연결 된 서버 계정에 필요한 사용 권한에 대 한 정보를 참조 하십시오.는 **지연 업데이트 구독이** 의 [링크 여기에 설명을 입력](../../../relational-databases/replication/security/secure-the-subscriber.md)합니다.

11. 마법사를 완료합니다.

## 관련 항목:

[트랜잭션 복제를 위한 업데이트 가능 구독](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md)

[Transact-SQL을 사용하여 트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 
