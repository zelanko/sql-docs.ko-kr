---
title: "구독자에서 데이터 유효성 검사 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "구독자 [SQL Server 복제], 데이터 유효성 검사"
  - "복제 [SQL Server], 데이터 유효성 검사"
  - "트랜잭션 복제, 데이터 유효성 검사"
  - "데이터 유효성 검사"
  - "병합 복제 데이터 유효성 검사 [SQL Server 복제], SQL Server Management Studio"
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 구독자에서 데이터 유효성 검사
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 구독자의 데이터에 대한 유효성을 검사하는 방법에 대해 설명합니다.  
  
 데이터 유효성 검사 프로세스는 세 부분으로 구성되어 있습니다.  
  
1.  게시에 대한 단일 구독이나 모든 구독을 유효성 검사용으로 *표시* 할 수 있습니다. **의**로컬 게시 **폴더와**로컬 구독 **폴더에서 사용할 수 있는** 구독 유효성 검사 **,** 구독 유효성 검사 **및** 모든 구독 유효성 검사 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자에서 유효성을 검사할 구독을 표시합니다. 또한 **모든 구독** 탭, **구독 조사 목록** 탭 및 복제 모니터의 게시 노드에서 구독을 표시할 수 있습니다. 복제 모니터를 시작 하는 방법에 대 한 정보를 참조 하십시오. [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)합니다.  
  
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
  
