---
title: 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1abc4a39fd9e667374383302f15a9246ea2c7cd0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213133"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하는 방법에 대해 설명합니다.  
  
 기본적으로 트랜잭션 복제는 각 아티클에 대한 저장 프로시저 집합을 사용하여 변경 내용을 구독자에 전파합니다. 이 프로시저는 사용자 지정 프로시저로 대체할 수 있습니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
-   **트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   복제에서 생성된 스냅숏 파일을 편집할 때는 주의해야 합니다. 사용자 지정 저장 프로시저의 사용자 지정 논리를 테스트하고 지원해야 합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 사용자 지정 논리에 대한 지원을 제공하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사와 **게시 속성 - \<게시>** 대화 상자에서 사용 가능한 **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에서 전파 방법을 지정합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](create-a-publication.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-the-propagation-method"></a>전파 방법을 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택하고 **아티클 속성**을 클릭합니다.  
  
2.  **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에 있는 **문 배달** 섹션에서 **INSERT 배달 형식**, **UPDATE 배달 형식** 및 **DELETE 배달 형식** 메뉴를 사용하여 각 작업의 전파 방법을 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="to-generate-and-use-custom-stored-procedures"></a>사용자 지정 저장 프로시저를 생성하여 사용하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택하고 **아티클 속성**을 클릭합니다.  
  
2.  **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
     **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에 있는 **문 배달** 섹션의 해당 배달 형식 메뉴(**INSERT 배달 형식**, **UPDATE 배달 형식** 또는 **DELETE 배달 형식**)에서 CALL 구문을 선택한 다음 **INSERT 저장 프로시저**, **DELETE 저장 프로시저** 또는 **UPDATE 저장 프로시저**에 사용할 프로시저 이름을 입력합니다. CALL 구문에 대한 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)에서 "저장 프로시저 호출 구문" 섹션을 참조하세요.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
5.  게시에 대한 스냅숏이 생성되면 이전 단계에서 지정한 프로시저가 포함됩니다. 이 프로시저는 지정한 CALL 구문을 사용하지만 복제에 사용되는 기본 논리를 포함합니다.  
  
     스냅숏이 생성된 후 이 아티클이 속해 있는 게시의 스냅숏 폴더로 이동하여 아티클과 동일한 이름을 가진 **.sch** 파일을 찾습니다. 메모장이나 다른 텍스트 편집기를 사용하여 이 파일을 열고 삽입, 업데이트 또는 삭제 저장 프로시저에 대한 CREATE PROCEDURE 명령을 찾은 후 프로시저 정의를 편집하여 데이터 변경 내용 전파에 대한 사용자 지정 논리를 제공합니다. 스냅숏이 다시 생성되면 사용자 지정 프로시저를 다시 만들어야 합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 트랜잭션 복제를 사용하면 게시자에서 구독자로 변경 내용을 전파하는 방법을 제어할 수 있습니다. 이 전파 방법은 아티클을 만들 때 프로그래밍 방식으로 설정될 수 있으며 나중에 복제 저장 프로시저에서 변경할 수도 있습니다.  
  
