---
title: Oracle 게시자에 대한 데이터 형식 매핑 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26331e3864940b9c7f2a2588e3d3cbfa9944c900
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060351"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Oracle 게시자에 대한 데이터 형식 매핑 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]의 Oracle 게시자에 대한 데이터 형식 매핑을 지정하는 방법에 대해 설명합니다. Oracle 게시자에 대해 기본 데이터 형식 매핑 집합이 제공되지만 특정 게시에 대해 다른 매핑을 지정해야 할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 Oracle게시자에 대한 데이터 형식 매핑을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **아티클 속성- \<Article> ** 대화 상자의 **데이터 매핑** 탭에서 데이터 형식 매핑을 지정 합니다. 이는 새 게시 마법사의 **아티클** 페이지 및 **게시 속성- \<Publication> ** 대화 상자에서 사용할 수 있습니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [Oracle 데이터베이스에서 게시 만들기](create-a-publication-from-an-oracle-database.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-a-data-type-mapping"></a>데이터 형식 매핑을 지정하려면  
  
1.  새 게시 마법사 또는 **게시 속성- \<Publication> ** 대화 상자의 **아티클** 페이지에서 테이블을 선택한 다음 **아티클 속성**을 클릭 합니다.  
  
2.  **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성- \<Article> ** 대화 상자의 **데이터 매핑** 탭에서 **구독자 데이터 형식** 열의 매핑을 선택 합니다.  
  
    -   하나의 매핑만 사용할 수 있는 데이터 형식의 경우 속성 표의 열이 읽기 전용입니다.  
  
    -   일부 형식의 경우 두 개 이상의 매핑을 선택할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 는 애플리케이션에 다른 매핑이 필요 하지 않는 한 기본 매핑을 사용할 것을 권장합니다. 자세한 내용은 [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 사용자 지정 데이터 형식 매핑을 프로그래밍 방식으로 지정할 수 있습니다. 또한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DBMS (데이터베이스 관리 시스템) 간에 데이터 형식을 매핑할 때 사용 되는 기본 매핑을 설정할 수 있습니다. 자세한 내용은 [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Oracle 게시에 속한 아티클을 작성할 때 사용자 지정 데이터 형식 매핑을 정의하려면  
  
1.  Oracle 게시가 아직 없는 경우 만듭니다.  
  
2.  배포자에서 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 실행합니다. **\@use_default_datatypes**에 **0** 값을 지정합니다. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
3.  배포자에서 [sp_helparticlecolumns](/sql/relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql) 를 실행하여 게시된 아티클의 열에 대한 기존 매핑을 확인합니다.  
  
4.  배포자에서 [sp_changearticlecolumndatatype](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql)을 실행합니다. 게시 된 열을 정의 하는 ** \@ 게시**, ** \@ 아티클**및 ** \@ 열** 뿐만 아니라 ** \@ 게시자**에 대 한 Oracle 게시자의 이름을 지정 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]해당 하는 경우 ** \@ 형식**에 대해 매핑할 데이터 형식의 이름을 지정 하 고 ** \@ 길이**, ** \@ 전체 자릿수**및 ** \@ 소수 자릿수**를 지정 합니다.  
  
5.  배포자에서 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)를 실행합니다. 이렇게 하면 Oracle 게시에서 스냅샷을 생성하는 데 사용되는 뷰가 만들어집니다.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>매핑을 데이터 형식에 대한 기본 매핑으로 지정하려면  
  
1.  (옵션) 데이터베이스의 배포자에서 [sp_getdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql)을 실행합니다. ** \@ Source_dbms**, ** \@ source_type**, ** \@ destination_dbms**, ** \@ destination_version**및 원본 dbms를 식별 하는 데 필요한 기타 매개 변수를 지정 합니다. 대상 DBMS의 현재 매핑된 데이터 형식에 대한 정보는 출력 매개 변수를 사용하여 반환됩니다.  
  
2.  (옵션) 데이터베이스의 배포자에서 [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql)을 실행합니다. 결과 집합을 필터링 하는 데 필요한 ** \@ source_dbms** 및 기타 매개 변수를 지정 합니다. 결과 집합에서 원하는 매핑에 대한 **mapping_id** 의 값을 확인합니다.  
  
3.  데이터베이스의 배포자에서 [sp_setdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql)을 실행합니다.  
  
    -   2단계에서 얻은 **mapping_id**의 원하는 값을 아는 경우 **\@mapping_id**에 이 값을 지정합니다.  
  
    -   **mapping_id**를 모르는 경우 **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_type** 매개 변수 및 기존 매핑을 식별하는 데 필요한 기타 매개 변수를 지정합니다.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>지정된 Oracle 데이터 형식에 대한 유효한 데이터 형식을 찾으려면  
  
1.  데이터베이스의 배포자에서 [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql)을 실행합니다. ** \@ Source_dbms** 에 **ORACLE** 값을 지정 하 고 결과 집합을 필터링 하는 데 필요한 기타 매개 변수를 지정 합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 열을 Oracle 데이터 형식 NUMBER로 변경하여 기본 `numeric` 데이터 형식 대신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 숫자 데이터 형식 `float`(38,38)에 매핑되도록 합니다.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_changecolumndatatype)]  
  
 다음 쿼리 예에서는 Oracle 9 데이터 형식 `CHAR`에 대한 기본 및 대체 매핑을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_char)]  
  
 다음 쿼리 예에서는 소수 자릿수 또는 전체 자릿수 없이 지정된 경우 Oracle 9 데이터 형식 `NUMBER`에 대한 기본 매핑을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_number)]  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자에 대 한 데이터 형식 매핑](../non-sql/data-type-mapping-for-oracle-publishers.md)   
 [다른 유형의 데이터베이스 복제](../non-sql/heterogeneous-database-replication.md)   
 [복제 시스템 저장 프로시저 개념](../concepts/replication-system-stored-procedures-concepts.md)   
 [Oracle 게시자 구성](../non-sql/configure-an-oracle-publisher.md)  
  
  
