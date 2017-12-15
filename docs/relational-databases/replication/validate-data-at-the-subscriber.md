---
title: "구독자에서 데이터 유효성 검사 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d78ec0ec5dcbb0fa259cc26950a9de9742bfaa6c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="validate-data-at-the-subscriber"></a>구독자에서 데이터 유효성 검사
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 구독자의 데이터에 대한 유효성을 검사하는 방법에 대해 설명합니다.  
  
 데이터 유효성 검사 프로세스는 세 부분으로 구성되어 있습니다.  
  
1.  게시에 대한 단일 구독이나 모든 구독을 유효성 검사용으로 *표시* 할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **로컬 게시** 폴더와 **로컬 구독** 폴더에서 사용할 수 있는 **구독 유효성 검사**, **구독 유효성 검사** 및 **모든 구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 표시합니다. 또한 **모든 구독** 탭, **구독 조사 목록** 탭 및 복제 모니터의 게시 노드에서 구독을 표시할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
2.  구독은 배포 에이전트(트랜잭션 복제의 경우)나 병합 에이전트(병합 복제의 경우)에 의해 다음 번에 동기화될 때 유효성이 검사됩니다. 배포 에이전트는 일반적으로 계속 실행되므로 유효성 검사가 바로 수행됩니다. 병합 에이전트는 일반적으로 요청 시 실행되므로 에이전트를 실행한 다음 유효성 검사가 수행됩니다.  
  
3.  다음 위치에서 유효성 검사 결과를 확인합니다.  
  
    -   복제 모니터의 세부 정보 창의 **배포자에서 구독자로의 연결 기록** 탭(트랜잭션 복제의 경우) 및 **동기화 기록** 탭(병합 복제의 경우)  
  
    -   **의** 동기화 상태 보기 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]대화 상자  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **구독자의 데이터에 대한 유효성을 검사하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   복제 모니터에서 끌어오기 구독은 동기화할 수 없으므로 복제 모니터의 프로시저는 밀어넣기 구독에 대해서만 사용할 수 있습니다. 그러나 구독을 유효성 검사용으로 표시하고 복제 모니터에서 끌어오기 구독에 대한 유효성 검사 결과를 볼 수 있습니다.  
  
-   유효성 검사 결과는 유효성 검사의 성공 여부를 나타내지만 실패한 경우 유효성 검사에 실패한 행은 표시하지 않습니다. 게시자와 구독자에서 데이터를 비교하려면 [tablediff Utility](../../tools/tablediff-utility.md)를 사용합니다. 이 유틸리티를 복제된 데이터와 함께 사용하는 방법은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-validate-data-for-subscriptions-to-a-transactional-publication-management-studio"></a>트랜잭션 게시에 대한 구독의 데이터 유효성을 검사하려면(Management Studio)  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.  
  
4.  **구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 선택합니다.  
  
    -   **모든 SQL Server 구독 유효성 검사**를 선택합니다.  
  
    -   **다음 구독 유효성 검사**를 선택한 다음 하나 이상의 구독을 선택합니다.  
  
5.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **유효성 검사 옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인합니다. 다음과 같이 각 구독에 대한 작업을 수행하세요.  
  
    1.  게시를 확장하고 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  
  
#### <a name="to-validate-data-for-a-single-subscription-to-a-merge-publication-management-studio"></a>병합 게시에 대한 단일 구독의 데이터 유효성을 검사하려면(Management Studio)  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독 유효성을 검사할 게시를 확장하고 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.  
  
4.  **구독 유효성 검사** 대화 상자에서 **이 구독 유효성 검사**를 선택합니다.  
  
5.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  다음과 같이 복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인하세요.  
  
    1.  게시를 확장하고 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  
  
#### <a name="to-validate-data-for-all-subscriptions-to-a-merge-publication-management-studio"></a>병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면(Management Studio)  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사**를 클릭합니다.  
  
4.  **모든 구독 유효성 검사** 대화 상자에서 수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인합니다. 다음과 같이 각 구독에 대한 작업을 수행하세요.  
  
    1.  게시를 확장하고 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-transactional-publication-replication-monitor"></a>트랜잭션 게시에 대한 모든 밀어넣기 구독의 데이터 유효성을 검사하려면(복제 모니터)  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.  
  
3.  **구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 선택합니다.  
  
    -   **모든 SQL Server 구독 유효성 검사**를 선택합니다.  
  
    -   **다음 구독 유효성 검사**를 선택한 다음 하나 이상의 구독을 선택합니다.  
  
4.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **유효성 검사 옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  **모든 구독** 탭을 클릭합니다.  
  
