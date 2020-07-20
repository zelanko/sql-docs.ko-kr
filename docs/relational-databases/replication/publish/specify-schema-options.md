---
title: SQL Server 복제의 스키마 옵션 지정 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a035d525492c1a99e7df28a13fcbd26a2fbbbdd2
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86159531"
---
# <a name="specify-schema-options-for-sql-server-replication"></a>SQL Server 복제의 스키마 옵션 지정
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 스키마 옵션을 지정하는 방법에 대해 설명합니다. 테이블 또는 뷰를 게시하는 경우 게시된 개체에 대해 복제되는 개체 작성 옵션을 제어할 수 있습니다. 아티클을 만들 때 이 옵션을 설정할 수 있으며 나중에 이 옵션을 변경할 수도 있습니다. 아티클에 대해 이 옵션을 명시적으로 지정하지 않으면 기본 옵션 집합이 정의됩니다.  
  
> [!NOTE]  
>  복제 저장 프로시저를 사용할 때의 기본 스키마 옵션은 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용하여 아티클을 추가할 때의 기본 옵션과 다를 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **스키마 옵션을 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   게시가 만들어진 후 스키마 옵션을 변경하면 새 스냅샷을 생성해야 합니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   스키마 옵션의 전체 목록은 [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 및 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)의 `@schema_option` 매개 변수를 참조하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 제약 조건 및 트리거를 구독자에 복사할지 여부 등의 스키마 옵션을 **아티클 속성-\<Article>** 대화 상자의 **속성** 탭에 지정합니다. 이 탭은 새 게시 마법사 및 **게시 속성 - \<Publication>** 대화 상자에서 사용할 수 있습니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-schema-options"></a>스키마 옵션을 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<Publication>** 대화 상자에서 아티클을 선택하고 **아티클 속성**을 클릭합니다.  
  
2.  스키마 옵션 변경 내용을 적용할 아티클을 선택합니다.  
  
    -   **선택한 \<ObjectType> 아티클 속성 설정**을 클릭하여 **아티클 속성 - \<ObjectName>** 대화 상자를 엽니다. 이 대화 상자에서 변경한 속성은 **아티클** 페이지의 개체 창에 강조 표시된 개체에만 적용됩니다.  
  
    -   **모든 \<ObjectType> 아티클 속성 설정**을 클릭하여 **모든 \<ObjectType> 아티클 속성** 대화 상자를 엽니다. 이 대화 상자에서 변경한 속성은 **아티클** 페이지의 개체 창에서 해당 형식을 갖는 모든 개체(아직 게시용으로 선택하지 않은 개체 포함)에 적용됩니다.  
  
        > [!NOTE]  
        >  **모든 \<ObjectType> 아티클의 속성** 대화 상자에서 변경한 속성은 이전에 **아티클 속성 - \<ObjectName>** 대화 상자에서 지정한 내용을 재정의합니다. 예를 들어 특정 개체 유형의 모든 아티클에 대해 여러 기본값을 설정하고 개별 개체에 대해 일부 속성도 설정하려면 먼저 모든 아티클의 기본값을 설정합니다. 그런 다음 개별 개체에 대해 속성을 설정합니다.  
  
3.  **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에 있는 **구독자에 개체 및 설정 복사** 및 **대상 개체** 섹션에서 옵션에 대한 값을 지정합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
5.  **게시 속성 - \<Publication>** 대화 상자에서 **확인**을 클릭하여 저장하고 대화 상자를 닫습니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 스키마 옵션은 하나 이상의 옵션에 대한 [|(비트 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 결과인 16진수 값으로 지정됩니다. 자세한 내용은 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 및 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  비트 연산을 수행하기 전에 스키마 옵션 값을 **binary** 에서 **int** 로 변환해야 합니다. 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 대한 아티클을 정의할 때 스키마 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름, `@source_object`에 게시되는 데이터베이스 개체, `@type`에 데이터베이스 개체 유형, `@schema_option`에 하나 이상 스키마 옵션의 [|(비트 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 결과를 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>병합 게시에 대한 아티클을 정의할 때 스키마 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름, `@source_object`에 게시되는 데이터베이스 개체, `@schema_option`에 하나 이상 스키마 옵션의 [|(비트 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 결과를 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시의 기존 아티클에 대한 스키마 옵션을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름을 지정합니다. 결과 집합에서 `schema_option` 열의 값을 확인합니다.  
  
2.  옵션이 설정되었는지 판단하기 위해 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [&(비트 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 연산을 실행합니다.  
  
    -   결과가 **0**이면 옵션이 설정되지 않은 것입니다.  
  
    -   결과가 옵션 값이면 옵션이 이미 설정된 것입니다.  
  
3.  옵션이 설정되지 않은 경우 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [|(비트 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 연산을 실행합니다.  
  
4.  게시 데이터베이스의 게시자에서 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름, `@property`에 `schema_option` 값, `@value`에 3단계의 16진수 결과를 지정합니다.  
  
5.  스냅샷 에이전트를 실행하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>병합 게시의 기존 아티클에 대한 스키마 옵션을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름을 지정합니다. 결과 집합에서 **schema_option** 열의 값을 확인합니다.  
  
2.  옵션이 설정되었는지 판단하기 위해 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [&(비트 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 연산을 실행합니다.  
  
    -   결과가 **0**이면 옵션이 설정되지 않은 것입니다.  
  
    -   결과가 옵션 값이면 옵션이 이미 설정된 것입니다.  
  
3.  옵션이 설정되지 않은 경우 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [|(비트 OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) 연산을 실행합니다.  
  
4.  게시 데이터베이스의 게시자에서 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름, `@property`에 `schema_option` 값, `@value`에 3단계의 16진수 결과를 지정합니다.  
  
5.  스냅샷 에이전트를 실행하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
