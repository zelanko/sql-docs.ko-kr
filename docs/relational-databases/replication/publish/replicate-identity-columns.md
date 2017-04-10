---
title: "ID 열 복제 | Microsoft Docs"
ms.custom: ""
ms.date: "10/04/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ID [SQL Server 복제]"
  - "ID 값 [SQL Server 복제]"
  - "병합 복제 [SQL Server 복제], ID 범위 관리"
  - "게시 [SQL Server 복제], ID 열"
  - "트랜잭션 복제, ID 범위 관리"
  - "ID 열 [SQL Server], 복제"
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# ID 열 복제
  열에 IDENTITY 속성을 할당하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 ID 열을 포함하는 테이블에 순차적 개수대로 삽입되는 새 행을 자동으로 생성합니다. 자세한 내용은 참조 [ID 및 #40; 속성 및 #41; &#40; TRANSACT-SQL &#41;](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md)합니다. ID 열은 기본 키의 일부분으로 포함될 수 있으므로 ID 열에 중복 값을 사용하지 않아야 합니다. 둘 이상의 노드에서 업데이트된 ID 열을 복제 토폴로지에서 사용하려면 복제 토폴로지의 각 노드가 다른 범위의 ID 값을 사용해야 중복이 발생하지 않습니다.  
  
 예를 들어 게시자에 1-100 범위, 구독자 A에 101-200 범위, 그리고 구독자 B에 201-300 범위를 할당할 수 있습니다. 예를 들어 게시자에 행이 삽입되고 ID 값이 65라면 이 값이 각 구독자에 복제됩니다. 복제가 각 구독자에 데이터를 삽입할 때 구독자 테이블의 ID 열 값을 증가시키지는 않습니다. 대신 리터럴 값 65가 삽입됩니다. 복제 에이전트 삽입이 아닌 사용자 삽입만 ID 열 값을 증가시킵니다.  
  
 복제는 모든 게시 및 구독 유형에서 ID 열을 처리하므로 사용자가 열을 수동으로 관리하거나 복제를 통해 자동으로 관리되도록 할 수 있습니다.  
  
> [!NOTE]  
>  열이 구독자로 복제될 때 데이터가 일치하지 않을 수 있기 때문에 게시된 테이블에 ID 열을 추가할 수 없습니다. 게시자의 ID 열 값은 영향을 받는 테이블 행이 실제로 저장된 순서에 따라 달라집니다. 구독자에서는 행이 다르게 저장될 수 있으므로 ID 열의 값이 같은 행에 대해 다를 수 있습니다.  
  
## ID 범위 관리 옵션 지정  
 복제는 3가지 ID 범위 관리 옵션을 제공합니다.  
  
-   자동. 구독자에서 업데이트를 수행하는 병합 복제 및 트랜잭션 복제에 사용됩니다. 게시자 및 구독자에 대한 크기 범위를 지정하면 복제는 새 범위의 할당을 자동으로 관리합니다. 복제는 구독자의 ID 열에 NOT FOR REPLICATION 옵션을 설정하므로 사용자 삽입만 구독자에서 값을 증가시킬 수 있습니다.  
  
    > [!NOTE]  
    >  구독자는 게시자와 동기화해야 새 범위를 받을 수 있습니다. 구독자에게는 ID 범위가 자동으로 할당되므로 구독자가 계속해서 새 범위를 요청할 경우 전체 ID 범위 공급이 중단될 수 있습니다.  
  
-   수동. 구독자에서 업데이트를 수행하지 않는 스냅숏 복제와 트랜잭션 복제 또는 피어 투 피어 트랜잭션 복제에 사용되거나 응용 프로그램이 ID 범위를 프로그래밍 방식으로 제어해야 할 경우 사용됩니다. 수동 관리를 지정하면 범위가 게시자 및 각 구독자에 할당되었는지 확인하고 초기 범위가 사용된 경우에는 새 범위가 할당되었는지 확인해야 합니다. 복제는 구독자의 ID 열에 NOT FOR REPLICATION 옵션을 설정합니다.  
  
-   없음 이 옵션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전과의 호환성을 위해서만 권장되며 트랜잭션 게시용 저장 프로시저 인터페이스에서만 사용할 수 있습니다.  
  
 Id 범위 관리 옵션을 지정 하려면 참조 [Id 열 관리](../../../relational-databases/replication/publish/manage-identity-columns.md)합니다.  
  
## ID 범위 할당  
 병합 복제 및 트랜잭션 복제는 여러 가지 방법으로 범위를 할당합니다. 이 섹션에서는 3가지 방법을 설명합니다.  
  
 ID 열을 복제하는 경우에는 두 가지 범위, 즉 게시자와 구독자에 할당된 범위와 열의 데이터 형식 범위를 고려해야 합니다. 다음 표에서는 일반적으로 ID 열에 사용되는 데이터 형식에 사용할 수 있는 범위를 보여 줍니다. 범위는 토폴로지의 모든 노드에서 사용됩니다. 예를 들어 1로 시작하여 1씩 증가하는 **smallint** 를 사용할 경우 게시자 및 모든 구독자에 대한 최대 삽입 수는 32,767입니다. 실제 삽입 수는 사용된 값에 차이가 있는지 여부와 임계값이 사용되는지 여부에 따라 달라집니다. 임계값에 대한 자세한 내용은 이 항목의 뒷부분에 나올 "병합 복제" 및 "지연 업데이트 구독이 있는 트랜잭션 복제" 섹션을 참조하십시오.  
  
 삽입 후 id 범위를 소모 하는 게시자를 하는 경우 자동으로 할당할 수 새 범위 삽입의 멤버에 의해 수행 된 경우는 **db_owner** 고정된 데이터베이스 역할입니다. 해당 역할, 로그 판독기 에이전트, 병합 에이전트 또는 구성원 인 사용자에 없는 사용자가 삽입을 수행 했으면 하는 경우의 **db_owner** 역할을 실행 해야 [sp_adjustpublisheridentityrange (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)합니다. 트랜잭션 게시의 경우 새 범위를 자동으로 할당하려면 로그 판독기 에이전트가 실행되고 있어야 합니다. 기본적으로 에이전트는 계속 실행됩니다.  
  
> [!WARNING]  
>  큰 일괄 처리 동안 복제 트리거 삽입은 삽입의 각 행에 대해 한 번만 발생합니다. ID 범위가 큰 삽입 시 사용되는 경우 **INSERT INTO** 문과 같은 insert 문이 실패할 수 있습니다.  
  
|데이터 형식|범위|  
|---------------|-----------|  
|**tinyint**|자동 관리에서 지원되지 않음|  
|**smallint**|-2^15(-32,768) ~ 2^15-1(32,767)|  
|**int**|-2^31(-2,147,483,648) ~ 2^31-1(2,147,483,647)|  
|**bigint**|-2^63(-9,223,372,036,854,775,808) ~ 2^63-1(9,223,372,036,854,775,807)|  
|**decimal** 및 **numeric**|-10^38+1 ~ 10^38-1|  
  
> [!NOTE]  
>  여러 테이블에서 사용할 수 있거나 테이블을 참조하지 않고 응용 프로그램에서 호출할 수 있는 자동으로 증가하는 번호를 만들려면 [시퀀스 번호](../../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
### 병합 복제  
 ID 범위는 게시자에 의해 관리되고 병합 에이전트에 의해 구독자로 전파됩니다. 재게시 계층에서는 범위가 루트 게시자와 재게시자에 의해 관리됩니다. ID 값은 게시자의 풀에서 할당됩니다. 새 게시 마법사 또는 사용 하 여 게시에 id 열이 있는 문서를 추가 하면 [sp_addmergearticle &#40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), 값을 지정 합니다.  
  
-   **@identity_range** 초기 클라이언트 구독인 게시자와 구독자 모두에 할당 되는 id 범위 크기를 제어 하는 매개 변수입니다.  
  
    > [!NOTE]  
    >  이전 버전의를 실행 하는 구독자에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 이 매개 변수 (보다는 **@pub_identity_range** 매개 변수) 또한 재게시 구독자 id 범위 크기를 제어 합니다.  
  
-    **@pub_identity_range** (데이터를 다시 게시에 필요) 서버 구독인 구독자에 게 할당 된 재게시 작업에 대 한 id 범위 크기를 제어 하는 매개 변수입니다. 구독 유형이 서버 구독인 모든 구독자는 실제로 데이터를 재게시하지 않더라도 재게시 작업을 위한 범위를 받습니다.  
  
-   **@threshold** 매개 변수 - [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 또는 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 구독에 새 ID 범위가 필요한 시기를 결정하는 데 사용됩니다.  
  
 예를 들어에 대해 10000을 지정할 수 있습니다 **@identity_range** 및에 대해 500000 **@pub_identity_range**합니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 게시자 및 모든 구독자(구독 유형이 서버 구독인 구독자 포함)에게 기본 범위 10000이 할당됩니다. 서버 구독이 있는 구독자에는 기본 범위 500000 재게시 구독자와 동기화 하는 구독자가 사용할 수 있는 할당 됩니다 (도 지정 해야 **@identity_range**, **@pub_identity_range**, 및 **@threshold** 재게시 구독자에서 게시의 아티클에 대해).  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상을 실행하는 각 구독자는 보조 ID 범위도 받습니다. 보조 범위의 크기는 주 범위의 크기와 같습니다. 주 범위를 모두 사용하면 보조 범위가 사용되고 병합 에이전트가 구독자에 새 범위를 할당합니다. 새 범위는 보조 범위가 되고 구독자가 ID 값을 사용하는 한 프로세스는 계속 진행됩니다.  
  
  
### 지연 업데이트 구독이 있는 트랜잭션 복제  
 ID 범위는 배포자에 의해 관리되고 배포 에이전트에 의해 구독자로 전파됩니다. ID 값은 배포자의 풀에서 할당됩니다. 풀 크기는 데이터 형식의 크기와 ID 열에 사용되는 증가값을 기반으로 합니다. 새 게시 마법사 또는 사용 하 여 게시에 id 열이 있는 문서를 추가 하면 [sp_addarticle (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), 값을 지정 합니다.  
  
-    **@identity_range** 처음에 모든 구독자에 게 할당 하는 id 범위 크기를 제어 하는 매개 변수입니다.  
  
-    **@pub_identity_range** 매개 변수를 게시자에 할당 된 id 범위 크기를 제어 합니다.  
  
-   **@threshold** 매개 변수 - 구독에 새 ID 범위가 필요한 시기를 결정하는 데 사용됩니다.  
  
 예를 들어에 대해 10000을 지정할 수 있습니다 **@pub_identity_range**, 1000으로 **@identity_range** (구독자에서의 업데이트 수가 가정)에 대해 80% **@threshold**합니다. 구독자에서 800(1000의 80%)이 삽입되면 구독자에 새 범위가 할당됩니다. 게시자에서 8000이 삽입되면 게시자에 새 범위가 할당됩니다. 새 범위를 지정하면 테이블의 ID 범위 값에 간격이 발생합니다. 더 높은 임계값을 지정하면 이러한 간격이 줄어들지만 시스템의 내결함성이 저하됩니다. 어떤 이유로든 배포 에이전트를 실행할 수 없으면 구독자에서 ID가 보다 빠른 속도로 줄어들 수 있습니다.  
  
## ID 범위 수동 관리를 위한 범위 할당  
 ID 범위 수동 관리를 지정할 경우 게시자와 각 구독자가 서로 다른 ID 범위를 사용하고 있는지 확인해야 합니다. 예를 들어 게시자에 있는 테이블의 ID 열이 `IDENTITY(1,1)`로 정의되어 있다고 가정합니다. 이 ID 열은 1에서 시작하고 행이 삽입될 때마다 1씩 증가합니다. 게시자의 테이블에 5,000개의 행이 있고 응용 프로그램 수명 동안 테이블이 얼마간 커질 것으로 예상되는 경우 게시자는 1-10,000 범위를 사용할 수 있습니다. 두 개의 구독자가 있는 경우 구독자 A는 10,001-20,000을 사용하고 구독자 B는 20,001-30,000을 사용할 수 있습니다.  
  
 스냅숏 또는 다른 방법으로 구독자가 초기화되면 DBCC CHECKIDENT를 실행하여 구독자에게 해당 ID 범위의 시작 지점을 할당합니다. 예를 들어 구독자 A에서 `DBCC CHECKIDENT('<TableName>','reseed',10001)`를 실행하고 구독자 B에서 `CHECKIDENT('<TableName>','reseed',20001)`를 실행합니다.  
  
 게시자 또는 구독자에 새 범위를 할당하려면 DBCC CHECKIDENT를 실행하고 새 값을 지정하여 테이블의 초기값을 다시 설정합니다. 새 범위를 할당해야 하는 시기를 결정하는 몇 가지 방법이 있습니다. 예를 들어 응용 프로그램에 노드가 범위를 거의 다 사용하는 시기를 감지하고 DBCC CHECKIDENT를 사용하여 새 범위를 할당하는 메커니즘이 있을 수 있습니다. 또한 범위를 벗어나는 ID 값이 사용되는 경우 행을 추가할 수 없도록 하는 CHECK 제약 조건을 추가할 수 있습니다.  
  
## 데이터베이스 복원 후 ID 범위 처리  
 ID 범위 자동 관리를 사용하는 경우 백업에서 구독자를 복원하면 구독자가 자동으로 새 ID 값 범위를 요청합니다. 백업에서 게시자가 복원되는 경우에는 게시자에 적절한 범위가 할당되었는지 확인해야 합니다. 병합 복제를 위해 사용 하 여 새 범위를 할당 [sp_restoremergeidentityrange (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql.md)합니다. 트랜잭션 복제의 경우 사용된 값 중 가장 높은 값을 확인한 후 새 범위의 시작 지점을 설정합니다. 게시 데이터베이스가 복원된 후 다음 절차를 따르십시오.  
  
1.  모든 구독자에서 모든 작업을 중지합니다.  
  
2.  ID 열을 포함하는 게시된 각 테이블의 경우에는 다음을 수행하십시오.  
  
    1.  각 구독자의 구독 데이터베이스에서 `IDENT_CURRENT('<TableName>')`를 실행합니다.  
  
    2.  모든 구독자에서 발견된 값 중 가장 높은 값을 기록합니다.  
  
    3.  게시자의 게시 데이터베이스에서 `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`)를 실행합니다.  
  
    4.  게시자의 게시 데이터베이스에서 `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`를 실행합니다.  
  
    > [!NOTE]  
    >  ID 열의 값이 증가값이 아닌 감소값으로 설정되면 발견된 값 중 가장 낮은 값을 기록하고 해당 값으로 초기값을 다시 설정합니다.  
  
## 관련 항목:  
 [BACKUP&#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [DBCC CHECKIDENT & #40입니다. TRANSACT-SQL &#41;](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_CURRENT & #40입니다. TRANSACT-SQL &#41;](../../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md)   
 [sp_adjustpublisheridentityrange & #40입니다. TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)  
  
  