7.  유효성 검사 결과를 확인합니다. 다음과 같이 각 밀어넣기 구독에 대한 작업을 수행하세요.  
  
    1.  에이전트가 실행되고 있지 않은 경우 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.  
  
    2.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
    3.  **선택한 세션의 동작** 텍스트 영역에 있는 **배포자에서 구독자로의 연결 기록** 탭의 정보를 확인합니다.  
  
#### <a name="to-validate-data-for-a-single-push-subscription-to-a-merge-publication-replication-monitor"></a>병합 게시에 대한 단일 밀어넣기 구독의 데이터 유효성을 검사하려면(복제 모니터)  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  유효성을 검사할 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.  
  
4.  **구독 유효성 검사** 대화 상자에서 **이 구독 유효성 검사**를 선택합니다.  
  
5.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  **모든 구독** 탭을 클릭합니다.  
  
8.  다음과 같이 유효성 검사 결과를 확인하세요.  
  
    1.  에이전트가 실행되고 있지 않은 경우 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.  
  
    2.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
    3.  **선택한 세션에 대한 마지막 메시지** 텍스트 영역에 있는 **동기화 기록** 탭의 정보를 확인합니다.  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-merge-publication-replication-monitor"></a>병합 게시에 대한 모든 밀어넣기 구독의 데이터 유효성을 검사하려면(복제 모니터)  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사**를 클릭합니다.  
  
3.  **모든 구독 유효성 검사** 대화 상자에서 수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  **모든 구독** 탭을 클릭합니다.  
  
6.  유효성 검사 결과를 확인합니다. 다음과 같이 각 밀어넣기 구독에 대한 작업을 수행하세요.  
  
    1.  에이전트가 실행되고 있지 않은 경우 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.  
  
    2.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
    3.  **선택한 세션에 대한 마지막 메시지** 텍스트 영역에 있는 **동기화 기록** 탭의 정보를 확인합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>트랜잭션 게시의 모든 아티클에 대해 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_publication_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)을 실행합니다. **@publication**를 지정하고 **@rowcount_only**에 다음 값 중 하나를 지정합니다.  
  
    -   **1** - 행 개수의 유효성만 검사합니다(기본값).  
  
    -   **2** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
    > [!NOTE]  
    >  [sp_publication_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)을 실행하면 게시의 각 아티클에 대해 [sp_article_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)이 실행됩니다. [sp_publication_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)을 올바르게 실행하려면 게시된 기본 테이블의 모든 열에 대해 SELECT 권한이 있어야 합니다.  
  
2.  (옵션) 각 구독에 대해 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)를 참조하세요.  
  
#### <a name="to-validate-data-for-a-single-article-in-a-transactional-publication"></a>트랜잭션 게시의 단일 아티클에 대한 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_article_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)을 실행합니다. **@publication**과 **@article**에 아티클 이름을 지정하고, **@rowcount_only**에 다음 값 중 하나를 지정합니다.  
  
    -   **1** - 행 개수의 유효성만 검사합니다(기본값).  
  
    -   **2** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
    > [!NOTE]  
    >  [sp_article_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)을 올바르게 실행하려면 게시된 기본 테이블의 모든 열에 대해 SELECT 권한이 있어야 합니다.  
  
2.  (옵션) 각 구독에 대해 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)를 참조하세요.  
  
#### <a name="to-validate-data-for-a-single-subscriber-to-a-transactional-publication"></a>트랜잭션 게시에 대한 단일 구독자의 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)을 사용하여 명시적 트랜잭션을 엽니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_marksubscriptionvalidation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)을 실행합니다. **@publication**에 게시를 지정하고 **@subscriber**에 구독자 이름을 지정한 후 **@destination_db**에 구독 데이터베이스 이름을 지정합니다.  
  
3.  (옵션) 유효성을 검사할 각 구독에 대해 2단계를 반복합니다.  
  
4.  게시 데이터베이스의 게시자에서 [sp_article_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)을 실행합니다. **@publication**과 **@article**에 아티클 이름을 지정하고, **@rowcount_only**에 다음 값 중 하나를 지정합니다.  
  
    -   **1** - 행 개수의 유효성만 검사합니다(기본값).  
  
    -   **2** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
    > [!NOTE]  
    >  [sp_article_validation&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)을 올바르게 실행하려면 게시된 기본 테이블의 모든 열에 대해 SELECT 권한이 있어야 합니다.  
  
5.  게시 데이터베이스의 게시자에서 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)을 사용하여 명시적 트랜잭션을 엽니다.  
  
6.  (옵션) 유효성을 검사할 각 아티클에 대해 1~5단계를 반복합니다.  
  
