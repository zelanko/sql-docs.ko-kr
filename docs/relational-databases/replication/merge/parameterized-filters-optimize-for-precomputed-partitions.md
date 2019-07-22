---
title: 사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication], about precomputed partitions
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9d4c2062662e07e35366d5bdccbf544d893568ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018692"
---
# <a name="parameterized-filters---optimize-for-precomputed-partitions"></a>매개 변수가 있는 필터 - 사전 계산된 파티션에 최적화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사전 계산 파티션을 필터링된 병합 게시에 사용하여 성능을 최적화할 수 있습니다. 또한 사전 계산 파티션은 필터링된 게시에서 논리 레코드를 사용하기 위한 요구 사항입니다. 논리적 레코드에 대한 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
 구독자가 게시자와 동기화되면 게시자는 구독자의 필터를 평가하여 그 구독자의 파티션이나 데이터 집합에 속하는 행을 확인해야 합니다. 게시자에서 필터링된 데이터 세트를 수신하는 각 구독자에 대한 변경 내용의 파티션 멤버 자격을 결정하는 이 과정을 *파티션 평가*라고 합니다. 사전 계산 파티션을 사용하지 않을 경우 특정 구독자에 대해 병합 에이전트를 마지막으로 실행한 이후에 게시자에서 필터링된 열의 각 변경 내용에 대해 파티션 평가를 수행해야 합니다. 게시자와 동기화하는 모든 구독자에 대해 이 프로세스를 반복합니다.  
  
 그러나 게시자와 구독자가 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 실행 중이고 사전 계산 파티션을 사용할 경우에는 변경이 발생할 때 게시자의 모든 변경 내용에 대한 파티션 멤버 자격이 사전 계산되고 지속됩니다. 결과적으로 구독자가 게시자와 동기화할 때 파티션 평가 과정을 거치지 않고도 파티션과 관련된 변경 내용을 즉시 다운로드할 수 있습니다. 이 기능을 통해 게시에 변경 내용, 구독자 또는 아티클이 많을 경우 성능이 크게 향상될 수 있습니다.  
  
 사전 계산 파티션을 사용하는 것 외에도 스냅샷을 미리 생성하거나 구독자가 처음 동기화될 때 스냅샷의 생성과 적용을 요청하도록 합니다. 이러한 옵션 중 하나 또는 둘 모두를 사용하여 매개 변수가 있는 필터를 사용하는 게시에 대한 스냅샷을 제공할 수 있습니다. 이러한 옵션을 하나도 지정하지 않으면 **bcp** 유틸리티를 사용하지 않고 일련의 SELECT 및 INSERT 문을 사용하여 구독을 초기화하게 되는데 이 경우 프로세스의 속도가 훨씬 느립니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
 **사전 계산 파티션을 사용하려면**  
  
 위에서 설명한 지침을 따르는 새 게시와 기존 게시의 경우 사전 계산 파티션이 기본적으로 설정됩니다. 설정은 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 를 통해 또는 프로그래밍 방식으로 변경할 수 있습니다. 자세한 내용은 [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)을 참조하세요.  
  
## <a name="requirements-for-using-precomputed-partitions"></a>사전 계산 파티션을 사용하기 위한 요구 사항  
 아래의 요구 사항이 만족되면 새 병합 게시는 기본적으로 사전 계산 파티션이 설정된 상태로 생성되고 기존 게시는 사전 계산 파티션을 사용하도록 자동으로 업그레이드됩니다. 게시가 요구 사항을 만족하지 않으면 게시를 변경한 다음 사전 계산 파티션을 설정할 수 있습니다. 아티클의 일부는 이러한 요구 사항을 만족하고 일부는 만족하지 않을 경우 두 개의 게시를 만들어 보십시오. 그 중 하나는 사전 계산 파티션을 설정합니다.  
  
### <a name="requirements-for-filter-clauses"></a>필터 절 요구 사항  
  
-   HOST_NAME() 및 SUSER_SNAME()과 같이 매개 변수가 있는 행 필터에 사용된 함수는 매개 변수가 있는 필터 절에 직접 표시되어야 하며 뷰 또는 동적 함수 내에서 중첩되지 않아야 합니다. 이러한 함수에 대한 자세한 내용은 [HOST_NAME&#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md), [SUSER_SNAME&#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) 및 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하세요.  
  
-   파티션이 생성된 후에는 각 구독자로 반환된 값을 변경하지 마십시오. 예를 들어 필터에 HOST_NAME()을 사용하고 HOST_NAME() 값을 무시하지 않을 경우 구독자에서 컴퓨터 이름을 변경하지 마십시오.  
  
-   조인 필터에는 HOST_NAME() 및 SUSER_SNAME() 함수와 같이 동기화 중인 구독자에 따라 다른 값으로 평가되는 동적 함수가 포함되지 않아야 합니다. 동적 함수는 매개 변수가 있는 행 필터만 포함할 수 있습니다.  
  
-   필터 절에는 비결정적 함수를 사용할 수 없습니다. 비결정적 함수에 대한 자세한 내용은 [Deterministic and Nondeterministic Functions](../../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하십시오.  
  
-   조인 필터 절이나 매개 변수가 있는 필터 절에서 참조하는 뷰에는 동적 함수가 포함되지 않아야 합니다.  
  
-   게시에 순환 조인 필터 관계가 없어야 합니다.  
  
### <a name="database-collation"></a>데이터베이스 정렬  
  
-   사전 계산 파티션을 사용할 경우 비교 시 테이블 또는 열의 데이터 정렬이 아닌 데이터베이스의 데이터 정렬을 항상 사용합니다. 다음과 같은 시나리오를 고려해 보세요.  
  
    -   데이터 정렬이 대/소문자를 구분하는 데이터베이스에 대/소문자를 구분하지 않는 테이블이 들어 있습니다.  
  
    -   매개 변수가 있는 필터에 있는 구독자의 호스트 이름과 비교할 **ComputerName**열이 테이블에 들어 있습니다.  
  
    -   테이블에 값이 "MYCOMPUTER"인 행과 "mycomputer"인 행이 하나씩 있습니다.  
  
     구독자가 호스트 이름 "mycomputer"와 동기화되면 비교 시 데이터베이스 정렬이 대/소문자를 구분하므로 구독자는 행을 하나만 받습니다. 사전 계산 파티션을 사용하지 않을 경우 테이블의 데이터 정렬이 대/소문자를 구분하지 않으므로 구독자는 행을 두 개 모두 받습니다.  
  
## <a name="performance-of-precomputed-partitions"></a>사전 계산 파티션의 성능  
 구독자에서 게시자로 변경 내용이 업로드될 경우 사전 계산 파티션에서 성능 손실이 적게 발생하지만 병합 처리 시간의 대부분이 파티션을 평가하고 게시자에서 구독자로 변경 내용을 다운로드하는 데 소비되므로 성능을 향상시키는 것이 중요합니다. 동시에 동기화하는 구독자의 수와 한 파티션에서 다른 파티션으로 행을 이동하는 동기화당 업데이트 수에 따라 성능상의 이점이 달라집니다.  
  
## <a name="see-also"></a>참고 항목  
 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
