---
title: 스냅숏 없이 트랜잭션 구독 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, initializing
- replication [SQL Server], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 75c8c1f8-60bc-44a8-944b-d18d1f6bda11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0cef8a7e8a64935cca6b378e14c00eb0d80f6b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721146"
---
# <a name="initialize-a-transactional-subscription-without-a-snapshot"></a>스냅숏 없이 트랜잭션 구독 초기화
  기본적으로 트랜잭션 게시에 대한 구독은 스냅숏 에이전트가 생성하고 배포 에이전트가 적용하는 스냅숏으로 초기화됩니다. 큰 초기 데이터 세트를 다루는 시나리오와 같은 일부 시나리오에서는 다른 방법을 사용하여 구독을 초기화하는 것이 좋습니다. 구독자를 초기화하는 다른 방법은 다음과 같습니다.  
  
-   백업을 지정하고 이 백업을 구독자에서 복원하면 배포 에이전트가 필요한 복제 메타데이터와 시스템 프로시저를 복사합니다. 게시를 백업으로 초기화할 수 있도록 설정한 다음 생성된 백업 중 어떤 최근 백업이든 사용할 수 있으므로 백업으로 초기화는 방법은 데이터를 구독자에 배달하는 가장 빠르고도 편리한 방법입니다.  
  
-   데이터베이스 연결과 같이 다른 메커니즘을 통해 초기 데이터 세트를 구독자에게 복사합니다. 올바른 데이터와 스키마가 구독자에 있는지 확인한 다음 배포 에이전트가 필요한 메타데이터와 시스템 프로시저를 복사하는지 확인해야 합니다.  
  
## <a name="initializing-a-subscription-with-a-backup"></a>백업으로 구독 초기화  
 백업은 전체 데이터베이스를 포함하므로 각 구독 데이터베이스는 초기화될 때 게시 데이터베이스의 전체 복사본을 포함하게 됩니다.  
  
-   백업은 게시에 대한 아티클로 지정되지 않은 테이블을 포함합니다.  
  
-   테이블에 행 또는 열 필터가 지정되어 있어도 백업은 모든 데이터를 포함합니다.  
  
 백업이 복원된 후에 필요 없는 개체나 데이터를 제거하는 작업은 관리자나 애플리케이션이 수행해야 합니다. 후속 동기화에서는 데이터 변경 내용이 아티클로 지정된 테이블에 적용되고 지정된 필터링 조건을 만족하는 경우에만 복제됩니다.  
  
> [!NOTE]  
>  백업을 복원할 때 구독자가 자동으로 동기화하도록 하려면 백업을 게시자에서 가져와야 합니다. 백업에 있는 LSN(로그 시퀀스 번호) 값(동기화를 시작할 시점을 설정하는 데 사용됨)은 게시자에만 해당됩니다.  
  
 **백업으로 구독을 초기화하려면**  
  
 백업으로 구독을 초기화하려면 먼저 게시를 만들 때 해당 옵션을 설정한 다음 구독을 만들 때 여러 옵션에 대한 값을 지정해야 합니다. 새 게시 마법사를 사용하거나 프로그래밍 방식으로 게시를 설정할 수 있습니다. 그러나 구독 옵션에 필요한 값은 프로그래밍 방식으로만 지정할 수 있습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [트랜잭션 게시에 대한 백업으로 초기화 설정&#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   복제 Transact-SQL 프로그래밍: [백업에서 트랜잭션 구독 초기화&#40;복제 Transact-SQL 프로그래밍&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
> [!NOTE]  
>  스냅숏을 사용하지 않고 구독을 초기화할 경우 게시자에서 SQL Server 서비스를 실행하는 계정에는 배포자의 스냅숏 폴더에 대한 쓰기 권한이 있어야 합니다. 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](security/replication-agent-security-model.md)을 참조하십시오.  
  
### <a name="ensuring-the-suitability-of-a-backup"></a>백업의 적합성 확인  
 백업 이후에 발생하는 트랜잭션이 모두 배포자에 저장되는 경우 백업이 구독자를 초기화하는 데 적합합니다. 백업이 적합하지 않으면 복제에서 오류 메시지를 표시합니다.  
  
 백업이 사용하기에 적합하지 확인하려면 다음 지침을 따르십시오.  
  
-   사용할 수 있는 최신 백업을 사용하고 최신 백업이 최대 배포 보존 기간보다 오래된 경우 백업으로 구독을 초기화하기 전에 새 백업을 만듭니다. 보존 기간에 대한 자세한 내용은 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)를 참조하십시오.  
  
-   기본적으로 배포 정리 작업은 배포 데이터베이스에서 72시간 이상된 트랜잭션을 정리합니다. 정리는 게시에 대해 설정된 보존 기간을 기반으로 합니다. 오래된 백업으로 동기화할 때는 복원할 백업 전에 해당 작업을 임시로 비활성화한 다음 구독이 성공적으로 생성된 후 다시 활성화하십시오. 이렇게 하면 백업을 통해 성공적으로 동기화되어야 하는 배포 데이터베이스에서 트랜잭션이 제거되지 않습니다. 정리 작업을 실행하는 방법은 [복제 유지 관리 작업 실행&#40;SQL Server Management Studio&#41;](administration/run-replication-maintenance-jobs-sql-server-management-studio.md)을 참조하세요.  
  
 경우에 따라 백업으로 초기화된 구독을 설정한 후에 복원된 구독자 데이터베이스에서 사용자 지정 작업을 수동으로 수행해야 합니다. 일반적으로 구독자 데이터베이스 내용이 게시자 데이터베이스 내용과 달라지도록 게시가 정의된 경우 복원된 구독자 데이터베이스에서 수동으로 수정 작업을 수행해야 합니다.  
  
-   복원된 데이터베이스의 인덱싱된 뷰가 로그 기반 테이블 아티클의 인덱싱된 뷰로 게시된 경우 해당 뷰를 테이블로 변환해야 합니다.  
  
-   복원된 데이터베이스에서 구독한 타임스탬프 열을 **binary(8)** 열로 변환해야 합니다. 즉, 타임스탬프 열이 포함된 테이블의 내용을 타임스탬프 열 대신 **binary(8)** 열이 있다는 사실만 제외하면 스키마가 일치하는 새 테이블로 복사하고 원래 테이블을 삭제한 다음 새 테이블의 이름을 원래 테이블과 같은 이름으로 변경합니다.  
  
## <a name="initializing-a-subscription-with-an-alternative-method"></a>대체 방법으로 구독 초기화  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]와 같이 게시 데이터베이스 스키마와 데이터를 구독자에 복사할 수 있는 방법을 사용하여 구독을 초기화할 수 있습니다. 대체 방법을 사용하여 구독자를 초기화하면 복제 지원 개체가 구독자에 복사됩니다.  
  
 백업으로 초기화하는 것과 달리 구독을 추가할 때 데이터 및 스키마가 제대로 동기화되었는지를 확인해야 합니다. 예를 들어 데이터와 스키마가 구독자로 복사된 시점과 구독이 추가된 시점 중간에 게시자에서 작업이 수행되었으면 이러한 작업으로 인한 변경 내용이 구독자로 복제되지 않을 수 있습니다.  
  
 대체 방법으로 구독을 초기화하려면 [Initialize a Subscription Manually](initialize-a-subscription-manually.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [구독 초기화](initialize-a-subscription.md)  
  
  