7.  (옵션) 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
8.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)을 참조하세요.  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_validatemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)을 실행합니다. **@publication**를 지정하고 **@level**에 다음 값 중 하나를 지정합니다.  
  
    -   **1** - 행 개수의 유효성만 검사합니다.  
  
    -   **3** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
     이렇게 하면 모든 구독이 유효성 검사 대상으로 표시됩니다.  
  
2.  각 구독에 대해 병합 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)을 참조하세요.  
  
#### <a name="to-validate-data-in-selected-subscriptions-to-a-merge-publication"></a>병합 게시에 대한 선택한 구독의 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_validatemergesubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)을 실행합니다. **@publication**을 지정하고 **@subscriber**에 구독자 이름을 지정하고 **@subscriber_db**에 구독 데이터베이스 이름을 지정한 후 **@level**에 다음 값 중 하나를 지정합니다.  
  
    -   **1** - 행 개수의 유효성만 검사합니다.  
  
    -   **3** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
     이렇게 하면 선택한 구독이 유효성 검사 대상으로 표시됩니다.  
  
2.  각 구독에 대해 병합 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다.  
  
4.  유효성을 검사할 각 구독에 대해 1~3단계를 반복합니다.  
  
> [!NOTE]  
>  **Replication Merge Agent** 를 실행할 때 [-Validate](../../relational-databases/replication/agents/replication-merge-agent.md)매개 변수를 지정하여 동기화가 끝날 때 병합 게시에 대한 구독의 유효성을 검사할 수도 있습니다.  
  
#### <a name="to-validate-data-in-a-subscription-using-merge-agent-parameters"></a>병합 에이전트 매개 변수를 사용하여 구독의 데이터 유효성을 검사하려면  
  
1.  명령 프롬프트에서 다음 방법 중 하나를 사용하여 구독자(끌어오기 구독) 또는 배포자(밀어넣기 구독)에서 병합 에이전트를 시작합니다.  
  
    -   **-Validate** 매개 변수에 **1** (행 개수) 또는 **3** (행 개수 및 이진 체크섬) 값을 지정합니다.  
  
    -   **-ProfileName** 매개 변수에 **행 개수 유효성 검사** 및 **행 개수 및 체크섬 유효성 검사** 를 지정합니다.  
  
     자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 또는 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 복제를 사용하면 RMO(복제 관리 개체)를 통해 구독자의 데이터가 게시자의 데이터와 일치하는지를 프로그래밍 방식으로 확인할 수 있습니다. 사용하는 개체는 복제 토폴로지의 유형에 따라 달라집니다. 트랜잭션 복제에는 게시에 대한 모든 구독의 유효성 검사가 필요합니다.  
  
> [!NOTE]  
>  예를 보려면 이 섹션의 뒷부분에 나오는 [예(RMO)](#RMOExample)를 참조하세요.  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>트랜잭션 게시의 모든 아티클에 대해 데이터 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 얻습니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 메서드를 호출합니다. 다음을 전달합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   유효성 검사가 완료된 후 배포 에이전트를 중지할지 여부를 나타내는 부울입니다.  
  
     이렇게 하면 해당 아티클이 유효성 검사 대상으로 표시됩니다.  
  
5.  배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작하여 각 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 또는 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가됩니다. 자세한 내용은 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 얻습니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 메서드를 호출합니다. 원하는 <xref:Microsoft.SqlServer.Replication.ValidationOption>을 전달합니다.  
  
5.  각 구독에 대해 병합 에이전트를 실행하여 유효성 검사를 시작하거나 예약된 다음 에이전트가 실행될 때까지 기다립니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가되며, 복제 모니터를 사용하여 해당 결과를 볼 수 있습니다. 자세한 내용은 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>병합 게시에 대한 단일 구독의 데이터 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 얻습니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 메서드를 호출합니다. 구독자 이름, 유효성을 검사할 구독 데이터베이스 및 원하는 <xref:Microsoft.SqlServer.Replication.ValidationOption>을 전달합니다.  
  
5.  유효성 검사를 시작할 구독에 대해 병합 에이전트를 실행하거나 예약된 다음 에이전트가 실행될 때까지 기다립니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가되며, 복제 모니터를 사용하여 해당 결과를 볼 수 있습니다. 자세한 내용은 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
###  <a name="RMOExample"></a> 예(RMO)  
 이 예제에서는 트랜잭션 게시에 대한 모든 구독을 대상으로 행 개수를 확인하도록 표시합니다.  
  
 [!code-cs[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 이 예제에서는 병합 게시에 대한 특정 구독을 대상으로 행 개수를 확인하도록 표시합니다.  
  
 [!code-cs[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  
