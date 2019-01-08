---
title: 구독 만료 및 비활성화 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89818f172ee9af09a44654dffc800bf6adc35de4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804335"
---
# <a name="subscription-expiration-and-deactivation"></a>구독 만료 및 비활성화
  지정된 *보존 기간*내에 동기화되지 않는 구독을 비활성화하거나 만료할 수 있습니다. 동작은 복제 유형 및 초과한 보존 기간에 따라 달라집니다.  
  
 보존 기간을 설정하려면 [구독에 대한 만료 기간 설정](publish/set-the-expiration-period-for-subscriptions.md), [Set the Distribution Retention Period for Transactional Publications &#40;SQL Server Management Studio&#41;](set-distribution-retention-period-for-transactional-publications.md)(트랜잭션 게시에 대한 배포 보존 기간 설정&#40;SQL Server Management Studio&#41;) 및 [게시 및 배포 구성](configure-publishing-and-distribution.md)을 참조하세요.  
  
## <a name="transactional-replication"></a>트랜잭션 복제  
 트랜잭션 복제는 최대 배포 보존 기간([sp_adddistributiondb&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)의 **@max_distretention** 매개 변수)과 게시 보존 기간([sp_addpublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)의 **@retention** 매개 변수)을 사용합니다.  
  
-   구독이 최대 배포 보존 기간(기본값: 72시간) 내에 동기화되지 않고 구독자에게 배달되지 않은 변경 내용이 배포 데이터베이스에 있는 경우 해당 구독은 배포자에서 실행되는 **배포 정리** 작업에 의해 비활성화된 상태로 표시됩니다. 구독을 다시 초기화해야 합니다.  
  
-   구독이 게시 보존 기간(기본값: 336시간) 내에 동기화되지 않는 경우 해당 구독은 만료되어 게시자에서 실행되는 **만료된 구독 정리** 작업에 의해 삭제됩니다. 구독을 다시 만들어 동기화해야 합니다.  
  
     밀어넣기 구독이 만료되면 완전히 제거되지만 끌어오기 구독은 그렇지 않습니다. 끌어오기 구독은 구독자에서 정리해야 합니다. 자세한 내용은 [Delete a Pull Subscription](delete-a-pull-subscription.md)을(를) 참조하세요.  
  
## <a name="merge-replication"></a>병합 복제  
 병합 복제는 게시 보존 기간([sp_addmergepublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)의 **@retention** 및 **@retention_period_unit** 매개 변수)을 사용합니다. 구독이 만료되면 구독에 대한 메타데이터가 제거되므로 구독을 다시 초기화해야 합니다. 다시 초기화되지 않은 구독은 게시자에서 실행되는 **만료된 구독 정리** 작업에 의해 삭제됩니다. 기본적으로 이 작업은 매일 실행됩니다. 이 작업을 통해 게시 보존 기간의 2배에 해당하는 기간 동안 동기화되지 않은 모든 밀어넣기 구독이 제거됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
-   게시의 보존 기간이 14일이면 14일 이내에 동기화되지 않은 구독은 만료될 수 있습니다.  
  
     게시자에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전이 실행되고 있으며 구독의 에이전트를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 가져온 경우 해당 구독의 파티션에 있는 데이터가 변경된 경우에만 구독이 만료됩니다. 예를 들어 구독자가 독일에 거주하는 고객에 대해서만 고객 데이터를 받는다고 가정합니다. 보존 기간을 14일로 설정한 경우 마지막 14일 내에 독일 거주 고객의 데이터가 변경된 경우에만 14일 후에 구독이 만료됩니다.  
  
-   마지막 동기화가 수행되고 14일부터 27일 내에 구독을 다시 초기화할 수 있습니다.  
  
-   마지막 동기화가 수행되고 28일이 경과되면 **만료된 구독 정리** 작업에 의해 구독이 삭제됩니다. 밀어넣기 구독이 만료되면 완전히 제거되지만 끌어오기 구독은 그렇지 않습니다. 끌어오기 구독은 구독자에서 정리해야 합니다. 자세한 내용은 [Delete a Pull Subscription](delete-a-pull-subscription.md)을(를) 참조하세요.  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>병합 게시에 대한 게시 보존 기간 설정 시 고려 사항  
 병합 게시의 보존 기간을 설정할 때 다음 사항을 고려하십시오.  
  
-   병합 게시의 보존 기간은 다양한 표준 시간대의 구독자를 수용하기 위해 24시간의 유예 기간을 갖습니다. 예를 들어 보존 기간을 하루로 설정한 경우 실제 보존 기간은 48시간이 됩니다.  
  
-   병합 복제 메타데이터의 정리는 다음과 같이 게시 보존 기간에 따라 달라집니다.  
  
    -   보존 기간에 도달하기 전까지는 복제 작업을 통해 게시 및 구독 데이터베이스의 메타데이터를 정리할 수 없습니다. 보존 기간을 너무 길게 설정하면 복제 성능이 저하될 수 있으므로 주의해야 합니다. 보존 기간 내에 모든 구독자가 정기적으로 동기화될 가능성이 있으면 보존 기간을 낮은 값으로 설정하는 것이 좋습니다.  
  
    -   **@retention**에 값 0을 지정하여 구독이 만료되지 않도록 지정할 수 있지만 이 경우 메타데이터를 정리할 수 없으므로 이 값은 사용하지 않도록 합니다.  
  
-   재게시자의 보존 기간은 원래 게시자에 설정한 보존 기간과 동일하거나 더 낮은 값으로 설정해야 합니다. 또한 모든 게시자와 대체 동기화 파트너에 대해 동일한 게시 보존 값을 사용해야 합니다. 다른 보존 값을 사용하면 데이터가 일치하지 않을 수 있습니다. 게시 보존 값을 변경해야 하는 경우 데이터 일치성을 유지하도록 구독자를 다시 초기화합니다.  
  
-   정리 후에 게시 보존 기간이 늘어나고 구독이 메타데이터가 이미 삭제된 게시자와 병합하려고 하면 늘어난 보존 기간으로 인해 구독은 만료되지 않습니다. 그러나 게시자에는 구독자에 대한 변경 내용을 다운로드할 만큼의 충분한 메타데이터가 없으므로 데이터가 제대로 일치되지 못할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독 다시 초기화](reinitialize-subscriptions.md)   
 [복제 에이전트 관리](agents/replication-agent-administration.md)   
 [게시 구독](subscribe-to-publications.md)  
  
  
