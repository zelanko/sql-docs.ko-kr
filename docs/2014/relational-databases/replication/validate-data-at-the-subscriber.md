---
title: 복제된 데이터의 유효성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4d09750c0cb81d64f5921ae2064b2e75edb6ca96
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047582"
---
# <a name="validate-replicated-data"></a>복제된 데이터의 유효성 검사
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 구독자의 데이터에 대한 유효성을 검사하는 방법에 대해 설명합니다.  

  트랜잭션 및 병합 복제를 사용하면 구독자의 데이터가 게시자의 데이터와 일치하는지 확인할 수 있습니다. 게시에 대한 특정 구독 또는 모든 구독에 대해 유효성 검사를 수행할 수 있습니다. 다음 유효성 검사 유형 중 하나를 지정합니다. 배포 에이전트 또는 병합 에이전트가 다음에 실행될 때 해당 유형에 따라 데이터의 유효성을 검사합니다.  
  
-   **행 개수만**. 이 유형은 구독자에 있는 테이블의 행 개수가 게시자에 있는 테이블의 행 개수와 동일한지 여부의 유효성만 검사하고 행 내용 일치 여부의 유효성은 검사하지 않습니다. 행 개수 유효성 검사에서는 최소 수준의 데이터 문제 인식을 위한 검사만 수행됩니다.    
-   **행 개수와 이진 체크섬**. 게시자 및 구독자에서 행 개수의 유효성을 검사할 뿐만 아니라 체크섬 알고리즘을 사용하여 모든 데이터의 체크섬을 계산합니다. 행 개수 확인을 실패하면 체크섬 계산이 수행되지 않습니다.  
  
 구독자의 데이터와 게시자의 데이터가 일치하는지에 대한 유효성 검사 외에도 병합 복제는 각 구독자에 대해 데이터가 올바르게 분할되었는지에 대한 유효성을 검사하는 기능을 제공합니다. 자세한 내용은 [병합 구독자의 파티션 정보 유효성 검사](validate-partition-information-for-a-merge-subscriber.md)를 참조하세요.  

## <a name="how-data-validation-works"></a>데이터 유효성 검사 작업 방식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 게시자에서 행 개수 또는 체크섬을 계산한 다음 그 값을 구독자에서 계산된 행 개수 또는 체크섬과 비교하여 데이터의 유효성을 검사합니다. 전체 게시 테이블과 전체 구독 테이블에 대해 각각 하나의 값이 계산되지만 `text`, `ntext` 또는 `image` 열의 데이터는 계산에 포함되지 않습니다.  
  
 계산이 수행되는 동안 행 개수 또는 체크섬이 실행될 테이블에 공유 잠금이 임시로 지정되지만 대부분 몇 초 내에 계산이 신속히 완료되고 공유 잠금이 제거됩니다.  
  
 이진 체크섬을 사용할 때는 데이터 페이지의 실제 행에 대한 CRC 대신 열 단위의 32비트 중복 검사(CRC)가 수행됩니다. 따라서 테이블의 열이 데이터 페이지에서 실제로 임의의 순서로 배열될 수 있지만, 해당 행에 대해 동일한 CRC로 컴퓨팅됩니다. 이진 체크섬 유효성 검사는 게시에 행 또는 열 필터가 있을 때 사용할 수 있습니다.  
  
 데이터 유효성 검사 프로세스는 세 부분으로 구성되어 있습니다.  
  
1.  게시에 대한 단일 구독이나 모든 구독을 유효성 검사용으로 *표시* 할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **로컬 게시** 폴더와 **로컬 구독** 폴더에서 사용할 수 있는 **구독 유효성 검사**, **구독 유효성 검사** 및 **모든 구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 표시합니다. 또한 **모든 구독** 탭, **구독 조사 목록** 탭 및 복제 모니터의 게시 노드에서 구독을 표시할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](monitor/start-the-replication-monitor.md)을 참조하세요.  
  
