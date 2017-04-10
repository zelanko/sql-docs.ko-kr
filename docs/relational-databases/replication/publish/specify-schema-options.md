---
title: "스키마 옵션 지정 | Microsoft Docs"
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
  - "스키마 [SQL Server 복제], 옵션"
  - "아티클 [SQL Server 복제], 트랜잭션 복제 옵션"
  - "아티클 [SQL Server 복제], 병합 복제 옵션"
  - "아티클 [SQL Server 복제], 스키마 옵션"
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 스키마 옵션 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 스키마 옵션을 지정하는 방법에 대해 설명합니다. 테이블 또는 뷰를 게시하는 경우 게시된 개체에 대해 복제되는 개체 작성 옵션을 제어할 수 있습니다. 아티클을 만들 때 이 옵션을 설정할 수 있으며 나중에 이 옵션을 변경할 수도 있습니다. 아티클에 대해 이 옵션을 명시적으로 지정하지 않으면 기본 옵션 집합이 정의됩니다.  
  
> [!NOTE]  
>  복제 저장 프로시저를 사용할 때의 기본 스키마 옵션은 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용하여 아티클을 추가할 때의 기본 옵션과 다를 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **스키마 옵션을 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시가 만들어진 후 스키마 옵션을 변경하면 새 스냅숏을 생성해야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   스키마 옵션의 전체 목록에 대 한 참조는 **@schema_option** 의 매개 변수 [sp_addarticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 및 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 제약 조건 및 트리거를 구독자에 복사할지 여부 등의 스키마 옵션을 지정 된 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자. 이 탭은 새 게시 마법사에서 사용할 수 있는 고 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 스키마 옵션을 지정하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자는 문서를 선택 하 고 클릭 **아티클 속성**합니다.  
  
2.  스키마 옵션 변경 내용을 적용할 아티클을 선택합니다.  
  
    -   클릭 **설정의 강조 표시 된 속성 \< ObjectType> 문서** 시작 하는 **아티클 속성-\< o b j>** 대화 상자, 속성이 대화 상자에서 변경한 내용을에 포함 된 개체 창에서 강조 표시 하는 개체에만 적용 됩니다는 **문서** 페이지입니다.  
  
    -   클릭 **설정 속성의 모든 \< ObjectType> 문서** 시작 하는 **모든 속성을 \< ObjectType> 문서** 대화 상자, 속성이 대화 상자에서 변경한 내용을에 개체 창에 있는 해당 유형의 모든 개체에 적용 되는 **문서** 게시에 대 한 선택 하지 않은 것을 포함 하 여 페이지.  
  
        > [!NOTE]  
        >  속성 변경 내용에서 **모든 속성을 \< ObjectType> 문서** 대화 상자에서 이전에 수행 된 모든 재정의 **아티클 속성-\< o b j>** 대화 상자. 예를 들어 특정 개체 유형의 모든 아티클에 대해 여러 기본값을 설정하고 개별 개체에 대해 일부 속성도 설정하려면 먼저 모든 아티클의 기본값을 설정합니다. 그런 다음 개별 개체에 대해 속성을 설정합니다.  
  
3.  에 **개체 및 설정 구독자로 복사** 및 **대상 개체** 의 섹션은 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자에서 옵션에 대 한 값을 지정 합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
5.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 스키마 옵션을 지정 하는 16 진수 값으로는 [| (비트 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 하나 이상의 옵션의 결과입니다. 자세한 내용은 참조 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 및 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다.  
  
> [!NOTE]  
>  비트 연산을 수행하기 전에 스키마 옵션 값을 **binary** 에서 **int** 로 변환해야 합니다. 자세한 내용은 참조 [CAST 및 CONVERT & #40; TRANSACT-SQL & #41;](../../../t-sql/functions/cast-and-convert-transact-sql.md)합니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 아티클을 정의할 때 스키마 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 이 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체, **@source_object**, 에 대 한 데이터베이스 개체의 유형 **@type**, 및 [| (비트 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 에 대 한 하나 이상의 스키마 옵션의 결과 **@schema_option**합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### 병합 게시에 대한 아티클을 정의할 때 스키마 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 이 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체, **@source_object**, 및 [| (비트 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 에 대 한 하나 이상의 스키마 옵션의 결과 **@schema_option**합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### 스냅숏 또는 트랜잭션 게시의 기존 아티클에 대한 스키마 옵션을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)합니다. **@publication** 에 아티클이 속한 게시의 이름을 지정하고 **@article**에 아티클의 이름을 지정합니다. 값은 **schema_option** 결과 집합의 열입니다.  
  
2.  실행 한 [& (비트 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 단계 1과 원하는 스키마에서 값을 사용 하 여 작업 옵션의 옵션이 설정 되어 있는지 확인 하는 값입니다.  
  
    -   결과가 **0**이면 옵션이 설정되지 않은 것입니다.  
  
    -   결과가 옵션 값이면 옵션이 이미 설정된 것입니다.  
  
3.  옵션을 설정 하지 않으면 경우 실행 하는 [| (비트 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 1 단계의 값과 원하는 스키마 옵션 값을 사용 하는 작업입니다.  
  
4.  게시 데이터베이스의 게시자에서 실행 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)합니다. 문서에 속한 게시의 이름을 지정 **@publication**, 아티클 이름 **@article**, 값 **schema_option** 에 대 한 **@property**, 3 단계의 16 진수 결과 **@value**합니다.  
  
5.  스냅숏 에이전트를 실행하여 새 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
#### 병합 게시의 기존 아티클에 대한 스키마 옵션을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)합니다. **@publication** 에 아티클이 속한 게시의 이름을 지정하고 **@article**에 아티클의 이름을 지정합니다. 값은 **schema_option** 결과 집합의 열입니다.  
  
2.  실행 한 [& (비트 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 단계 1과 원하는 스키마에서 값을 사용 하 여 작업 옵션의 옵션이 설정 되어 있는지 확인 하는 값입니다.  
  
    -   결과가 **0**이면 옵션이 설정되지 않은 것입니다.  
  
    -   결과가 옵션 값이면 옵션이 이미 설정된 것입니다.  
  
3.  옵션을 설정 하지 않으면 경우 실행 하는 [| (비트 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 1 단계의 값과 원하는 스키마 옵션 값을 사용 하는 작업입니다.  
  
4.  게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 문서에 속한 게시의 이름을 지정 **@publication**, 아티클 이름 **@article**, 값 **schema_option** 에 대 한 **@property**, 3 단계의 16 진수 결과 **@value**합니다.  
  
5.  스냅숏 에이전트를 실행하여 새 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
## 참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [트랜잭션 복제를 위한 아티클 옵션](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  