> [!NOTE]  
>  게시된 데이터 행에서 수행되는 각 DML(데이터 조작 언어) 작업 유형(삽입, 업데이트 또는 삭제)에 따라 다른 전파 방법을 지정할 수 있습니다.  
  
 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>Transact-SQL 명령을 사용하여 데이터 변경 내용을 전파하는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행합니다. **@publication**에 아티클이 속한 게시 이름, **@article**에 아티클 이름, **@source_object**에 게시할 데이터베이스 개체를 지정하고 다음 매개 변수 중 하나 이상에 **SQL** 값을 지정합니다.  
  
    -   **@ins_cmd** - [INSERT](/sql/t-sql/statements/insert-transact-sql) 명령의 복제를 제어합니다.  
  
    -   **@upd_cmd** - [UPDATE](/sql/t-sql/queries/update-transact-sql) 명령의 복제를 제어합니다.  
  
    -   **@del_cmd** - [DELETE](/sql/t-sql/statements/delete-transact-sql) 명령의 복제를 제어합니다.  
  
    > [!NOTE]  
    >  위 매개 변수 중 하나에 **SQL** 값을 지정하면 해당 유형의 명령이 적절한 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령으로 구독자에 복제됩니다.  
  
     자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>데이터 변경 내용을 전파하지 않는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행합니다. **@publication**에 아티클이 속한 게시 이름, **@article**에 아티클 이름, **@source_object**에 게시할 데이터베이스 개체를 지정하고 다음 매개 변수 중 하나 이상에 **NONE** 값을 지정합니다.  
  
    -   **@ins_cmd** - [INSERT](/sql/t-sql/statements/insert-transact-sql) 명령의 복제를 제어합니다.  
  
    -   **@upd_cmd** - [UPDATE](/sql/t-sql/queries/update-transact-sql) 명령의 복제를 제어합니다.  
  
    -   **@del_cmd** - [DELETE](/sql/t-sql/statements/delete-transact-sql) 명령의 복제를 제어합니다.  
  
    > [!NOTE]  
    >  위 매개 변수 중 하나에 **NONE** 값을 지정하면 해당 유형의 명령이 구독자에 복제되지 않습니다.  
  
     자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>사용자가 수정한 사용자 지정 저장 프로시저를 포함하는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행합니다. **@publication**에 아티클이 속한 게시 이름, **@article**에 아티클 이름, **@source_object**에 게시할 데이터베이스 개체, **0x02** 값(사용자 지정 저장 프로시저의 자동 생성 설정)을 포함하는 **@schema_option** 비트마스크에 값을 지정하고 다음 매개 변수 중 하나 이상을 지정합니다.  
  
    -   **@ins_cmd** - **CALL sp_MSins_* article_name*** 값을 지정합니다. 여기서 ***article_name***은 **@article**에 지정된 값입니다.  
  
    -   **@del_cmd** - **CALL sp_MSdel_*article_name*** 또는 **XCALL sp_MSdel_* article_name*** 값을 지정합니다. 여기서 ***article_name***은 **@article**에 지정된 값입니다.  
  
    -   **@upd_cmd** - **SCALL sp_MSupd_* article_name***, **CALL sp_MSupd_* article_name***, **XCALL sp_MSupd_* article_name*** 또는 **MCALL sp_MSupd_* article_name*** 값을 지정합니다. 여기서 ***article_name***은 **@article**에서 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하는 방법에 대해 설명합니다.  
  
    > [!NOTE]  
    >  위 명령 매개 변수마다 복제 시 생성되는 저장 프로시저의 이름을 고유하게 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  CALL, SCALL, XCALL 및 MCALL 구문에 대한 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
     자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
2.  스냅숏이 생성된 후 이 아티클이 속해 있는 게시의 스냅숏 폴더로 이동하여 아티클과 동일한 이름을 가진 **.sch** 파일을 찾습니다. Notepad.exe를 사용하여 이 파일을 열고 삽입, 업데이트 또는 삭제 저장 프로시저에 대한 CREATE PROCEDURE 명령을 찾은 후 프로시저 정의를 편집하여 데이터 변경 내용 전파에 대한 사용자 지정 논리를 제공합니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>데이터 변경 내용을 전파하기 위해 사용자 지정 저장 프로시저의 사용자 지정 스크립팅을 포함하는 아티클을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행합니다. **@publication**에 아티클이 속한 게시 이름, **@article**에 아티클 이름, **@source_object**에 게시할 데이터베이스 개체, **0x02** 값(사용자 지정 저장 프로시저의 자동 생성 설정)을 포함하는 **@schema_option** 비트마스크에 값을 지정하고 다음 매개 변수 중 하나 이상을 지정합니다.  
  
    -   **@ins_cmd** - **CALL sp_MSins_* article_name*** 값을 지정합니다. 여기서 ***article_name***은 **@article**에 지정된 값입니다.  
  
    -   **@del_cmd** - **CALL sp_MSdel_*article_name*** 또는 **XCALL sp_MSdel_* article_name*** 값을 지정합니다. 여기서 ***article_name***은 **@article**에 지정된 값입니다.  
  
    -   **@upd_cmd** - **SCALL sp_MSupd_* article_name***, **CALL sp_MSupd_* article_name***, **XCALL sp_MSupd_* article_name***, **MCALL sp_MSupd_* article_name*** 값을 지정합니다. 여기서 ***article_name***은 **@article**에서 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하는 방법에 대해 설명합니다.  
  
    > [!NOTE]  
    >  위 명령 매개 변수마다 복제 시 생성되는 저장 프로시저의 이름을 고유하게 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  CALL, SCALL, XCALL 및 MCALL 구문에 대한 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
     자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 [ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql) 문을 사용하여 삽입, 업데이트 및 삭제 사용자 지정 저장 프로시저에 대한 [CREATE PROCEDURE](/sql/relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql) 스크립트를 반환하도록 [sp_scriptpublicationcustomprocs](/sql/t-sql/statements/create-procedure-transact-sql) 를 편집하면 합니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>기존 아티클에 대한 변경 내용 전파 방법을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)을 실행합니다. **@publication**, **@article**, **@property**에 **ins_cmd**, **upd_cmd** 또는 **del_cmd** 값, **@value**에 적절한 전파 방법을 지정합니다.  
  
2.  변경하려는 각 전파 방법에 대해 1단계를 반복합니다.  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [게시 및 아티클 만들기, 수정 및 삭제&#40;복제&#41;](create-modify-and-delete-publications-and-articles-replication.md)  
  
  