2.  구독은 배포 에이전트(트랜잭션 복제의 경우)나 병합 에이전트(병합 복제의 경우)에 의해 다음 번에 동기화될 때 유효성이 검사됩니다. 배포 에이전트는 일반적으로 계속 실행되므로 유효성 검사가 바로 수행됩니다. 병합 에이전트는 일반적으로 요청 시 실행되므로 에이전트를 실행한 다음 유효성 검사가 수행됩니다.  
  
3.  다음 위치에서 유효성 검사 결과를 확인합니다.  
  
    -  복제 모니터의 세부 정보 창의 **배포자에서 구독자로의 연결 기록** 탭(트랜잭션 복제의 경우) 및 **동기화 기록** 탭(병합 복제의 경우)    
    -  **의** 동기화 상태 보기 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]대화 상자  
  


  
## <a name="considerations-and-restrictions"></a>고려 사항 및 제한 사항  
  
-   복제 모니터에서 끌어오기 구독은 동기화할 수 없으므로 복제 모니터의 프로시저는 밀어넣기 구독에 대해서만 사용할 수 있습니다. 그러나 구독을 유효성 검사용으로 표시하고 복제 모니터에서 끌어오기 구독에 대한 유효성 검사 결과를 볼 수 있습니다.    
-   유효성 검사 결과는 유효성 검사의 성공 여부를 나타내지만 실패한 경우 유효성 검사에 실패한 행은 표시하지 않습니다. 게시자와 구독자에서 데이터를 비교하려면 [tablediff Utility](../../tools/tablediff-utility.md)를 사용합니다. 이 유틸리티를 복제된 데이터와 함께 사용하는 방법은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
 
데이터 유효성을 검사할 때 다음 사항을 고려하십시오.  
  
