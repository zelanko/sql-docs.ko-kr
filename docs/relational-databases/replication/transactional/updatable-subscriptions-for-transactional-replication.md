---
title: 업데이트할 수 있는 구독(트랜잭션)
description: SQL Server에서 트랜잭션 복제에 사용할 수 있는 업데이트할 수 있는 구독 기능을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 07/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7baa131caa531038d8764c070ebd00ba44147c54
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321442"
---
# <a name="updatable-subscriptions---for-transactional-replication"></a>트랜잭션 복제를 위한 업데이트 가능 구독
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  이 기능은 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012부터 2016 버전에서 계속 지원됩니다. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 트랜잭션 복제에서는 업데이트할 수 있는 구독과 피어 투 피어 복제를 통해 구독자에서 업데이트를 수행할 수 있습니다. 업데이트할 수 있는 구독에는 다음 두 가지 유형이 있습니다.  
  
-   즉시 업데이트. 구독자에서 데이터를 업데이트하려면 게시자와 구독자를 연결해야 합니다.  
  
-   지연 업데이트. 구독자에서 데이터를 업데이트하기 위해 게시자와 구독자를 연결할 필요가 없습니다. 구독자나 게시자가 오프라인 상태일 때도 업데이트할 수 있습니다.  
  
 구독자에서 데이터를 업데이트하면 이 데이터는 먼저 게시자로 전파된 다음 다른 구독자로 전파됩니다. 즉시 업데이트를 사용하는 경우 변경 내용은 2단계 커밋 프로토콜을 사용하여 즉시 전파됩니다. 지연 업데이트를 사용하는 경우 변경 내용은 큐에 저장됩니다. 그런 다음 네트워크 연결이 가능할 때마다 지연 트랜잭션이 게시자에서 비동기적으로 적용됩니다. 업데이트한 내용은 게시자에 비동기식으로 전파되기 때문에 같은 데이터를 게시자나 다른 구독자가 업데이트할 수 있고 업데이트를 적용할 때 충돌이 발생할 수 있습니다. 게시를 만들 때 설정한 충돌 해결 정책에 따라 충돌을 감지하고 해결합니다.  
  
 새 게시 마법사에서 업데이트할 수 있는 구독이 있는 트랜잭션 게시를 만드는 경우 즉시 업데이트와 지연 업데이트를 모두 설정할 수 있습니다. 저장 프로시저가 있는 게시를 만드는 경우 이 두 가지 옵션 중 하나 또는 둘 다를 설정할 수 있습니다. 게시에 대한 구독을 만드는 경우에는 사용할 업데이트 모드를 지정합니다. 그런 다음 필요에 따라 업데이트 모드를 전환할 수 있습니다. 자세한 내용은 다음에 나올 "업데이트 모드 전환" 섹션을 참조하십시오.  
  
 트랜잭션 게시에 대해 업데이트할 수 있는 구독을 설정하려면 [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)을 참조하세요.  
  
 트랜잭션 게시에 대해 업데이트할 수 있는 구독을 만들려면 [트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)를 참조하세요. 
  
## <a name="switching-between-update-modes"></a>업데이트 모드 전환  
 업데이트할 수 있는 구독을 사용할 때는 구독에서 특정 업데이트 모드를 사용하도록 지정한 다음 애플리케이션의 필요에 따라 다른 업데이트 모드로 전환할 수 있습니다. 예를 들어 구독에서 즉시 업데이트를 사용하도록 지정한 다음 시스템 오류로 인해 네트워크 연결이 손실된 경우에 지연 업데이트로 전환할 수 있습니다.  
  
> [!NOTE]  
>  복제에서는 업데이트 모드가 자동으로 전환되지 않습니다. 모드를 전환하려면 SQL Server Management Studio를 통해 업데이트 모드를 설정하거나 애플리케이션에서 [sp_setreplfailovermode&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)를 호출해야 합니다.  
  
 즉시 업데이트에서 지연 업데이트로 전환하면 구독자와 게시자가 연결되고 큐 판독기 에이전트에서 큐의 보류 중인 모든 메시지를 게시자에 적용할 때까지는 즉시 업데이트로 다시 전환할 수 없습니다.  
  
 **업데이트 모드를 전환하려면**  
  
 업데이트 모드를 전환하려면 이 두 업데이트 모드에 대한 게시와 구독을 설정한 다음 필요에 따라 모드를 전환합니다. 자세한 내용은 다음을 참조하세요.  
