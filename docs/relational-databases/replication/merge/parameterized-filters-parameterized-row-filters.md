---
title: 매개 변수가 있는 행 필터 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], dynamic filters
- merge replication [SQL Server replication], dynamic filters
- parameterized filters [SQL Server replication]
- filters [SQL Server replication], dynamic
- merge replication parameterized filters [SQL Server replication]
- publications [SQL Server replication], parameterized filters
- parameterized filters [SQL Server replication], about parameterized filters
- filters [SQL Server replication], parameterized
- dynamic filters [SQL Server replication]
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55de7bcfd14c4a3fde78ac6b62874b75b103e01b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127713"
---
# <a name="parameterized-filters---parameterized-row-filters"></a>매개 변수가 있는 필터 - 매개 변수가 있는 행 필터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  매개 변수가 있는 행 필터를 사용하면 여러 게시를 만들지 않고도 데이터의 여러 파티션을 서로 다른 구독자로 보낼 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 매개 변수가 있는 행 필터를 동적 필터라고 불렀습니다. 파티션은 테이블에 있는 행의 하위 집합입니다. 게시된 테이블의 각 행은 매개 변수가 있는 필터를 만들 때 선택한 설정에 따라 하나의 파티션에만 속하거나(겹치지 않는 파티션 생성) 두 개 이상의 파티션에 속할 수 있습니다(겹치는 파티션 생성).  
  
 겹치지 않는 파티션을 구독 간에 공유하게 하거나 지정된 파티션을 한 구독에서만 받도록 제한할 수 있습니다. 파티션의 동작을 제어하는 설정은 나중에 이 항목의 "적절한 필터링 옵션 사용"에서 설명합니다. 이 설정을 사용하면 매개 변수가 있는 필터링을 애플리케이션 및 성능 요구 사항에 알맞게 조정할 수 있습니다. 일반적으로 겹치는 파티션은 유연성이 뛰어나고, 단일 구독으로 복제되는 겹치지 않는 파티션은 성능이 뛰어납니다.  
  
 매개 변수가 있는 필터는 단일 테이블에서 사용되며 일반적으로 조인 필터와 함께 사용하여 관련 테이블로 필터링을 확장합니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)를 참조하세요.  
  
 매개 변수가 있는 행 필터를 정의하거나 수정하려면 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하십시오.  
  
## <a name="how-parameterized-filters-work"></a>매개 변수가 있는 필터의 동작 방식  
 매개 변수가 있는 행 필터는 WHERE 절을 사용하여 게시할 데이터를 선택합니다. 정적 행 필터와는 달리 해당 절에 리터럴 값을 지정하는 대신 하나 또는 둘 모두를 지정합니다. 사용자 정의 함수를 사용할 수도 있지만 사용자 정의 함수는 함수 본문에 SUSER_SNAME() 또는 HOST_NAME()을 포함해야 하거나 `MyUDF(SUSER_SNAME()`과 같은 시스템 함수 중 하나를 평가해야 합니다. 사용자 정의 함수의 본문에 SUSER_SNAME() 또는 HOST_NAME()이 포함되어 있는 경우 함수에 매개 변수를 전달할 수 없습니다.  
  
 SUSER_SNAME() 및 HOST_NAME() 시스템 함수는 병합 복제에 사용하는 것이 아니라 병합 복제에서 매개 변수가 있는 필터링용으로 사용합니다.  
  
-   SUSER_SNAME()은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스 연결에 대한 로그인 정보를 반환합니다. 매개 변수가 있는 필터에서 사용하면 병합 에이전트가 게시자로 연결할 때 사용한 로그인을 반환합니다. 로그인은 구독을 만들 때 지정합니다.  
  
