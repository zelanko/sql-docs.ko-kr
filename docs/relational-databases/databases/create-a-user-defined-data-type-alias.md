---
title: 사용자 정의 데이터 형식 별칭 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.userdefineddatatype.general.f1
- sql13.swb.new.datatype.properties.general.f1
helpviewer_keywords:
- alias data types [SQL Server], creating
ms.assetid: b1dd8413-0cd0-411b-a79b-1bb043ccc62d
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 411b717866ff137b498d12aff3994e2a7436101d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32931298"
---
# <a name="create-a-user-defined-data-type-alias"></a>사용자 정의 데이터 형식 별칭 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 새 사용자 정의 데이터 형식 별칭을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **사용자 정의 데이터 형식 별칭을 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   사용자 정의 데이터 형식 별칭의 이름은 식별자에 대한 규칙을 따라야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 현재 데이터베이스에 대한 CREATE TYPE 권한 및 *schema_name*에 대한 ALTER 권한이 필요합니다. *schema_name* 을 지정하지 않으면 현재 사용자에 대한 스키마를 결정하는 기본 이름 확인 규칙이 적용됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-user-defined-data-type"></a>사용자 정의 데이터 형식을 만들려면  
  
1.  개체 탐색기에서 **데이터베이스**를 확장하고 목록에서 원하는 데이터베이스를 확장한 다음, **프로그래밍 기능**과 **유형**을 차례로 확장하고 **사용자 정의 데이터 형식**을 마우스 오른쪽 단추로 클릭한 다음 **새 사용자 정의 데이터 형식**을 클릭합니다.  
  
     **NULL 허용**  
     사용자 정의 데이터 형식에 NULL 값이 허용되는지 여부를 지정합니다. 기존 사용자 정의 데이터 형식의 Null 허용 여부는 편집할 수 없습니다.  
  
     **Data type**  
     목록 상자에서 기본 데이터 형식을 선택합니다. 목록 상자에는 **geography**, **geometry**, **hierarchyid**, **sysname**, **timestamp** 및 **xml** 데이터 형식을 제외한 모든 데이터 형식이 표시됩니다. 기존 사용자 정의 데이터 형식의 데이터 형식은 편집할 수 없습니다.  
  
     **Default**  
     필요에 따라 사용자 정의 데이터 형식 별칭에 바인딩할 기본값을 선택합니다.  
  
     **길이/전체 자릿수**  
     데이터 형식에 적용되는 길이 또는 전체 자릿수를 표시합니다. **길이** 는 문자 기반 사용자 정의 데이터 형식에 적용되고 **전체 자릿수** 는 숫자 기반 사용자 정의 데이터 형식에 적용됩니다. 이 옵션의 레이블은 이전에 선택한 데이터 형식에 따라 바뀝니다. 선택한 데이터 형식의 길이 또는 전체 자릿수가 고정된 경우에는 이 상자를 편집할 수 없습니다.  
  
     **nvarchar(max)**, **varchar(max)** 또는 **varbinary(max)** 데이터 형식에 대해서는 길이가 표시되지 않습니다.  
  
     **이름**  
     새 사용자 정의 데이터 형식 별칭을 만드는 경우 데이터베이스에서 사용자 정의 데이터 형식을 나타내는 데 사용할 고유 이름을 입력합니다. 사용할 수 있는 최대 문자 수는 시스템의 **sysname** 데이터 형식과 동일합니다. 기존 사용자 정의 데이터 형식 별칭의 이름은 편집할 수 없습니다.  
  
     **규칙**  
     필요에 따라 사용자 정의 데이터 형식 별칭에 바인딩할 규칙을 선택합니다.  
  
     **소수 자릿수**  
     소수점의 오른쪽에 저장될 수 있는 최대 자릿수를 지정합니다.  
  
     **스키마**  
     현재 사용자가 사용할 수 있는 모든 스키마의 목록에서 스키마를 선택합니다. 현재 사용자에 대한 기본 스키마가 기본적으로 선택되어 있습니다.  
  
     **저장소**  
     사용자 정의 데이터 형식 별칭에 대한 최대 저장소 크기를 표시합니다. 최대 저장소 크기는 전체 자릿수에 따라 달라집니다.  
  
    |||  
    |-|-|  
    |1 – 9|5|  
    |10 – 19|9|  
    |20 – 28|13|  
    |29 – 38|17|  
  
     **nchar** 및 **nvarchar** 데이터 형식의 경우 저장소 값이 항상 **길이**값의 두 배입니다.  
  
     **nvarchar(max)**, **varchar(max)** 또는 **varbinary(max)** 데이터 형식에 대해서는 저장소가 표시되지 않습니다.  
  
2.  **새 사용자 정의 데이터 형식** 대화 상자의 **스키마** 상자에 이 데이터 형식 별칭을 소유할 스키마를 입력하거나 찾아보기 단추를 사용하여 스키마를 선택합니다.  
  
3.  **이름** 상자에 새 데이터 형식 별칭의 이름을 입력합니다.  
  
4.  **데이터 형식** 상자에서 어떤 데이터 형식을 기반으로 새 데이터 형식 별칭을 만들 것인지 선택합니다.  
  
5.  해당 데이터 형식에 맞게 적절히 **길이**, **전체 자릿수**및 **소수 자릿수** 상자를 채웁니다.  
  
6.  새 데이터 형식 별칭에 NULL 값을 허용하려면 **NULL 허용** 확인란을 선택합니다.  
  
7.  기본값이나 규칙을 새 데이터 형식 별칭에 바인딩하려면 **바인딩** 영역에서 **기본값** 또는 **규칙** 상자를 채웁니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 기본값과 규칙을 만들 수 없으므로 대신 [!INCLUDE[tsql](../../includes/tsql-md.md)]를 기본값과 규칙을 만드는 예제 코드는 템플릿 탐색기에서 찾을 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-user-defined-data-type-alias"></a>사용자 정의 데이터 형식 별칭을 만들려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 시스템이 제공하는 `varchar` 데이터 형식을 기반으로 데이터 형식 별칭을 만듭니다. `ssn` 데이터 형식 별칭은 11자리의 주민 등록 번호(999-99-9999)를 보유하는 열에 사용됩니다. 이 열은 NULL이 될 수 없습니다.  
  
```sql  
CREATE TYPE ssn  
FROM varchar(11) NOT NULL ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)   
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
  