[업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>업데이트할 수 있는 구독 사용 시 고려 사항  
  
-   구독 업데이트나 지연 업데이트 구독에 대해 게시를 설정한 다음에는 구독에서 게시를 사용할 필요가 없더라도 해당 옵션을 해제할 수 없습니다. 이 옵션을 해제하려면 해당 게시를 삭제하고 새 게시를 만들어야 합니다.  
  
-   데이터 재게시는 지원되지 않습니다.  
  
-   복제는 추적을 위해 **msrepl_tran_version** 열을 게시된 테이블에 추가합니다. 이 추가 열 때문에 모든 **INSERT** 문에 열 목록이 포함되어야 합니다.  
  
-   구독 업데이트를 지원하는 게시의 테이블에서 스키마를 변경하려면 게시자와 구독자에서 해당 테이블에 대한 모든 작업을 중단해야 하고 보류 중인 데이터 변경 내용이 스키마를 변경하기 전에 모든 노드로 전파되어야 합니다. 이렇게 하면 처리 중인 트랜잭션이 보류 중인 스키마 변경과 충돌하지 않습니다. 스키마 변경을 모든 노드로 전파하면 게시된 테이블에 대한 작업을 재개할 수 있습니다. 자세한 내용은 [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)를 참조하세요.  
  
-   업데이트 모드를 전환하려면 구독을 초기화한 후 큐 판독기 에이전트를 최소한 한 번은 실행해야 합니다. 큐 판독기 에이전트는 기본적으로 계속 실행됩니다.  
  
-   구독자 데이터베이스가 수평으로 분할되고 파티션에 구독자에는 존재하면서 게시자에는 없는 행이 있다면 구독자는 기존 행을 업데이트할 수 없습니다. 이러한 행을 업데이트하려고 하면 오류가 발생합니다. 테이블에서 이 행을 삭제한 다음 게시자에서 추가해야 합니다.  

-   고유하게 필터링된 인덱스를 사용하면 지연 업데이트 구독자로 인해 트랜잭션 복제 성능이 저하될 수 있습니다. 고유하게 필터링된 인덱스가 있는 아티클에 충돌이 발생한 경우 충돌을 해결하면 구독자에서 고유하게 필터링된 인덱스가 적용되지 않은 행에 대한 추가 삭제 및 삽입이 발생합니다.
  
### <a name="updates-at-the-subscriber"></a>구독자에서의 업데이트  
  
-   구독자에서의 업데이트는 구독이 만료되었거나 비활성화 상태에 있더라도 게시자로 전파됩니다. 이러한 구독은 삭제하거나 다시 초기화하십시오.  
  
-   **TIMESTAMP** 또는 **IDENTITY** 열을 사용하고 이러한 열이 자체 기본 데이터 형식으로 복제되는 경우에는 이러한 열의 값을 구독자에서 업데이트할 수 없습니다.  
  
-   복제에 대한 변경 내용 추적 트리거 내의 삽입 테이블 또는 삭제 테이블에서는 읽기 작업을 수행할 수 없으므로 구독자는 **text**, **ntext** 또는 **image** 값을 업데이트하거나 삽입할 수 없습니다. 마찬가지로 게시자가 데이터를 덮어쓰므로 구독자는 **WRITETEXT** 또는 **UPDATETEXT** 를 사용하여 **text** 또는 **image** 값을 업데이트하거나 삽입할 수 없습니다. 대신 **text** 및 **image** 열을 별개의 테이블에 분할할 수 있고 트랜잭션 내에서 두 테이블을 수정할 수 있습니다.  
  
     구독자에서 큰 개체를 업데이트하려면 **text**, **ntext**및 **image** 데이터 형식 대신 **varchar(max)** , **nvarchar(max)** 및 **varbinary(max)** 데이터 형식을 사용합니다.  
  
-   중복을 생성하는 고유 키(기본 키 포함)에 대한 업데이트(예: `UPDATE <column> SET <column> =<column>+1` 형식의 업데이트)는 허용되지 않으며 고유성 위반 때문에 거부됩니다. 이는 구독자에서의 업데이트 설정이 영향을 받는 각 행에 대한 개별 **UPDATE** 문으로 복제에 의해 전파되기 때문입니다.  
  
-   구독자 데이터베이스가 수평으로 분할되고 파티션에 구독자에는 존재하면서 게시자에는 없는 행이 있다면 구독자는 기존 행을 업데이트할 수 없습니다. 이러한 행을 업데이트하려고 하면 오류가 발생합니다. 테이블에서 이 행을 삭제하고 다시 삽입해야 합니다.  
  
### <a name="user-defined-triggers"></a>사용자 정의 트리거  
  
-   애플리케이션이 구독자에 대한 트리거를 요구하는 경우에는 게시자와 구독자에서 `NOT FOR REPLICATION` 옵션을 사용하여 트리거를 정의해야 합니다. 이렇게 하면 원래 데이터가 변경될 때만 트리거가 발생되고 변경 내용이 복제될 때는 트리거가 발생되지 않습니다.  
  
     복제 트리거에 의해 테이블이 업데이트될 때 사용자 정의 트리거가 발생되지 않도록 합니다. 이는 사용자 정의 트리거 본문에서 **sp_check_for_sync_trigger** 프로시저를 호출하여 수행할 수 있습니다. 자세한 내용은 [sp_check_for_sync_trigger&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql.md)를 참조하세요.  
  
### <a name="immediate-updating"></a>즉시 업데이트  
  
-   즉시 업데이트 구독의 경우에 구독자에서의 변경 내용은 게시자로 전파되고 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 적용됩니다. 게시자와 구독자에 MS DTC가 설치되고 구성되어 있는지 확인하십시오. 자세한 내용은 Windows 설명서를 참조하십시오.  
  
-   변경 내용을 복제하려면 즉시 업데이트 구독에 사용되는 트리거를 게시자에 연결해야 합니다.  
  
-   게시에서 즉시 업데이트 구독을 허용하고 게시의 아티클에 열 필터가 있는 경우에는 기본값이 없고 Null을 허용하지 않는 열을 필터를 사용하여 제외할 수 없습니다.  
  
### <a name="queued-updating"></a>지연 업데이트  
  
-   병합 게시에 포함된 테이블도 지연 업데이트 구독을 허용하는 트랜잭션 게시의 일부로 게시할 수 없습니다.  
  
-   지연 업데이트를 사용할 경우에는 기본 키가 모든 쿼리에 대해 레코드 로케이터로 사용되기 때문에 기본 키 열에 대해 업데이트를 하지 않는 것이 좋습니다. 충돌 해결 정책이 구독자 내용을 적용하도록 설정된 경우 기본 키는 주의해서 업데이트해야 합니다. 게시자 및 구독자 모두에서 기본 키를 업데이트하면 그 결과로 다른 기본 키를 가진 두 개의 행이 생성됩니다.  
  
-   데이터 형식이 **SQL_VARIANT**인 열의 경우: 데이터를 구독자에서 삽입하거나 업데이트하면 해당 데이터가 구독자에서 큐로 복사될 때 큐 판독기 에이전트에 의해 다음과 같은 방식으로 매핑됩니다.  
  
    -   **BIGINT**, **DECIMAL**, **NUMERIC**, **MONEY**및 **SMALLMONEY** 는 **NUMERIC**으로 매핑됩니다.  
  
    -   **BINARY** 및 **VARBINARY** 는 **VARBINARY** 데이터로 매핑됩니다.  
  
### <a name="conflict-detection-and-resolution"></a>충돌 감지 및 해결  
  
-   "구독자 내용 적용" 충돌 정책을 사용하는 경우: 기본 키 열에 대한 업데이트에 대해서는 충돌 해결이 지원되지 않습니다.  
  
-   FOREIGN KEY 제약 조건 오류로 인한 충돌은 복제로 해결되지 않습니다.  
  
    -   충돌이 예상되지 않고 데이터가 제대로 분할된 경우(구독자가 같은 행을 업데이트하지 않음)에는 게시자와 구독자에서 FOREIGN KEY 제약 조건을 사용할 수 있습니다.  
  
    -   충돌이 예상되는 경우에는 "구독자 내용 적용" 충돌 해결 사용 시 게시자나 구독자에서 외래 키 제약 조건을 사용해서는 안 되며 "게시자 내용 적용" 충돌 해결 사용 시 구독자에서 외래 키 제약 조건을 사용해서는 안 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [트랜잭션 복제](../../../relational-databases/replication/transactional/transactional-replication.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