-   HOST_NAME()은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 연결한 컴퓨터의 이름을 반환합니다. 이 시스템 함수를 매개 변수가 있는 필터에 사용하면 기본적으로 병합 에이전트가 실행 중인 컴퓨터의 이름이 반환됩니다. 끌어오기 구독의 경우 구독자의 이름을 반환하고 밀어넣기 구독의 경우 배포자의 이름을 반환합니다.  
  
     구독자 또는 배포자 이름 대신 다른 값으로 이 함수를 재정의할 수도 있습니다. 일반적으로 애플리케이션에서는 판매 직원 이름 또는 판매 직원 ID와 같은 의미 있는 값으로 이 함수를 재정의합니다. 자세한 내용은 이 항목의 "HOST_NAME() 값 재정의"를 참조하십시오.  
  
 시스템 함수에서 반환된 값을 사용자가 필터링하는 테이블에서 지정한 열과 비교한 다음 해당 데이터가 구독자로 다운로드됩니다. 구독이 초기화되어 초기 스냅샷에 해당 데이터만 들어 있을 경우와 구독이 동기화될 때마다 이 비교를 수행합니다. 기본적으로 게시자에서 발생한 변경으로 인해 행이 파티션에서 이동되는 경우 해당 행은 구독자에서 삭제됩니다. 이 동작은 [sp_addmergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)의 **@allow_partition_realignment** 매개 변수를 사용하여 제어할 수 있습니다.  
  
> [!NOTE]  
>  매개 변수가 있는 필터에 대해 비교가 수행될 경우 항상 데이터베이스 데이터 정렬을 사용합니다. 예를 들어 데이터베이스 데이터 정렬에서는 대/소문자를 구분하지 않지만 테이블 또는 열 데이터 정렬에서는 대/소문자를 구분할 경우 비교 시 대/소문자를 구분하지 않습니다.  
  
### <a name="filtering-with-susersname"></a>SUSER_SNAME()으로 필터링  
 **예제 데이터베이스의** Employee 테이블 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 을 고려해 봅니다. 이 테이블의 **LoginID**열에는 각 직원에 대한 로그인이 '*domain\login*' 형식으로 포함되어 있습니다. 직원이 자신에게 관련된 데이터만 받을 수 있도록 이 테이블을 필터링하려면 다음과 같은 필터 절을 지정합니다.  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 예를 들어 값이 'adventure-works\john5'인 직원이 있습니다. 병합 에이전트가 게시자로 연결할 경우 구독을 만들 때 사용자가 지정한 로그인(이 경우 'adventure-works\john5')을 사용합니다. 그러면 병합 에이전트는 SUSER_SNAME()에서 반환된 값을 해당 테이블의 값과 비교한 다음 **LoginID** 열에 'adventure-works\john5'라는 값이 포함된 행만 다운로드합니다.  
  
### <a name="filtering-with-hostname"></a>HOST_NAME()으로 필터링  
 **HumanResources.Employee** 테이블을 고려해 봅니다. 이 테이블의 **ComputerName** 과 같은 열에 각 직원의 컴퓨터 이름이 '*name_computertype*' 형식으로 포함되어 있다고 가정합니다. 직원이 자신에게 관련된 데이터만 받을 수 있도록 이 테이블을 필터링하려면 다음과 같은 필터 절을 지정합니다.  
  
```  
ComputerName = HOST_NAME()  
```  
  
 예를 들어 값이 'john5_laptop'인 직원이 있습니다. 병합 에이전트가 게시자로 연결하면 HOST_NAME()에서 반환된 값을 해당 테이블의 값과 비교한 다음 **ComputerName** 열에 'john5_laptop'이라는 값이 포함된 행만 다운로드합니다.  
  
 함수를 필터에서 함께 사용할 수도 있습니다. 예를 들어 직원이 자신의 컴퓨터에서 자신의 로그인을 사용할 때만 데이터를 받도록 하려면 필터 절을 다음과 같이 지정합니다.  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 HOST_NAME() 값을 재정의하지 않을 경우 HOST_NAME()으로 필터링하는 방법은 일반적으로 끌어오기 구독에만 사용합니다. 함수에서 반환되는 값은 병합 에이전트가 실행 중인 컴퓨터의 이름입니다. 끌어오기 구독의 경우 각 구독마다 값이 다르지만 밀어넣기 구독의 경우 값이 동일합니다. 밀어넣기 구독의 경우 병합 에이전트는 모두 배포자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  HOST_NAME() 함수의 값을 재정의할 수 있으므로 HOST_NAME()이 포함된 필터를 사용하여 데이터 파티션에 대한 액세스를 제어할 수 없습니다. 데이터 파티션에 대한 액세스를 제어하려면 SUSER_SNAME()을 사용하거나 SUSER_SNAME()을 HOST_NAME()과 함께 사용합니다. 또는 정적 행 필터를 사용합니다.  
  