-   데이터 유효성을 검사하기 전에 구독자에서 모든 업데이트 작업을 중지해야 합니다. 유효성 검사가 수행 중일 때는 게시자에서 작업을 중지할 필요가 없습니다.    
-   큰 데이터 집합의 유효성을 검사할 때는 체크섬 및 이진 체크섬이 프로세서 리소스를 많이 요구할 수 있으므로 복제에 사용되는 서버에서 진행 중인 작업 수가 가장 적은 경우 유효성 검사가 수행되도록 예약해야 합니다.    
-   복제는 테이블의 유효성만 검사하고 게시자의 스키마 전용 아티클(예: 저장 프로시저)이 구독자의 스키마 전용 아티클과 동일한지 여부의 유효성은 검사하지 않습니다.    
-   게시된 테이블에는 이진 체크섬을 사용할 수 있습니다. 체크섬은 열 필터가 있는 테이블 또는 열을 삭제 또는 추가하는 ALTER TABLE 문으로 인해 열 오프셋이 다른 논리적 테이블 구조의 유효성을 검사할 수 없습니다.    
-   복제 유효성 검사에서는 `checksum` 및 **binary_checksum** 함수를 사용 합니다. 해당 동작에 대한 자세한 내용은 [CHECKSUM&#40;Transact-SQL&#41;](/sql/t-sql/functions/checksum-transact-sql) 및 [BINARY_CHECKSUM&#40;Transact-SQL&#41;](/sql/t-sql/functions/binary-checksum-transact-sql)을 참조하세요.  
  
-   구독자에서의 데이터 형식과 게시자에서의 데이터 형식이 다른 경우 이진 체크섬 또는 체크섬 유효성 검사가 올바르지 않을 수 있습니다. 이 문제는 다음 중 하나를 수행할 경우 발생할 수 있습니다.    
    -   이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 형식을 매핑하도록 스키마 옵션을 명시적으로 설정한 경우.    
    -   병합 게시의 게시 호환성 수준을 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설정했으며 게시된 테이블에 이 버전에 대해 매핑해야 하는 데이터 형식이 하나 이상 들어 있는 경우.    
    -   구독을 수동으로 초기화하고 구독자에서 다른 데이터 형식을 사용하는 경우    
-   트랜잭션 복제의 변환 가능한 구독에서는 이진 체크섬 및 체크섬 유효성 검사가 지원되지 않습니다.   
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자로 복제된 데이터에 대해서는 유효성 검사가 지원되지 않습니다.  

## <a name="data-validation-results"></a>데이터 유효성 검사 결과  
 유효성 검사가 완료되면 배포 에이전트 또는 병합 에이전트는 성공 여부에 대한 메시지를 기록합니다. 복제는 유효성이 확인되지 못한 행은 보고하지 않습니다. 이러한 메시지는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 복제 모니터 및 복제 시스템 테이블에서 볼 수 있습니다. 위에 나열된 방법 항목에서 유효성 검사를 실행하고 결과를 확인하는 방법을 설명합니다.  
  
 유효성 검사 실패를 처리하려면 다음 사항을 살펴보십시오.  
  
-   **복제: 구독자가 데이터 유효성 검사에 실패했습니다**라는 복제 경고를 구성하여 검사 실패에 대한 알림을 받도록 합니다. 자세한 내용은 [미리 정의 된 복제 경고 구성 &#40;SQL Server Management Studio& # 41 (관리/구성-미리 정의 된 복제-경고-s e r v e r v e r-s e r v e r-s e r v e r  
  
-   유효성 검사 실패가 애플리케이션에 문제가 됩니까? 유효성 검사 실패가 문제가 되는 경우 수동으로 데이터를 업데이트하여 동기화하거나 구독을 다시 초기화합니다.  
  
    -   [tablediff 유틸리티](../../tools/tablediff-utility.md)를 사용하여 데이터를 업데이트할 수 있습니다. 이 유틸리티를 사용하는 방법은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
  
    -   다시 초기화에 대한 자세한 내용은 [구독 다시 초기화](reinitialize-subscriptions.md)를 참조하세요.   
 
  
## <a name="articles-in-transactional-replication"></a>트랜잭션 복제의 아티클 

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용  
  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.    
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.    
3.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.    
4.  **구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 선택합니다.    
    -   **모든 SQL Server 구독 유효성 검사**를 선택합니다.    
    -   **다음 구독 유효성 검사**를 선택한 다음 하나 이상의 구독을 선택합니다.    
5.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **유효성 검사 옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.    
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인합니다. 다음과 같이 각 구독에 대한 작업을 수행하십시오.    
    1.  게시를 확장하고 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.    
    2.  에이전트가 실행되고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  

### <a name="using-transact-sql-t-sql"></a>Transact-SQL(T-SQL) 사용

#### <a name="all-articles"></a>모든 아티클
  
1.  게시 데이터베이스의 게시자에서 [sp_publication_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql)을 실행합니다. ** \@ 게시** 를 지정 하 고 ** \@ rowcount_only**에 다음 값 중 하나를 지정 합니다.    
    -   **1** - 행 개수의 유효성만 검사합니다(기본값).    
    -   **2** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
    > [!NOTE]  
    >  [sp_publication_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql)을 실행하면 게시의 각 아티클에 대해 [sp_article_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)이 실행됩니다. [sp_publication_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql)을 올바르게 실행하려면 게시된 기본 테이블의 모든 열에 대해 SELECT 권한이 있어야 합니다.  
  
2.  (옵션) 각 구독에 대해 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요.    
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](validate-data-at-the-subscriber.md)를 참조하세요.  
  
#### <a name="single-article"></a>단일 아티클 
  
1.  게시 데이터베이스의 게시자에서 [sp_article_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)을 실행합니다. ** \@ 게시**, ** \@ 아티클의**아티클 이름 및 ** \@ rowcount_only**에 대 한 다음 값 중 하나를 지정 합니다.    
    -   **1** - 행 개수의 유효성만 검사합니다(기본값).    
    -   **2** -행 개수 및 이진 체크섬  
  
    > [!NOTE]  
    >  [sp_article_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)을 올바르게 실행하려면 게시된 기본 테이블의 모든 열에 대해 SELECT 권한이 있어야 합니다.  
  
2.  (옵션) 각 구독에 대해 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요.    
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](validate-data-at-the-subscriber.md)를 참조하세요.  
  
