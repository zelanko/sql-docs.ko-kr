---
title: "트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정 | Microsoft Docs"
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
  - "트랜잭션 복제, 전파 방법"
  - "데이터 변경 내용 전파 [SQL Server 복제]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하는 방법에 대해 설명합니다.  
  
 기본적으로 트랜잭션 복제는 각 아티클에 대한 저장 프로시저 집합을 사용하여 변경 내용을 구독자에 전파합니다. 이 프로시저는 사용자 지정 프로시저로 대체할 수 있습니다. 자세한 내용은 참조 [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   복제에서 생성된 스냅숏 파일을 편집할 때는 주의해야 합니다. 사용자 지정 저장 프로시저의 사용자 지정 논리를 테스트하고 지원해야 합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 사용자 지정 논리에 대한 지원을 제공하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 전파 방법을 지정는 **속성** 탭은 **아티클 속성-\< 문서>** 새 게시 마법사에서 사용할 수 있는 대화 상자 및 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 전파 방법을 지정하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택한 다음 **아티클 속성**합니다.  
  
2.  **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자는 **문 배달** 섹션에서 사용 하 여 각 작업에 대 한 전파 방법을 지정는 **INSERT 배달 형식**, **UPDATE 배달 형식**, 및 **DELETE 배달 형식** 메뉴.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 사용자 지정 저장 프로시저를 생성하여 사용하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택한 다음 **아티클 속성**합니다.  
  
2.  **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
     에 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자는 **문 배달** 섹션에서 적절 한 배포 서식 메뉴에서 호출 구문을 선택 (**INSERT 배달 형식**, **UPDATE 배달 형식**, 또는 **DELETE 배달 형식**), 다음에서 사용 하는 프로시저의 이름을 입력 하 고 **INSERT 저장 프로시저**, **DELETE 저장 프로시저**, 또는 **업데이트 저장 프로시저**합니다. 호출 구문에 대 한 자세한 내용은 "저장된 프로시저 호출 구문" 섹션을 참조 [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
5.  게시에 대한 스냅숏이 생성되면 이전 단계에서 지정한 프로시저가 포함됩니다. 이 프로시저는 지정한 CALL 구문을 사용하지만 복제에 사용되는 기본 논리를 포함합니다.  
  
     스냅숏이 생성된 후 이 아티클이 속해 있는 게시의 스냅숏 폴더로 이동하여 아티클과 동일한 이름을 가진 **.sch** 파일을 찾습니다. 메모장이나 다른 텍스트 편집기를 사용하여 이 파일을 열고 삽입, 업데이트 또는 삭제 저장 프로시저에 대한 CREATE PROCEDURE 명령을 찾은 후 프로시저 정의를 편집하여 데이터 변경 내용 전파에 대한 사용자 지정 논리를 제공합니다. 스냅숏이 다시 생성되면 사용자 지정 프로시저를 다시 만들어야 합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 트랜잭션 복제를 사용하면 게시자에서 구독자로 변경 내용을 전파하는 방법을 제어할 수 있습니다. 이 전파 방법은 아티클을 만들 때 프로그래밍 방식으로 설정될 수 있으며 나중에 복제 저장 프로시저에서 변경할 수도 있습니다.  
  
> [!NOTE]  
>  게시된 데이터 행에서 수행되는 각 DML(데이터 조작 언어) 작업 유형(삽입, 업데이트 또는 삭제)에 따라 다른 전파 방법을 지정할 수 있습니다.  
  
 자세한 내용은 참조 [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
#### Transact-SQL 명령을 사용하여 데이터 변경 내용을 전파하는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체 **@source_object**, 및의 값 **SQL** 최소한 하나에 대해 다음 매개 변수 중:  
  
    -   **@ins_cmd** -복제를 제어 [삽입](../../../t-sql/statements/insert-transact-sql.md) 명령입니다.  
  
    -   **@upd_cmd** -복제를 제어 [업데이트](../../../t-sql/queries/update-transact-sql.md) 명령입니다.  
  
    -   **@del_cmd** -복제를 제어 [삭제](../../../t-sql/statements/delete-transact-sql.md) 명령입니다.  
  
    > [!NOTE]  
    >  값을 지정 하면 **SQL** 위의 매개 변수 중 하나에 대 한 해당 유형의 명령이 적절 한 형식으로 구독자에 복제 됩니다 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령입니다.  
  
     자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### 데이터 변경 내용을 전파하지 않는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체 **@source_object**, 및의 값 **NONE** 최소한 하나에 대해 다음 매개 변수 중:  
  
    -   **@ins_cmd** -복제를 제어 [삽입](../../../t-sql/statements/insert-transact-sql.md) 명령입니다.  
  
    -   **@upd_cmd** -복제를 제어 [업데이트](../../../t-sql/queries/update-transact-sql.md) 명령입니다.  
  
    -   **@del_cmd** -복제를 제어 [삭제](../../../t-sql/statements/delete-transact-sql.md) 명령입니다.  
  
    > [!NOTE]  
    >  값을 지정 하면 **NONE** 위의 매개 변수 중 하나에 대 한 해당 유형의 명령이 복제 되지 않는다는 구독자에 있습니다.  
  
     자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### 사용자가 수정한 사용자 지정 저장 프로시저를 포함하는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체 **@source_object**, 에 대 한 값은 **@schema_option** 값을 포함 하는 비트 마스크 **0x02** (사용자 지정 저장된 프로시저의 자동 생성할 수 있도록), 및 다음 매개 변수 중 적어도 하나:  
  
    -   **@ins_cmd** -값을 지정 **CALL sp_MSins_*article_name***, 여기서 ***article_name*** 값에 대 한 지정 **@article** 합니다.  
  
    -   **@del_cmd** -값을 지정 **호출 sp_MSdel_*article_name*** 또는 **XCALL sp_MSdel_*article_name***, 여기서 ***article_name*** 값에 대 한 지정 **@article** 합니다.  
  
    -   **@upd_cmd** -값을 지정 **SCALL sp_MSupd_*article_name***, **호출 sp_MSupd_*article_name***, **XCALL sp_MSupd_*article_name***, 또는 **MCALL sp_MSupd_*article_name***, 여기서 ***article_name*** 값에 대 한 지정 **@article** 합니다.  
  
    > [!NOTE]  
    >  위 명령 매개 변수마다 복제 시 생성되는 저장 프로시저의 이름을 고유하게 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  통화, SCALL, XCALL 및 MCALL 구문에 대 한 자세한 내용은 참조 하십시오. [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
     자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  스냅숏이 생성된 후 이 아티클이 속해 있는 게시의 스냅숏 폴더로 이동하여 아티클과 동일한 이름을 가진 **.sch** 파일을 찾습니다. Notepad.exe를 사용하여 이 파일을 열고 삽입, 업데이트 또는 삭제 저장 프로시저에 대한 CREATE PROCEDURE 명령을 찾은 후 프로시저 정의를 편집하여 데이터 변경 내용 전파에 대한 사용자 지정 논리를 제공합니다. 자세한 내용은 참조 [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
#### 데이터 변경 내용을 전파하기 위해 사용자 지정 저장 프로시저의 사용자 지정 스크립팅을 포함하는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체 **@source_object**, 에 대 한 값은 **@schema_option** 값을 포함 하는 비트 마스크 **0x02** (사용자 지정 저장된 프로시저의 자동 생성할 수 있도록), 및 다음 매개 변수 중 적어도 하나:  
  
    -   **@ins_cmd** -값을 지정 **CALL sp_MSins_*article_name***, 여기서 ***article_name*** 값에 대 한 지정 **@article** 합니다.  
  
    -   **@del_cmd** -값을 지정 **호출 sp_MSdel_*article_name*** 또는 **XCALL sp_MSdel_*article_name***, 여기서 ***article_name*** 값에 대 한 지정 **@article** 합니다.  
  
    -   **@upd_cmd** -값을 지정 **SCALL sp_MSupd_*article_name***, **호출 sp_MSupd_*article_name***, **XCALL sp_MSupd_*article_name***, **MCALL sp_MSupd_*article_name***, 여기서 ***article_name*** 값에 대 한 지정 **@article** 합니다.  
  
    > [!NOTE]  
    >  위 명령 매개 변수마다 복제 시 생성되는 저장 프로시저의 이름을 고유하게 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  통화, SCALL, XCALL 및 MCALL 구문에 대 한 자세한 내용은 참조 하십시오. [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
     자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 사용 하 여는 [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) 편집할 문을 [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) 반환 되도록는 [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) 삽입, 업데이트 및 삭제 사용자 지정 저장 프로시저에 대 한 스크립트입니다. 자세한 내용은 참조 [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
#### 기존 아티클에 대한 변경 내용 전파 방법을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)합니다. 지정 **@publication**, **@article**, 값이 **ins_cmd**, **upd_cmd**, 또는 **del_cmd** 에 대 한 **@property**, 및에 대 한 적절 한 전파 방법 **@value**합니다.  
  
2.  변경하려는 각 전파 방법에 대해 1단계를 반복합니다.  
  
## 참고 항목  
 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [만들기, 수정 및 게시 하 고 문서 및 #40;를 삭제 합니다. 복제 및 #41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  