#### <a name="overriding-the-hostname-value"></a>HOST_NAME() 값 재정의  
 위에서 설명한 것처럼 HOST_NAME()은 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 연결된 컴퓨터의 이름을 반환합니다. 매개 변수가 있는 필터를 사용할 경우 구독을 만들 때 값을 입력하여 이 값을 재정의하는 것이 일반적입니다. 그러면 HOST_NAME() 함수는 컴퓨터 이름 대신 사용자가 지정한 값을 반환합니다.  
  
> [!NOTE]  
>  HOST_NAME()을 재정의할 경우 HOST_NAME() 함수에 대한 모든 호출은 사용자가 지정한 값을 반환합니다. 다른 애플리케이션이 컴퓨터 이름을 반환하는 HOST_NAME()에 종속되지 않아야 합니다.  
  
 **HumanResources.Employee** 테이블을 고려해 봅니다. 이 테이블에는 **EmployeeID**열이 포함되어 있습니다. 각 직원이 자신에게 관련된 데이터만 받을 수 있도록 이 테이블을 필터링하려면 다음과 같은 필터 절을 지정합니다.  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 예를 들어 직원 Pamela Ansman-Wolfe에게 직원 ID로 280을 할당합니다. 이 직원에 대한 구독을 만들 때 HOST_NAME() 값에 직원 ID 값(이 경우 280)을 지정합니다. 병합 에이전트가 게시자로 연결하면 HOST_NAME()에서 반환된 값을 해당 테이블의 값과 비교한 다음 **EmployeeID** 열에 280이라는 값이 포함된 행만 다운로드합니다.  
  
