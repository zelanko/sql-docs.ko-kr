---
title: 매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏 | Microsoft 문서
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 621966b18de4f7b1d8e48c755b9c52edfa5afe77
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052051"
---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏
  병합 게시에서 매개 변수가 있는 행 필터를 사용하면 복제 시 각 구독이 두 부분으로 구성된 스냅숏으로 초기화됩니다. 먼저 복제에 필요한 모든 개체와 게시된 개체의 스키마를 포함하는 스키마 스냅숏이 생성되는데 이때 데이터는 제외됩니다. 그런 다음 스키마 스냅숏의 개체 및 스키마와 구독의 파티션에 속한 데이터를 포함하는 스냅숏으로 각 구독을 초기화합니다. 둘 이상의 구독이 주어진 파티션(동일한 스키마와 데이터)을 받는다면 해당 파티션에 대한 스냅숏은 단 한 번만 생성됩니다. 동일한 스냅숏에서 여러 개의 구독이 초기화됩니다. 매개 변수가 있는 행 필터에 대한 자세한 내용은 [매개 변수가 있는 행 필터](merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
 다음 3가지 방법 중 하나로 매개 변수가 있는 필터를 사용하여 게시에 대한 스냅숏을 만들 수 있습니다.  
  
-   각 파티션에 대한 스냅숏을 미리 생성합니다. 이 옵션을 사용하여 스냅숏이 생성되는 시기를 제어할 수 있습니다.  
  
     일정에 따라 스냅숏을 새로 고칠 수 있도록 선택할 수도 있습니다. 스냅숏이 생성된 파티션을 구독하는 새 구독자는 최신 스냅숏을 받게 됩니다.  
  
-   구독자가 처음 동기화될 때 스냅숏 생성 및 적용을 요청하도록 허용합니다. 이 옵션을 사용하여 새 구독자는 관리자 간섭을 요청할 필요 없이 동기화할 수 있습니다. 스냅숏을 생성하기 위해서는[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 게시자에서 실행되고 있어야 합니다.  
  
    > [!NOTE]  
    >  게시에 있는 여러 아티클에 대한 필터링 시 각 구독에 고유하면서도 겹치지 않는 파티션이 생성될 경우 메타데이터는 병합 에이전트가 실행될 때마다 정리됩니다. 따라서 분할된 스냅숏은 더 빨리 만료됩니다. 이 옵션을 사용할 경우 구독자가 스냅숏 생성 및 배달을 시작하도록 허용하는 것을 고려해야 합니다. 필터링 옵션에 대한 자세한 내용은 [매개 변수가 있는 행 필터](merge/parameterized-filters-parameterized-row-filters.md)을 참조하십시오.  
  
-   스냅숏 에이전트를 사용하여 각 구독자에 대한 스냅숏을 수동으로 생성합니다. 그런 다음 구독자에서 병합 에이전트에 스냅숏 위치를 제공하여 병합 에이전트가 올바른 스냅숏을 검색하고 적용할 수 있도록 해야 합니다.  
  
    > [!NOTE]  
    >  이 옵션은 이전 버전과의 호환성을 위해 제공되며 FTP 스냅숏 공유를 허용하지 않습니다.  
  
 가장 융통성이 높은 방법은 미리 생성된 스냅숏 옵션과 구독자가 요청한 스냅숏 옵션을 조합하여 사용하는 것입니다. 스냅숏을 미리 생성한 다음 일정에 따라 새로 고치지만(보통 사용량이 적은 시간에 새로 고침) 새 파티션이 필요한 구독이 생성되면 구독자는 자신의 스냅숏을 생성할 수 있습니다.  
  
 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]라는 회사에 재고를 각 상점으로 배달하는 이동 가능 인력이 있다고 가정합니다. 각 영업 사원은 로그인할 때만 구독을 접수하며 자신이 담당하는 상점에 대한 데이터를 검색합니다. 관리자는 스냅숏을 미리 생성하고 일요일마다 새로 고치도록 선택합니다. 새 사용자가 시스템에 추가되고 현재 사용 가능한 스냅숏이 없는 파티션에 대한 데이터를 요구하는 경우도 가끔 있습니다. 관리자는 스냅숏을 사용할 수 없어서 구독자가 게시를 구독하지 못하는 상황을 피하기 위해 구독자에 의해 시작되는 스냅숏을 허용하도록 선택합니다. 새 구독자가 처음으로 연결할 때 지정된 파티션에 대한 스냅숏이 생성되고 구독자에서 적용됩니다. 스냅숏을 생성하기 위해서는[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 게시자에서 실행되고 있어야 합니다.  
  
 매개 변수가 있는 필터로 게시에 대한 스냅숏을 만들려면 [매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)를 참조하십시오.  
  
## <a name="security-settings-for-the-snapshot-agent"></a>스냅숏 에이전트에 대한 보안 설정  
 스냅숏 에이전트는 각 파티션에 대해 스냅숏을 만듭니다. 미리 생성된 스냅숏과 구독자가 요청한 스냅숏에 대해 게시에 대한 스냅숏 에이전트 작업을 새 게시 마법사 또는 **sp_addpublication_snapshot**을 통해 만들 때 지정한 자격 증명으로 스냅숏 에이전트를 실행 및 연결합니다. 자격 증명을 변경하려면 **sp_changedynamicsnapshot_job**을 사용합니다. 자세한 내용은 [sp_changedynamicsnapshot_job&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [스냅숏으로 구독 초기화](initialize-a-subscription-with-a-snapshot.md)   
 [매개 변수가 있는 행 필터](merge/parameterized-filters-parameterized-row-filters.md)   
 [스냅숏 폴더 보안 설정](security/secure-the-snapshot-folder.md)  
  
  
