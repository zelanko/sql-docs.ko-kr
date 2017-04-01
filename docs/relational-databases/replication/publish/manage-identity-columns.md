---
title: "ID 열 관리 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ID 값 [SQL Server 복제]"
  - "병합 복제 [SQL Server 복제], ID 범위 관리"
  - "게시 [SQL Server 복제], ID 열"
  - "트랜잭션 복제, ID 범위 관리"
  - "ID 열 [SQL Server], 복제"
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# ID 열 관리
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 ID 열을 관리하는 방법에 대해 설명합니다. 구독자 삽입이 게시자로 복제되는 경우 구독자와 게시자 모두에 동일한 ID 값이 할당되지 않도록 ID 열을 관리해야 합니다. 복제는 ID 범위를 자동으로 관리할 수 있으며, 사용자가 ID 범위 관리를 수동으로 처리하도록 선택할 수도 있습니다.  복제에서 제공 하는 id 범위 관리 옵션에 대 한 정보를 참조 하십시오. [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 ID 열을 관리하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   둘 이상의 게시에 테이블을 게시하는 경우 두 게시에 대해 동일한 ID 범위 관리 옵션을 지정해야 합니다. 자세한 내용은의 "게시 테이블에서 둘 이상의 게시" 참조 [게시 데이터 및 데이터베이스 개체](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)합니다.  
  
-   여러 테이블에 사용할 수 있는 또는 테이블을 참조 하지 않고 응용 프로그램에서 호출할 수 있는 자동 증분 번호를 만들려면 참조 [시퀀스 번호](../../../relational-databases/sequence-numbers/sequence-numbers.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 에 id 열 관리 옵션을 지정 된 **속성** 탭은 **아티클 속성-\< 문서>** 새 게시 마법사의 대화 상자. 이 마법사를 사용 하는 방법에 대 한 자세한 내용은 참조 [발행물 만들기](../../../relational-databases/replication/publish/create-a-publication.md)합니다. 새 게시 마법사에서의 속성 설정은 다음과 같습니다.  
  
-   선택 하는 경우 **병합 게시** 또는 **구독 업데이트가 있는 트랜잭션 게시** 에 **게시 유형** 페이지 자동 또는 수동 id 범위 관리를 선택 합니다 (자동, 기본, 권장). 테이블을 게시한 후에 이 속성은 수정할 수 없지만 다른 관련 속성은 수정할 수 있습니다.  
  
-   다른 게시 유형을 선택한 경우에 ID 범위 관리는 수동으로 설정해야 합니다.  
  
 id 범위 및 임계값을 수정 된 **속성** 탭은 **아티클 속성-\< 문서>**, 에서 제공 되는 **게시 속성-\< 게시>** 대화 상자. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### ID 열 관리 옵션을 지정하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]를 실행하는 게시자의 경우 새 게시 마법사의 **게시 유형** 페이지에서 **병합 게시** 또는 **업데이트할 수 있는 구독이 있는 트랜잭션 게시**를 선택합니다.  
  
2.  **아티클** 페이지에서 ID 열이 있는 테이블을 선택합니다.  
  
3.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
4.  에 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자는 **Id 범위 관리** 섹션에서 설정는 **자동 id 범위 관리** 속성을 **자동** 또는 **수동** (실행 중인 게시자에 대 한 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상), 또는 **True** 또는 **False** (의 버전을 실행 하는 게시자에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]).  
  
5.  4단계에서 **자동** 또는 **True** 를 선택한 경우 다음 표를 참조하여 옵션 값을 입력합니다. 이러한 설정을 사용 하는 방법에 대 한 자세한 내용은의 "Id 범위 할당" 섹션을 참조 하십시오. [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.  
  
    |옵션|값|설명|  
    |------------|-----------|-----------------|  
    |**게시자 범위 크기**|범위 크기에 대한 정수 값(예: 20000)|"Id 범위 할당" 섹션을 참조 [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.|  
    |**구독자 범위 크기**|범위 크기에 대한 정수 값(예: 10000)|"Id 범위 할당" 섹션을 참조 [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.|  
    |**범위 임계값 비율**|백분율 임계값의 정수 값(예: 90은 90%)|새 ID 범위를 할당하기 전에 노드에 사용되는 전체 ID 값의 백분율입니다.<br /><br /> <br /><br /> 참고: 이 값은 지정은 해야 하지만 지연 업데이트 구독을 사용하는 구독자와 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 또는 다른 SQL Server 에디션의 이전 버전을 실행하는 병합 게시 구독자에 의해서만 사용됩니다. 자세한 내용은의 "Id 범위 할당" 섹션을 참조 하십시오. [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.|  
    |**다음 범위 시작 값**|정수 값. 읽기 전용입니다.|다음 범위가 시작되는 값입니다. 예를 들어 현재 범위가 5001-6000이면 이 값은 6001이 됩니다.|  
    |**최대 ID 값**|정수 값. 읽기 전용입니다.|ID 열의 최대값입니다. 열의 기본 데이터 형식에 따라 결정됩니다.|  
    |**ID 증가값**|정수 값. 읽기 전용입니다.|각 삽입 작업마다 ID 열의 숫자가 증가 또는 감소되는 크기이며 일반적으로 1로 설정합니다.|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 테이블을 게시한 후 ID 범위 및 임계값을 수정하려면  
  
1.  에 **문서** 의 페이지는 **게시 속성-\< 게시>** 대화 상자, id 열이 있는 테이블을 선택 합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자는 **Id 범위 관리** 섹션에서 다음 속성 중 하나 이상을 실행 하는 것에 대 한 값을 입력: **게시자 범위 크기**, **구독자 범위 크기**, 및 **범위 임계값 비율**합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  클릭 **확인** 에 **게시 속성-\< 게시>** 대화 상자입니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 아티클이 작성될 때 ID 범위 관리 옵션을 지정할 수 있습니다.  
  
#### 트랜잭션 게시에 대한 아티클을 정의할 때 자동 ID 범위 관리를 설정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 게시 되는 원본 테이블에 id 열을 하는 경우의 값을 지정 **자동** 에 대 한 **@identityrangemanagementoption**, 을 위해 게시자에 할당 된 id 값의 범위 **@pub_identity_range**, 에 대 한 각 구독자에 게 할당 된 id 값의 범위 **@identity_range**, 및에 대 한 새 id 범위 할당 되기 전에 사용 되는 전체 id 값의 비율 **@threshold**합니다. 문서를 정의 하는 방법에 대 한 자세한 내용은 참조 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)합니다.  
  
    > [!NOTE]  
    >  ID 열의 데이터 형식은 모든 구독자에 할당되는 ID의 전체 범위를 지원하기에 충분할 만큼 커야 합니다.  
  
#### 트랜잭션 게시에 대한 아티클을 정의할 때 자동 ID 범위 관리를 해제하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. **@identityrangemanagementoption** 에 **manual**값을 지정합니다. 문서를 정의 하는 방법에 대 한 자세한 내용은 참조 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)합니다.  
  
2.  구독자 업데이트에 대한 충돌 발생을 방지하려면 구독자에서 ID 아티클 열에 범위를 할당합니다. 자세한 내용은 섹션을 참조 항목에서 수동 id 범위 관리를 위한 범위 할당에 [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.  
  
#### 병합 게시에 대한 아티클을 정의할 때 자동 ID 범위 관리를 설정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 게시 되는 원본 테이블에 id 열을 하는 경우의 값을 지정 **자동** 에 대 한 **@identityrangemanagementoption**, 에 대 한 서버 구독에 할당 된 id 값의 범위 **@pub_identity_range**, 게시자 및에 대 한 각 클라이언트 구독에 할당 된 id 값의 범위 **@identity_range**, 및에 대 한 새 id 범위 할당 되기 전에 사용 되는 전체 id 값의 비율 **@threshold**합니다. 새 id 범위가 할당 되는 경우에 대 한 자세한 내용은 항목의 Id 범위 할당 참조 [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다. 문서를 정의 하는 방법에 대 한 자세한 내용은 참조 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)합니다.  
  
    > [!NOTE]  
    >  특히 서버 구독이 있는 구독자의 경우 ID 열의 데이터 형식은 모든 구독자에 할당되는 ID의 전체 범위를 지원하기에 충분할 만큼 커야 합니다.  
  
#### 병합 게시에 대한 아티클을 정의할 때 자동 ID 범위 관리를 해제하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. **@identityrangemanagementoption**에 다음 값 중 하나를 지정합니다.  
  
    -   **수동** -구독자 업데이트에 대 한 Id 범위를 수동으로 할당 되어야 합니다.  
  
    -   **none** -게시자에서 Id 열은 구독자에서 id 열으로 정의 되지 것입니다.  
  
     문서를 정의 하는 방법에 대 한 자세한 내용은 참조 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)합니다.  
  
2.  구독자 업데이트에 대한 충돌 발생을 방지하려면 구독자에서 ID 아티클 열에 범위를 할당합니다.  
  
#### 스냅숏 또는 트랜잭션 게시의 기존 아티클에 대한 자동 ID 범위 관리 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) 의 값을 확인 하 고 **identityrangemanagementoption** 결과 집합에 있습니다. 이 값이 **0**이면 자동 ID 범위 관리가 설정되지 않은 것입니다.  
  
2.  결과 집합의 **identityrangemanagementoption** 값이 **1**이면 다음과 같이 설정을 변경합니다.  
  
    -   할당된 된 id 범위를 변경 하려면 실행 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 게시 데이터베이스의 게시자에서. 값을 지정 **identity_range** 또는 **pub_identity_range** 에 대 한 **@property** 새 범위 값에 대 한 **@value**합니다.  
  
    -   새 범위가 할당 되는 임계값을 변경 하려면 실행 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 게시 데이터베이스의 게시자에서. **@property** 에 **threshold** 값, **@value**에 새 임계값을 지정합니다.  
  
#### 병합 게시의 기존 아티클에 대한 자동 ID 범위 관리 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 의 값을 확인 하 고 **identity_support** 결과 집합에 있습니다. 이 값이 **0**이면 자동 ID 범위 관리가 설정되지 않은 것입니다.  
  
2.  하는 경우의 값 **identity_support** 결과에서 집합은 **1**, 다음과 같이 설정을 변경 합니다.  
  
    -   할당된 된 id 범위를 변경 하려면 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 게시 데이터베이스의 게시자에서. 값을 지정 **identity_range** 또는 **pub_identity_range** 에 대 한 **@property** 새 범위 값에 대 한 **@value**합니다.  
  
    -   새 범위가 할당 되는 임계값을 변경 하려면 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 게시 데이터베이스의 게시자에서. **@property** 에 **threshold** 값, **@value**에 새 임계값을 지정합니다. 새 id 범위가 할당 되는 경우에 대 한 자세한 내용은 항목의 Id 범위 할당 참조 [Id 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)합니다.  
  
    -   자동 id 범위 관리를 사용 하지 않으려면 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 게시 데이터베이스의 게시자에서. **@property** 에 **identityrangemanagementoption** 값을 지정하고 **@value** 에 **manual** 또는 **none**을 지정합니다.  
  
## 참고 항목  
 [피어 투 피어 트랜잭션 복제](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [ID 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  