> [!IMPORTANT]
>  HOST_NAME() 함수는 **nchar** 값을 반환하므로 위의 예처럼 필터 절의 열이 숫자 데이터 형식인 경우 CONVERT를 사용해야 합니다. 성능상의 이유로 `CONVERT(nchar,EmployeeID) = HOST_NAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 대신 `EmployeeID = CONVERT(int,HOST_NAME())`예제에서 보여준 방식을 사용하는 것이 좋습니다. 이 절을 **@subset_filterclause** @allow_partition_realignment [@subset_filterclause](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)매개 변수에 사용할 수 있지만 일반적으로 새 게시 마법사에서는 사용할 수 없습니다. 마법사는 필터 절을 실행하여 유효성을 검사하는데 컴퓨터 이름을 **int**에서는 매개 변수가 있는 행 필터를 동적 필터라고 불렀습니다. 새 게시 마법사를 사용할 경우 게시에 대한 스냅샷을 만들기 전에 마법사에서 `CONVERT(nchar,EmployeeID) = HOST_NAME()` 을 지정한 다음 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 을 사용하여 해당 절을 `EmployeeID = CONVERT(int,HOST_NAME())` 로 변경하는 것이 좋습니다.  
  
 **HOST_NAME() 값을 재정의하려면**  
  
 다음 방법 중 하나를 사용하여 HOST_NAME() 값을 재정의할 수 있습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: 새 구독 마법사의 **HOST\_NAME\(\) 값** 페이지에서 값을 지정합니다. 구독 만들기에 대한 자세한 내용은 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md)을 참조하세요.  
  
-   복제 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 프로그래밍: [sp_addmergesubscription&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)(밀어넣기 구독의 경우) 또는 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)(끌어오기 구독의 경우)의 **@hostname** 매개 변수에 값을 지정합니다.  
  
-   병합 에이전트: 명령줄 또는 에이전트 프로필을 통해 **-Hostname** 매개 변수의 값을 지정합니다. 병합 에이전트에 대한 자세한 내용은 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)를 참조하십시오. 에이전트 프로필에 대한 자세한 내용은 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하십시오.  
  
## <a name="initializing-a-subscription-to-a-publication-with-parameterized-filters"></a>매개 변수가 있는 필터로 게시에 대한 구독 초기화  
 병합 게시에서 매개 변수가 있는 행 필터를 사용하면 복제 시 각 구독이 두 부분으로 구성된 스냅샷으로 초기화됩니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
## <a name="using-the-appropriate-filtering-options"></a>적절한 필터링 옵션 사용  
 매개 변수가 있는 필터를 사용할 경우 사용자가 제어하는 두 가지 중요한 영역이 있습니다.  
  
-   병합 복제에서 필터를 처리하는 방법은 **use partition groups** 및 **keep partition changes**게시 설정 중 하나를 통해 제어할 수 있습니다.  
  
-   구독자 간에 데이터를 공유하는 방법은 아티클 설정 **partition options**에 반영해야 합니다.  
  
 필터링 옵션을 설정하려면 [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)를 참조하십시오.  
  
### <a name="setting-use-partition-groups-and-keep-partition-changes"></a>'use partition groups' 및 'keep partition changes' 설정  
 **use partition groups** 및 **keep partition changes** 옵션은 모두 게시 데이터베이스에 추가 메타데이터를 저장하여 필터링된 아티클이 있는 게시에 대한 동기화 성능을 향상시킵니다. **use partition groups** 옵션은 사전 계산 파티션 기능을 사용하여 더욱 향상된 성능을 제공합니다. 게시의 아티클이 일련의 요구 사항을 충족하는 경우 이 옵션은 기본적으로 **true** 로 설정됩니다. 이러한 요구 사항에 대한 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요. 아티클이 사전 계산 파티션을 사용하기 위한 요구 사항을 만족시키지 못할 경우 **keep partition changes** 옵션이 **true**로 설정됩니다.  
  
### <a name="setting-partition-options"></a>'partition options' 설정  
 아티클을 만들 때 필터링된 테이블의 데이터를 구독자에서 공유하는 방식에 따라 **partition options** 속성의 값을 지정합니다. 속성은 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)및 **Article Properties** 대화 상자를 사용하여 네 값 중 하나로 설정할 수 있습니다. 새 게시 마법사와 **게시 속성** 대화 상자의 **필터 추가** 또는 **필터 편집** 대화 상자를 사용하여 이 속성을 두 개의 값 중 하나로 설정할 수 있습니다. 다음 표에서는 사용할 수 있는 값을 요약합니다.  
  
|설명|필터 추가 및 필터 편집에 있는 값|아티클 속성에 있는 값|저장 프로시저에 있는 값|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|파티션에 있는 데이터는 겹치며 구독자는 매개 변수가 있는 필터에서 참조된 열은 업데이트할 수 있습니다.|**이 테이블의 행을 여러 구독으로 이동**|**겹침**|**0**|  
|파티션에 있는 데이터는 겹치며 구독자는 매개 변수가 있는 필터에서 참조된 열은 업데이트할 수 없습니다.|N/A*|**겹침, 파티션 외부 데이터 변경 내용 허용 안 함**|**1**|  
|파티션에 있는 데이터가 겹치지 않으며 데이터는 구독자 간에 공유됩니다. 구독자는 매개 변수가 있는 필터에서 참조된 열은 업데이트할 수 없습니다.|N/A*|**겹치지 않음, 구독 간 공유**|**2**|  
|파티션에 있는 데이터는 겹치지 않으며 파티션당 하나의 구독이 있습니다. 구독자는 매개 변수가 있는 필터에서 참조된 열은 업데이트할 수 없습니다.**|**이 테이블의 행을 단일 구독으로 이동**|**겹치지 않음, 단일 구독**|**3**|  
  
 \*기본 필터링 옵션이 **0**, **1** 또는 **2**로 설정될 경우 **필터 추가** 및 **필터 편집** 대화 상자에 **이 테이블의 행을 여러 구독으로 이동**이 표시됩니다.  
  
 **이 옵션을 지정하면 해당 아티클의 각 데이터 파티션에 대해 하나의 구독만 허용합니다. 새 구독의 필터링 조건이 기존 구독과 동일한 파티션을 사용하도록 하여 두 번째 구독이 생성될 경우 기존 구독이 삭제됩니다.  
  
> [!IMPORTANT]  
>  구독자가 데이터를 공유하는 방식에 따라 **partition options** 값을 설정해야 합니다. 예를 들어 파티션당 구독이 하나 있는 겹치지 않는 파티션을 지정했지만 데이터가 다른 구독자에서 업데이트되는 경우 병합 에이전트가 동기화 중에 실패하고 데이터가 일치하지 않을 수 있습니다.  
  
#### <a name="selecting-the-appropriate-partition-option"></a>적절한 파티션 옵션 선택  
 겹치지 않는 파티션을 사전 계산 파티션과 함께 사용하여 일부 기능 제한이 허용되는 상황에서 성능을 향상시킬 수 있습니다. 사전 계산 파티션을 사용하면 구독자로 다운로드하는 속도는 빨라지지만 업로드 속도는 느려집니다. 겹치지 않는 파티션을 사용하면 사전 계산 파티션으로 인한 업로드 작업 손실을 최소할 수 있습니다. 사용하는 매개 변수가 있는 필터와 조인 필터가 복잡할수록 겹치지 않는 파티션의 성능상 이점이 더욱 분명하게 드러납니다.  
  
 게시에서 사용할 파티션 옵션을 결정할 경우 다음 시나리오를 고려하십시오.  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 에는 지정된 우편 번호에 해당하는 고객을 담당하는 판매원으로 구성된 이동 영업팀이 있습니다. 고객이 한 판매 지역에서 다른 판매 지역으로 이동할 경우 고객이 다른 판매원에게 할당되도록 애플리케이션에서 우편 변호를 업데이트해야 합니다. 매개 변수가 있는 필터는 고객의 우편 번호를 기준으로 하며 업데이트가 발생하면 한 판매원의 파티션에서 우편 번호가 제거되어 다른 판매원의 파티션으로 삽입됩니다. 이 작업에는 매개 변수가 있는 필터에서 참조되는 열을 업데이트하는 기능이 있는 겹치는 파티션이 필요합니다. 이 옵션을 사용하면 융통성을 최대로 높일 수 있지만 겹치지 않는 파티션보다 성능이 떨어질 수 있습니다.  
  
-   직업 소개소에는 각 지방의 지역 사무실로 전달할 데이터가 있습니다. 데이터는 겹치지 않습니다. 본사의 테이블에 있는 각 행은 하나의 파티션에만 포함되지만 이러한 행을 포함하는 파티션은 해당 지방의 여러 지역 사무실로 전송됩니다. 이 작업에는 구독 간에 파티션을 공유하는 겹치지 않는 파티션 옵션이 적합합니다. 이 옵션을 사용하면 겹치는 파티션에 비해 보다 뛰어난 성능을 제공하면서 애플리케이션 요구 사항도 만족시킵니다.  
  
-   겹치지 않는 파티션이 있고 하나의 구독만이 파티션에서 데이터를 받고 업데이트할 경우 더 많은 성능상의 이점이 있습니다. 이 시나리오는 POS(Point of Sale) 시스템 및 구독자에서 주로 데이터를 수집하여 게시자로 업로드하는 FF(Field Force) 애플리케이션에 적합합니다. 배달 애플리케이션의 **Package** 테이블을 고려해 보십시오. 각 패키지가 트럭에 실리면서 **Package** 테이블에서 패키지의 상태가 변경되고 해당 변경 내용은 다시 본사로 복제됩니다. 운전 기사는 두 대의 서로 다른 트럭에 실린 같은 패키지의 상태를 업데이트하지 않으므로 **Package** 테이블을 파티션당 하나의 구독이 있는 겹치지 않는 파티션으로 만들 수 있습니다.  
  
#### <a name="considerations-for-nonoverlapping-partitions"></a>겹치지 않는 파티션에 대한 고려 사항  
 겹치지 않는 파티션 사용 시 다음 사항을 고려하십시오.  
  
##### <a name="general-considerations"></a>일반적인 고려 사항  
  
-   게시에서는 사전 계산 파티션을 사용해야 합니다.  
  
-   행은 하나의 파티션에만 속해야 합니다.  
  
-   아티클은 논리적 레코드의 일부일 수 없습니다.  
  
-   대체 동기화 파트너는 지원되지 않습니다(이 기능은 사용되지 않음).  
  
-   구독자는 매개 변수가 있는 필터에서 참조된 열은 업데이트할 수 없습니다.  
  
-   파티션에 속하지 않는 구독자에서의 삽입은 삭제되지 않지만 다른 구독자로 복제되지 않습니다.  
  
-   겹치는 파티션을 사용하는 일부 환경에서 병합 에이전트가 데이터를 삽입하면 ID 범위가 조정됩니다. 겹치지 않는 파티션을 사용할 경우 구독 데이터베이스에서 ID 범위를 조정할 권한이 있는 사용자가 삽입할 때에만 범위가 조정됩니다. 사용자는 테이블의 소유자이거나 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##### <a name="additional-considerations-for-nonoverlapping-partitions-with-a-single-subscription-per-partition"></a>파티션당 하나의 구독이 있는 겹치지 않는 파티션에 대한 추가 고려 사항  
  
-   아티클은 하나의 게시에만 존재할 수 있으며 다시 게시할 수 없습니다.  
  
-   게시에서 구독자가 스냅샷 프로세스를 시작할 수 있어야 합니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
##### <a name="additional-considerations-for-join-filters"></a>조인 필터에 대한 추가 고려 사항  
  
-   조인 필터 계층에서 겹치는 파티션이 있는 아티클은 겹치지 않는 파티션이 있는 아티클 위에 표시될 수 없습니다. 즉 자식 아티클이 겹치지 않는 파티션을 사용하면 부모 아티클도 겹치지 않는 파티션을 사용해야 합니다. 조인 필터에 대한 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)를 참조하십시오.  
  
-   겹치지 않는 파티션이 자식인 조인 필터에서는 **join unique key** 속성을 1로 설정해야 합니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)을 참조하세요.  
  
-   아티클에는 매개 변수가 있는 필터 또는 조인 필터가 하나만 있어야 합니다. 매개 변수가 있는 필터가 있으면서 조인 필터에서 부모일 수 있습니다. 매개 변수가 있는 필터가 있으면서 조인 필터에서 자식일 수는 없습니다. 조인 필터가 두 개 이상일 수도 없습니다.  
  
-   게시자의 두 테이블에 조인 필터 관계가 있고 자식 테이블에는 부모 테이블에 없는 행이 있을 경우 부모 테이블에 없는 행을 삽입해도 관련된 행이 구독자로 다운로드되지 않습니다(겹치는 파티션의 경우 다운로드됨). 예를 들어 **SalesOrderHeader** 테이블에는 없는 행이 **SalesOrderDetail** 테이블에 있고 이 행을 **SalesOrderHeader**에 삽입하면 해당 행은 구독자로 다운로드되지만 **SalesOrderDetail** 의 행은 다운로드되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시간 기반 행 필터에 대한 최상의 구현 방법](../../../relational-databases/replication/merge/best-practices-for-time-based-row-filters.md)   
 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)   
 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