#### <a name="single-subscriber"></a>단일 구독자
  
1.  게시 데이터베이스의 게시자에서 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql)을 사용하여 명시적 트랜잭션을 엽니다.    
2.  게시 데이터베이스의 게시자에서 [sp_marksubscriptionvalidation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql)을 실행합니다. ** \@ 게시**에 대 한 게시, ** \@ 구독자**의 구독자 이름 및 ** \@ destination_db**에 대 한 구독 데이터베이스의 이름을 지정 합니다.    
3.  (옵션) 유효성을 검사할 각 구독에 대해 2단계를 반복합니다.    
4.  게시 데이터베이스의 게시자에서 [sp_article_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)을 실행합니다. ** \@ 게시**, ** \@ 아티클의**아티클 이름 및 ** \@ rowcount_only**에 대 한 다음 값 중 하나를 지정 합니다.    
    -   **1** - 행 개수의 유효성만 검사합니다(기본값).    
    -   **2** -행 개수 및 이진 체크섬  
  
    > [!NOTE]  
    >  [sp_article_validation&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)을 올바르게 실행하려면 게시된 기본 테이블의 모든 열에 대해 SELECT 권한이 있어야 합니다.  
  
5.  게시 데이터베이스의 게시자에서 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql)을 사용하여 명시적 트랜잭션을 엽니다.    
6.  (옵션) 유효성을 검사할 각 아티클에 대해 1~5단계를 반복합니다.    
7.  (옵션) 배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요.    
8.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [Validate Data at the Subscriber](validate-data-at-the-subscriber.md)을 참조하세요.  

##  <a name="all-push-subscriptions-to-a-transactional-publication"></a>트랜잭션 게시에 대 한 모든 밀어넣기 구독 

### <a name="using-replication-monitor"></a>복제 모니터 사용
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.    
2.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.    
3.  **구독 유효성 검사** 대화 상자에서 유효성을 검사할 구독을 선택합니다.    
    -   **모든 SQL Server 구독 유효성 검사**를 선택합니다.    
    -   **다음 구독 유효성 검사**를 선택한 다음 하나 이상의 구독을 선택합니다.   
4.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **유효성 검사 옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.    
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
6.  **모든 구독** 탭을 클릭합니다.    
7.  유효성 검사 결과를 확인합니다. 다음과 같이 각 밀어넣기 구독에 대한 작업을 수행하십시오.   
    1.  에이전트가 실행되고 있지 않은 경우 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.   
    2.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.    
    3.  **선택한 세션의 동작** 텍스트 영역에 있는 **배포자에서 구독자로의 연결 기록** 탭의 정보를 확인합니다.  
  

## <a name="for-a-single-subscription-to-a-merge-publication"></a>병합 게시에 대한 단일 구독의 경우
  
### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.    
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.    
3.  구독 유효성을 검사할 게시를 확장하고 구독을 마우스 오른쪽 단추로 클릭한 다음 **구독 유효성 검사**를 클릭합니다.    
4.  **구독 유효성 검사** 대화 상자에서 **이 구독 유효성 검사**를 선택합니다.    
5.  수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정하려면 **옵션**을 클릭한 다음 **구독 유효성 검사 옵션** 대화 상자에서 옵션을 지정합니다.    
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
7.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인 합니다.  
    1.  게시를 확장하고 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.   
    2.  에이전트가 실행 되 고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭 합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  

### <a name="using-transact-sql-t-sql"></a>Transact-SQL(T-SQL) 사용

1.  게시 데이터베이스의 게시자에서 [sp_validatemergesubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql)을 실행합니다. ** \@ 게시**, ** \@ 구독자**의 구독자 이름, ** \@ subscriber_db**에 대 한 구독 데이터베이스 이름 및 ** \@ level**에 대 한 다음 값 중 하나를 지정 합니다.   
    -   **1** - 행 개수의 유효성만 검사합니다.    
    -   **3** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
     이렇게 하면 선택한 구독이 유효성 검사 대상으로 표시됩니다.  
  
