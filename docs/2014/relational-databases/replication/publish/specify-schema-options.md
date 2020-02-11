---
title: 스키마 옵션 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: e6826d28ec923de221e94b985b740a172bdaa7d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73882161"
---
# <a name="specify-schema-options"></a>스키마 옵션 지정
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
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시가 만들어진 후 스키마 옵션을 변경하면 새 스냅샷을 생성해야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   스키마 옵션의 전체 목록은 [transact-sql&#41;&#40;sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 의 ** \@schema_option** 매개 변수를 참조 하 고 sp_addmergearticle [&#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 참조 하십시오.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 제약 조건 및 트리거를 구독자에 복사할지 여부 등의 스키마 옵션을 **아티클 속성-** Article> **대화 상자의 \<속성** 탭에 지정합니다. 이 탭은 새 게시 마법사 및 **게시 속성 - \<게시>** 대화 상자에서 사용할 수 있습니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](create-a-publication.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-schema-options"></a>스키마 옵션을 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 아티클을 선택하고 **아티클 속성**을 클릭합니다.  
  
2.  스키마 옵션 변경 내용을 적용할 아티클을 선택합니다.  
  
    -   **선택한 \<ObjectType> 아티클 속성 설정**을 클릭하여 **아티클 속성 - \<ObjectName>** 대화 상자를 엽니다. 이 대화 상자에서 변경한 속성은 **아티클** 페이지의 개체 창에 강조 표시된 개체에만 적용됩니다.  
  
    -   **모든 \<ObjectType> 아티클 속성 설정**을 클릭하여 **모든 \<ObjectType> 아티클의 속성** 대화 상자를 엽니다. 이 대화 상자에서 변경한 속성은 게시용으로 아직 선택하지 않은 개체를 비롯하여 **아티클** 페이지의 개체 창에서 해당 형식을 갖는 모든 개체에 적용됩니다.  
  
        > [!NOTE]  
        >  **모든 \<ObjectType> 아티클의 속성** 대화 상자에서 변경한 속성은 이전에 **아티클 속성 - \<ObjectName>** 대화 상자에서 지정한 내용을 재정의합니다. 예를 들어 특정 개체 유형의 모든 아티클에 대해 여러 기본값을 설정하고 개별 개체에 대해 일부 속성도 설정하려면 먼저 모든 아티클의 기본값을 설정합니다. 그런 다음 개별 개체에 대해 속성을 설정합니다.  
  
3.  **아티클 속성 -** 아티클> **대화 상자의**속성**탭에 있는**구독자에게 개체 및 설정 복사 **및 \<대상 개체** 섹션은 옵션에 대한 값을 지정합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
5.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 스키마 옵션은 하나 이상의 옵션에 대한 [|(비트 OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 결과인 16진수 값으로 지정됩니다. 자세한 내용은 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 및 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 참조하세요.  
  
> [!NOTE]  
>  비트 연산을 수행하기 전에 스키마 옵션 값을 **binary** 에서 **int** 로 변환해야 합니다. 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)를 참조하세요.  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 대한 아티클을 정의할 때 스키마 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행합니다. ** \@게시**에 대해 아티클이 속한 게시의 이름, ** \@아티클**용 아티클의 이름, ** \@source_object**에 대해 게시 되는 데이터베이스 개체, ** \@형식**에 대 한 데이터베이스 개체의 유형 및 |를 지정 합니다. [ (비트 or)](/sql/t-sql/language-elements/bitwise-or-transact-sql) ** \@schema_option**에 대 한 하나 이상의 스키마 옵션의 결과입니다. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>병합 게시에 대한 아티클을 정의할 때 스키마 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행합니다. ** \@게시**에 대해 아티클이 속한 게시의 이름 ** \@, 아티클의 아티클 이름,** ** \@source_object**에 대해 게시 되는 데이터베이스 개체 및 [| (비트 or)](/sql/t-sql/language-elements/bitwise-or-transact-sql) ** \@schema_option**에 대 한 하나 이상의 스키마 옵션의 결과입니다. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시의 기존 아티클에 대한 스키마 옵션을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)을 실행합니다. ** \@게시** 에 대해 아티클이 속한 게시의 이름과 ** \@아티클에**대 한 아티클 이름을 지정 합니다. 결과 집합에서 **schema_option** 열의 값을 확인합니다.  
  
2.  옵션이 설정되었는지 판단하기 위해 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [&(비트 AND)](/sql/t-sql/language-elements/bitwise-and-transact-sql) 연산을 실행합니다.  
  
    -   결과가 **0**이면 옵션이 설정되지 않은 것입니다.  
  
    -   결과가 옵션 값이면 옵션이 이미 설정된 것입니다.  
  
3.  옵션이 설정되지 않은 경우 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [|(비트 OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 연산을 실행합니다.  
  
4.  게시 데이터베이스의 게시자에서 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)을 실행합니다. ** \@게시**에 대해 아티클이 속한 게시의 이름, ** \@아티클의**아티클 이름, ** \@속성**에 **schema_option** 값, ** \@값**에 3 단계의 16 진수 결과를 지정 합니다.  
  
5.  스냅샷 에이전트를 실행하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>병합 게시의 기존 아티클에 대한 스키마 옵션을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)을 실행합니다. ** \@게시** 에 대해 아티클이 속한 게시의 이름과 ** \@아티클에**대 한 아티클 이름을 지정 합니다. 결과 집합에서 **schema_option** 열의 값을 확인합니다.  
  
2.  옵션이 설정되었는지 판단하기 위해 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [&(비트 AND)](/sql/t-sql/language-elements/bitwise-and-transact-sql) 연산을 실행합니다.  
  
    -   결과가 **0**이면 옵션이 설정되지 않은 것입니다.  
  
    -   결과가 옵션 값이면 옵션이 이미 설정된 것입니다.  
  
3.  옵션이 설정되지 않은 경우 1단계의 값과 원하는 스키마 옵션 값을 사용하여 [|(비트 OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 연산을 실행합니다.  
  
4.  게시 데이터베이스의 게시자에서 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 실행합니다. ** \@게시**에 대해 아티클이 속한 게시의 이름, ** \@아티클의**아티클 이름, ** \@속성**에 **schema_option** 값, ** \@값**에 3 단계의 16 진수 결과를 지정 합니다.  
  
5.  스냅샷 에이전트를 실행하여 새 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](publish-data-and-database-objects.md)   
 [Article Options for Transactional Replication](../transactional/article-options-for-transactional-replication.md)  
  
  