-   유효성 검사 결과는 유효성 검사의 성공 여부를 나타내지만 실패한 경우 유효성 검사에 실패한 행은 표시하지 않습니다. 게시자와 구독자에서 데이터를 비교하려면 [tablediff Utility](../../tools/tablediff-utility.md)를 사용합니다. 복제 된 데이터와 함께이 유틸리티를 사용 하는 방법에 대 한 자세한 내용은 참조 [차이 & #40;에 대 한 복제 된 테이블 비교 복제 프로그래밍 및 #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 트랜잭션 게시에 대한 구독의 데이터 유효성을 검사하려면(Management Studio)  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독을 유효성 검사를 클릭 한 다음 원하는 게시를 마우스 오른쪽 단추로 클릭 **구독 유효성 검사**합니다.  
  
4.  **구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 선택합니다.  
  
    -   **모든 SQL Server 구독 유효성 검사**를 선택합니다.  
  
    -   **다음 구독 유효성 검사**를 선택한 다음 하나 이상의 구독을 선택합니다.  
  
5.  (행 개수 또는 행 개수 및 체크섬)을 수행 하려면 유효성 검사의 유형을 지정 하려면 클릭 **유효성 검사 옵션**, 다음에서 옵션을 지정 하 고는 **구독 유효성 검사 옵션** 대화 상자입니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인합니다. 다음과 같이 각 구독에 대한 작업을 수행하세요.  
  
    1.  게시를 확장 하 고, 해당 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **동기화 상태 보기**합니다.  
  
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  
  
#### 병합 게시에 대한 단일 구독의 데이터 유효성을 검사하려면(Management Studio)  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독 유효성 검사, 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 하려는 게시 확장 **구독 유효성 검사**합니다.  
  
4.  **구독 유효성 검사** 대화 상자에서 **이 구독 유효성 검사**를 선택합니다.  
  
5.  (행 개수 또는 행 개수 및 체크섬)을 수행 하려면 유효성 검사의 유형을 지정 하려면 클릭 **옵션**, 다음에서 옵션을 지정 하 고는 **구독 유효성 검사 옵션** 대화 상자입니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  다음과 같이 복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인하세요.  
  
    1.  게시를 확장 하 고, 해당 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **동기화 상태 보기**합니다.  
  
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  
  
#### 병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면(Management Studio)  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  구독을 유효성 검사를 클릭 한 다음 원하는 게시를 마우스 오른쪽 단추로 클릭 **모든 구독 유효성 검사**합니다.  
  
4.  에 **모든 구독 유효성 검사** 대화 상자 (행 개수 또는 행 개수 및 체크섬)을 수행 하려면 유효성 검사의 유형을 지정 합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인합니다. 다음과 같이 각 구독에 대한 작업을 수행하세요.  
  
    1.  게시를 확장 하 고, 해당 구독을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **동기화 상태 보기**합니다.  
  
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  
  
#### 트랜잭션 게시에 대한 모든 밀어넣기 구독의 데이터 유효성을 검사하려면(복제 모니터)  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  구독을 유효성 검사를 클릭 한 다음 원하는 게시를 마우스 오른쪽 단추로 클릭 **구독 유효성 검사**합니다.  
  
3.  **구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 선택합니다.  
  
    -   **모든 SQL Server 구독 유효성 검사**를 선택합니다.  
  
    -   **다음 구독 유효성 검사**를 선택한 다음 하나 이상의 구독을 선택합니다.  
  
4.  (행 개수 또는 행 개수 및 체크섬)을 수행 하려면 유효성 검사의 유형을 지정 하려면 클릭 **유효성 검사 옵션**, 다음에서 옵션을 지정 하 고는 **구독 유효성 검사 옵션** 대화 상자입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  **모든 구독** 탭을 클릭합니다.  
  
7.  유효성 검사 결과를 확인합니다. 다음과 같이 각 밀어넣기 구독에 대한 작업을 수행하세요.  
  
    1.  에이전트를 실행 하지 않는 경우 해당 구독을 마우스 오른쪽 단추로 클릭 **동기화 시작**합니다.  
  
    2.  구독을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **세부 정보 보기**합니다.  
  
    3.  **선택한 세션의 동작** 텍스트 영역에 있는 **배포자에서 구독자로의 연결 기록** 탭의 정보를 확인합니다.  
  
#### 병합 게시에 대한 단일 밀어넣기 구독의 데이터 유효성을 검사하려면(복제 모니터)  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **모든 구독** 탭을 클릭합니다.  
  
3.  유효성을 검사 하 고 다음을 클릭 하 고 싶은 구독을 마우스 오른쪽 단추로 클릭 **구독 유효성 검사**합니다.  
  
4.  **구독 유효성 검사** 대화 상자에서 **이 구독 유효성 검사**를 선택합니다.  
  
5.  (행 개수 또는 행 개수 및 체크섬)을 수행 하려면 유효성 검사의 유형을 지정 하려면 클릭 **옵션**, 다음에서 옵션을 지정 하 고는 **구독 유효성 검사 옵션** 대화 상자입니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  **모든 구독** 탭을 클릭합니다.  
  
8.  다음과 같이 유효성 검사 결과를 확인하세요.  
  
    1.  에이전트를 실행 하지 않는 경우 해당 구독을 마우스 오른쪽 단추로 클릭 **동기화 시작**합니다.  
  
    2.  구독을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **세부 정보 보기**합니다.  
  
    3.  **선택한 세션에 대한 마지막 메시지** 텍스트 영역에 있는 **동기화 기록** 탭의 정보를 확인합니다.  
  
#### 병합 게시에 대한 모든 밀어넣기 구독의 데이터 유효성을 검사하려면(복제 모니터)  
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.  
  
2.  구독을 유효성 검사를 클릭 한 다음 원하는 게시를 마우스 오른쪽 단추로 클릭 **모든 구독 유효성 검사**합니다.  
  
3.  에 **모든 구독 유효성 검사** 대화 상자 (행 개수 또는 행 개수 및 체크섬)을 수행 하려면 유효성 검사의 유형을 지정 합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  **모든 구독** 탭을 클릭합니다.  
  
6.  유효성 검사 결과를 확인합니다. 다음과 같이 각 밀어넣기 구독에 대한 작업을 수행하세요.  
  
    1.  에이전트를 실행 하지 않는 경우 해당 구독을 마우스 오른쪽 단추로 클릭 **동기화 시작**합니다.  
  
    2.  구독을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **세부 정보 보기**합니다.  
  
    3.  **선택한 세션에 대한 마지막 메시지** 텍스트 영역에 있는 **동기화 기록** 탭의 정보를 확인합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 트랜잭션 게시의 모든 아티클에 대해 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_publication_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)합니다. 지정 **@publication** 는 다음 값 중 하나에 대 한 고 **@rowcount_only**:  
  
    -   **1** -행 개수의 유효성 검사에만 사용 (기본값)  
  
    -   **2** -행 개수 및 이진 체크섬.  
  
    > [!NOTE]  
    >  실행 하는 동안 [sp_publication_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), [sp_article_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 게시의 각 아티클에 대해 실행 됩니다. 성공적으로 실행 하려면 [sp_publication_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), 게시 된 기본 테이블의 모든 열에 대 한 SELECT 권한이 있어야 합니다.  
  
2.  (옵션) 각 구독에 대해 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 참조 [복제 된 데이터의 유효성을 검사](../../relational-databases/replication/validate-replicated-data.md)합니다.  
  
#### 트랜잭션 게시의 단일 아티클에 대한 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_article_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)합니다. 지정 **@publication**, 아티클 이름 **@article**, 는 다음 값 중 하나에 대 한 고 **@rowcount_only**:  
  
    -   **1** -행 개수의 유효성 검사에만 사용 (기본값)  
  
    -   **2** -행 개수 및 이진 체크섬.  
  
    > [!NOTE]  
    >  성공적으로 실행 하려면 [sp_article_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), 게시 된 기본 테이블의 모든 열에 대 한 SELECT 권한이 있어야 합니다.  
  
2.  (옵션) 각 구독에 대해 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 참조 [복제 된 데이터의 유효성을 검사](../../relational-databases/replication/validate-replicated-data.md)합니다.  
  
#### 트랜잭션 게시에 대한 단일 구독자의 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 사용 하 여 명시적 트랜잭션을 엽니다 [BEGIN TRANSACTION & #40; TRANSACT-SQL & #41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_marksubscriptionvalidation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)합니다. 게시에 대 한 지정 **@publication**, 에 대 한 구독자의 이름을 **@subscriber**, 및에 대 한 구독 데이터베이스의 이름을 **@destination_db**합니다.  
  
3.  (옵션) 유효성을 검사할 각 구독에 대해 2단계를 반복합니다.  
  
4.  게시 데이터베이스의 게시자에서 실행 [sp_article_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)합니다. 지정 **@publication**, 아티클 이름 **@article**, 는 다음 값 중 하나에 대 한 고 **@rowcount_only**:  
  
    -   **1** -행 개수의 유효성 검사에만 사용 (기본값)  
  
    -   **2** -행 개수 및 이진 체크섬.  
  
    > [!NOTE]  
    >  성공적으로 실행 하려면 [sp_article_validation (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), 게시 된 기본 테이블의 모든 열에 대 한 SELECT 권한이 있어야 합니다.  
  
5.  게시 데이터베이스의 게시자에서 사용 하 여 트랜잭션 커밋 [트랜잭션 커밋 & #40; TRANSACT-SQL & #41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)합니다.  
  
6.  (옵션) 유효성을 검사할 각 아티클에 대해 1~5단계를 반복합니다.  
  
7.  (옵션) 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
8.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)을 참조하세요.  
  
#### 병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_validatemergepublication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)합니다. **@publication** 을 지정하고 **@level**에 다음 값 중 하나를 지정합니다.  
  
    -   **1** -행 개수만 유효성 검사 합니다.  
  
    -   **3** -행 개수 이진 체크섬 유효성 검사 합니다.  
  
     이렇게 하면 모든 구독이 유효성 검사 대상으로 표시됩니다.  
  
2.  각 구독에 대해 병합 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)을 참조하세요.  
  
#### 병합 게시에 대한 선택한 구독의 데이터 유효성을 검사하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_validatemergesubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)합니다. 지정 **@publication**, 에 대 한 구독자의 이름을 **@subscriber**, 에 대 한 구독 데이터베이스의 이름을 **@subscriber_db**, 는 다음 값 중 하나에 대 한 고 **@level**:  
  
    -   **1** -행 개수만 유효성 검사 합니다.  
  
    -   **3** -행 개수 이진 체크섬 유효성 검사 합니다.  
  
     이렇게 하면 선택한 구독이 유효성 검사 대상으로 표시됩니다.  
  
2.  각 구독에 대해 병합 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다.  
  
4.  유효성을 검사할 각 구독에 대해 1~3단계를 반복합니다.  
  
> [!NOTE]  
>  병합 게시에 대 한 구독도 유효성을 검사할 수는 동기화의 끝에 지정 하는 **-유효성을 검사** 실행 될 때 매개 변수는 [복제 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)합니다.  
  
#### 병합 에이전트 매개 변수를 사용하여 구독의 데이터 유효성을 검사하려면  
  
1.  명령 프롬프트에서 다음 방법 중 하나를 사용하여 구독자(끌어오기 구독) 또는 배포자(밀어넣기 구독)에서 병합 에이전트를 시작합니다.  
  
    -   값을 지정 하면 **1** (행 개수) 또는 **3** (행 개수 및 이진 체크섬)에 대 한는 **-유효성을 검사** 매개 변수입니다.  
  
    -   지정 **행 개수 유효성 검사** 또는 **행 개수 및 체크섬 유효성 검사** 에 대 한는 **-ProfileName** 매개 변수입니다.  
  
     자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 또는 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 복제를 사용하면 RMO(복제 관리 개체)를 통해 구독자의 데이터가 게시자의 데이터와 일치하는지를 프로그래밍 방식으로 확인할 수 있습니다. 사용하는 개체는 복제 토폴로지의 유형에 따라 달라집니다. 트랜잭션 복제에는 게시에 대한 모든 구독의 유효성 검사가 필요합니다.  
  
> [!NOTE]  
>  예를 들어 참조 [예 (RMO)](#RMOExample), 이 섹션의 뒷부분에 나오는 합니다.  
  
#### 트랜잭션 게시의 모든 아티클에 대해 데이터 유효성을 검사하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시에 대 한 속성입니다. 설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 나머지 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 메서드. 다음을 전달합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   유효성 검사가 완료된 후 배포 에이전트를 중지할지 여부를 나타내는 부울입니다.  
  
     이렇게 하면 해당 아티클이 유효성 검사 대상으로 표시됩니다.  
  
5.  배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작하여 각 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 또는 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가됩니다. 자세한 내용은 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
#### 병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시에 대 한 속성입니다. 설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 나머지 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 메서드. 원하는 전달 <xref:Microsoft.SqlServer.Replication.ValidationOption>합니다.  
  
5.  각 구독에 대해 병합 에이전트를 실행하여 유효성 검사를 시작하거나 예약된 다음 에이전트가 실행될 때까지 기다립니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가되며, 복제 모니터를 사용하여 해당 결과를 볼 수 있습니다. 자세한 내용은 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
#### 병합 게시에 대한 단일 구독의 데이터 유효성을 검사하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시에 대 한 속성입니다. 설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 나머지 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 메서드. 유효성을 검사 중인 구독자 및 구독 데이터베이스의 이름 및 원하는 전달 <xref:Microsoft.SqlServer.Replication.ValidationOption>합니다.  
  
5.  유효성 검사를 시작할 구독에 대해 병합 에이전트를 실행하거나 예약된 다음 에이전트가 실행될 때까지 기다립니다. 자세한 내용은 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가되며, 복제 모니터를 사용하여 해당 결과를 볼 수 있습니다. 자세한 내용은 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)을 참조하세요.  
  
###  <a name="RMOExample"></a> 예(RMO)  
 이 예제에서는 트랜잭션 게시에 대한 모든 구독을 대상으로 행 개수를 확인하도록 표시합니다.  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 이 예제에서는 병합 게시에 대한 특정 구독을 대상으로 행 개수를 확인하도록 표시합니다.  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  