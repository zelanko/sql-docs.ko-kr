---
title: "Oracle 게시자에 대한 데이터 형식 매핑 지정 | Microsoft Docs"
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
  - "Oracle 게시 [SQL Server 복제], 데이터 형식 매핑"
  - "데이터 형식 [SQL Server 복제], Oracle 게시"
  - "데이터 형식 매핑 [SQL Server 복제]"
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Oracle 게시자에 대한 데이터 형식 매핑 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]의 Oracle 게시자에 대한 데이터 형식 매핑을 지정하는 방법에 대해 설명합니다. Oracle 게시자에 대해 기본 데이터 형식 매핑 집합이 제공되지만 특정 게시에 대해 다른 매핑을 지정해야 할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 Oracle게시자에 대한 데이터 형식 매핑을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 데이터 형식 매핑을 지정는 **데이터 매핑** 탭은 **아티클 속성-\< 아티클>** 대화 상자입니다. 사용할 수는 **문서** 새 게시 마법사의 페이지 및 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [Oracle 데이터베이스에서 게시를 만들](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 데이터 형식 매핑을 지정하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택한 다음 **아티클 속성**합니다.  
  
2.  **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **데이터 매핑** 탭은 **아티클 속성-\< 아티클>** 에서 매핑 선택 대화 상자는 **구독자 데이터 형식** 열:  
  
    -   하나의 매핑만 사용할 수 있는 데이터 형식의 경우 속성 표의 열이 읽기 전용입니다.  
  
    -   일부 형식의 경우 두 개 이상의 매핑을 선택할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 는 응용 프로그램에 다른 매핑이 필요 하지 않는 한 기본 매핑을 사용할 것을 권장합니다. 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 사용자 지정 데이터 형식 매핑을 프로그래밍 방식으로 지정할 수 있습니다. 데이터 형식을 매핑할 때 간에 사용 되는 기본 매핑을 설정할 수도 있습니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 비-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 관리 시스템 (DBMS). 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
#### Oracle 게시에 속한 아티클을 작성할 때 사용자 지정 데이터 형식 매핑을 정의하려면  
  
1.  Oracle 게시가 아직 없는 경우 만듭니다.  
  
2.  배포자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 값을 지정 **0** 에 대 한 **@use_default_datatypes**합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  배포자에서 실행 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) 게시 된 문서에서 열에 대 한 기존 매핑을 볼 수 있습니다.  
  
4.  배포자에서 실행 [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)합니다. **@publisher**에 Oracle 게시자의 이름을 지정하고 **@publication**, **@article**및 **@column** 을 지정하여 게시된 열을 정의합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @type **에 매핑할**데이터 형식의 이름을 지정하고 해당되는 경우 **@length**, **@precision**및 **@scale**을 지정합니다.  
  
5.  배포자에서 실행 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)합니다. 이렇게 하면 Oracle 게시에서 스냅숏을 생성하는 데 사용되는 뷰가 만들어집니다.  
  
#### 매핑을 데이터 형식에 대한 기본 매핑으로 지정하려면  
  
1.  (선택 사항) 모든 데이터베이스의 배포자에서 실행 [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)합니다. 지정 **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**, 원본 DBMS를 식별 하는 데 필요한 기타 매개 변수입니다. 대상 DBMS의 현재 매핑된 데이터 형식에 대한 정보는 출력 매개 변수를 사용하여 반환됩니다.  
  
2.  (선택 사항) 모든 데이터베이스의 배포자에서 실행 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)합니다. 지정 **@source_dbms** 결과 집합을 필터링 하는 데 필요한 다른 매개 변수입니다. 값을 확인 **mapping_id** 결과에서 원하는 매핑을 설정 합니다.  
  
3.  모든 데이터베이스의 배포자에서 실행 [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)합니다.  
  
    -   원하는 값을 알고 있으면 **mapping_id** 에 대해 지정 2 단계에서 얻은, **@mapping_id**합니다.  
  
    -   알 수 없는 경우는 **mapping_id**, 매개 변수를 지정 **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**, 기존 매핑을 식별 하는 데 필요한 기타 매개 변수입니다.  
  
#### 지정된 Oracle 데이터 형식에 대한 유효한 데이터 형식을 찾으려면  
  
1.  모든 데이터베이스의 배포자에서 실행 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)합니다. 값을 지정 **ORACLE** 에 대 한 **@source_dbms** 결과 집합을 필터링 하는 데 필요한 다른 매개 변수입니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는에 매핑되도록 번호의 Oracle 데이터 형식이 있는 열을 변경 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 **숫자**(38, 38)의 기본 데이터 형식을 대신 **float**합니다.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 다음 쿼리 예에서는 Oracle 9 데이터 형식 **CHAR**에 대한 기본 및 대체 매핑을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 다음 쿼리 예에서는 소수 자릿수 또는 전체 자릿수 없이 지정된 경우 Oracle 9 데이터 형식 **NUMBER** 에 대한 기본 매핑을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## 참고 항목  
 [Oracle 게시자에 대한 데이터 형식 매핑](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [다른 유형의 데이터베이스 복제](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  