2.  각 구독에 대해 병합 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요.    
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다.    
4.  유효성을 검사할 각 구독에 대해 1~3단계를 반복합니다.  
  
> [!NOTE]  
>  **Replication Merge Agent** 를 실행할 때 [-Validate](agents/replication-merge-agent.md)매개 변수를 지정하여 동기화가 끝날 때 병합 게시에 대한 구독의 유효성을 검사할 수도 있습니다.  

  
## <a name="for-all-subscriptions-to-a-merge-publication"></a>병합 게시에 대한 모든 구독의 경우

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용 
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.    
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.    
3.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사**를 클릭합니다.    
4.  **모든 구독 유효성 검사** 대화 상자에서 수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정합니다.    
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
6.  복제 모니터 또는 **동기화 상태 보기** 대화 상자에서 유효성 검사 결과를 확인합니다. 다음과 같이 각 구독에 대한 작업을 수행하십시오.    
    1.  게시를 확장하고 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.   
    2.  에이전트가 실행 되 고 있지 않은 경우 **동기화 상태 보기** 대화 상자에서 **시작** 을 클릭 합니다. 대화 상자에서는 유효성 검사와 관련된 정보 메시지를 보여 줍니다.  
  
     유효성 검사와 관련된 메시지가 나타나지 않는 경우 에이전트가 이미 이어서 나타나는 메시지를 로깅한 것입니다. 이 경우 복제 모니터에서 유효성 검사 결과를 확인합니다. 자세한 내용은 이 항목의 복제 모니터 사용 방법을 참조하세요.  

### <a name="using-transact-sql-t-sql"></a>Transact-SQL(T-SQL) 사용

1.  게시 데이터베이스의 게시자에서 [sp_validatemergepublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql)을 실행합니다. ** \@ 게시** 를 지정 하 고 ** \@ 수준**에 다음 값 중 하나를 지정 합니다.    
    -   **1** - 행 개수의 유효성만 검사합니다.    
    -   **3** - 행 개수 및 이진 체크섬의 유효성을 검사합니다.  
  
     이렇게 하면 모든 구독이 유효성 검사 대상으로 표시됩니다.  
  
2.  각 구독에 대해 병합 에이전트를 시작합니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요.    
3.  유효성 검사의 결과에 대한 에이전트 출력을 확인합니다. 자세한 내용은 [Validate Data at the Subscriber](validate-data-at-the-subscriber.md)을 참조하세요.  


## <a name="for-a-single-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 단일 밀어넣기 구독의 경우 

### <a name="using-replication-monitor"></a>복제 모니터 사용
  
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
  
## <a name="for-all-push-subscriptions-to-a-merge-publication"></a>병합 게시에 대한 모든 밀어넣기 구독의 경우 

### <a name="using-replication-monitor"></a>복제 모니터 사용
  
1.  복제 모니터에서 왼쪽 창의 게시자 그룹을 확장한 다음 게시자를 확장합니다.    
2.  구독 유효성을 검사할 게시를 마우스 오른쪽 단추로 클릭한 다음 **모든 구독 유효성 검사**를 클릭합니다.    
3.  **모든 구독 유효성 검사** 대화 상자에서 수행할 유효성 검사 유형(행 개수 또는 행 개수 및 체크섬)을 지정합니다.    
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
5.  **모든 구독** 탭을 클릭합니다.    
6.  유효성 검사 결과를 확인합니다. 다음과 같이 각 밀어넣기 구독에 대한 작업을 수행하십시오.    
    1.  에이전트가 실행되고 있지 않은 경우 해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 시작**을 클릭합니다.    
    2.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.    
    3.  **선택한 세션에 대한 마지막 메시지** 텍스트 영역에 있는 **동기화 기록** 탭의 정보를 확인합니다.  
  
  
## <a name="validate-data-using-merge-agent-parameters"></a>병합 에이전트 매개 변수를 사용 하 여 데이터 유효성 검사
  
1.  명령 프롬프트에서 다음 방법 중 하나를 사용하여 구독자(끌어오기 구독) 또는 배포자(밀어넣기 구독)에서 병합 에이전트를 시작합니다.    
    -   **-Validate** 매개 변수에 **1** (행 개수) 또는 **3** (행 개수 및 이진 체크섬) 값을 지정합니다.   
    -   **-ProfileName** 매개 변수에 **행 개수 유효성 검사** 및 **행 개수 및 체크섬 유효성 검사** 를 지정합니다.  
  
     자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 또는 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요.  
  
## <a name="using-replication-management-objects-rmo"></a>RMO(복제 관리 개체) 사용  
 복제를 사용하면 RMO(복제 관리 개체)를 통해 구독자의 데이터가 게시자의 데이터와 일치하는지를 프로그래밍 방식으로 확인할 수 있습니다. 사용하는 개체는 복제 토폴로지의 유형에 따라 달라집니다. 트랜잭션 복제에는 게시에 대한 모든 구독의 유효성 검사가 필요합니다.  
  
> [!NOTE]  
>  예를 보려면 이 섹션의 뒷부분에 나오는 [예(RMO)](#RMOExample)를 참조하세요.  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>트랜잭션 게시의 모든 아티클에 대해 데이터 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.    
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.   
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 얻습니다. 이 메서드가 `false`를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.    
4.  <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 메서드를 호출합니다. 다음을 전달합니다.    
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>    
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>    
    -   유효성 검사가 완료된 후 배포 에이전트를 중지할지 여부를 나타내는 부울입니다.  
  
     이렇게 하면 해당 아티클이 유효성 검사 대상으로 표시됩니다.  
  
5.  배포 에이전트를 아직 실행하지 않은 경우 배포 에이전트를 시작하여 각 구독을 동기화합니다. 자세한 내용은 [Synchronize a Push Subscription](synchronize-a-push-subscription.md) 또는 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가됩니다. 자세한 내용은 [Monitoring Replication](monitoring-replication.md)을 참조하세요.  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>병합 게시에 대한 모든 구독의 데이터 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.   
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.   
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 얻습니다. 이 메서드가 `false`를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.    
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 메서드를 호출합니다. 원하는 <xref:Microsoft.SqlServer.Replication.ValidationOption>을 전달합니다.    
5.  각 구독에 대해 병합 에이전트를 실행하여 유효성 검사를 시작하거나 예약된 다음 에이전트가 실행될 때까지 기다립니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가되며, 복제 모니터를 사용하여 해당 결과를 볼 수 있습니다. 자세한 내용은 [Monitoring Replication](monitoring-replication.md)을 참조하세요.  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>병합 게시에 대한 단일 구독의 데이터 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.    
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만듭니다. 게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정합니다. <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.    
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체의 나머지 속성을 얻습니다. 이 메서드가 `false`를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.    
4.  <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 메서드를 호출합니다. 구독자 이름, 유효성을 검사할 구독 데이터베이스 및 원하는 <xref:Microsoft.SqlServer.Replication.ValidationOption>을 전달합니다.    
5.  유효성 검사를 시작할 구독에 대해 병합 에이전트를 실행하거나 예약된 다음 에이전트가 실행될 때까지 기다립니다. 자세한 내용은 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 및 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)를 참조하세요. 유효성 검사 작업의 결과는 에이전트 기록에 추가되며, 복제 모니터를 사용하여 해당 결과를 볼 수 있습니다. 자세한 내용은 [Monitoring Replication](monitoring-replication.md)을 참조하세요.  
  
###  <a name="example-rmo"></a><a name="RMOExample"></a>예 (RMO)  
 이 예제에서는 트랜잭션 게시에 대한 모든 구독을 대상으로 행 개수를 확인하도록 표시합니다.  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 이 예제에서는 병합 게시에 대한 특정 구독을 대상으로 행 개수를 확인하도록 표시합니다.  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  
