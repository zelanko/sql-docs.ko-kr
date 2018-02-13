---
title: "동의어(데이터베이스 엔진) | Microsoft 문서"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: synonyms
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 15c8ca0028ae722823198087b06d4f435aba40e4
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="synonyms-database-engine"></a>동의어(데이터베이스 엔진)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
동의어란 다음 용도로 사용되는 데이터베이스 개체입니다.  
  
-   로컬 서버나 원격 서버에 있을 수 있는 기본 개체로 참조되는 다른 데이터베이스 개체의 대체 이름을 제공합니다.  
  
-   기본 개체의 이름이나 위치의 변경으로부터 클라이언트 응용 프로그램을 보호하는 추상적 계층을 제공합니다.  
  
 예를 들어 **Server1** 이라는 서버에 있는 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]의 **Employee**테이블을 검토해 보십시오. 다른 서버 **Server2**에서 이 테이블을 참조하려면 클라이언트 응용 프로그램이 네 부분으로 된 이름 **Server1.AdventureWorks.Person.Employee**를 사용해야 합니다. 또한 테이블 위치를 다른 서버 등으로 변경하는 경우 이 변경 내용을 반영하기 위해 클라이언트 응용 프로그램을 수정해야 합니다.  
  
 **Server1**의 **Employee** 테이블에 대한 동의어, **EmpTable** 을 **Server2**에 만들어 이러한 문제를 해결할 수 있습니다. 이제 클라이언트 응용 프로그램은 단일 부분으로 된 이름인 **EmpTable**만 사용하여 **Employee** 테이블을 참조해야 합니다. 또한 **Employee** 테이블 위치가 변경되면 동의어 **EmpTable**를 수정하여 **Employee** 테이블의 새 위치를 가리키게 해야 합니다. ALTER SYNONYM 문이 없으므로 먼저 동의어 **EmpTable**을 삭제한 다음 같은 이름으로 동의어를 다시 만들지만 **Employee**의 새 위치를 가리키게 해야 합니다.  
  
 동의어는 스키마에 속하고 스키마의 다른 개체처럼 동의어 이름은 고유해야 합니다. 다음 데이터베이스 개체의 동의어를 만들 수 있습니다.  
  
|||  
|-|-|  
|어셈블리(CLR) 저장 프로시저|어셈블리(CLR) 테이블 반환 함수|  
|어셈블리(CLR) 스칼라 함수|어셈블리(CLR) 집계 함수|  
|복제 필터 프로시저|확장 저장 프로시저|  
|SQL 스칼라 함수|SQL 테이블 반환 함수|  
|SQL 인라인 테이블 반환 함수|SQL 저장 프로시저|  
|보기|테이블*(사용자 정의)|  
  
 *로컬 및 전역 임시 테이블이 포함됩니다.  
  
> [!NOTE]  
>  함수 기본 개체의 네 부분으로 된 이름은 지원되지 않습니다.  
  
 동의어는 다른 동의어의 기본 개체가 될 수 없고 사용자 정의 집계 함수를 참조할 수 없습니다.  
  
 동의어와 해당 기본 개체는 이름별로만 바인딩됩니다. 기본 개체에 대한 모든 존재, 유형 및 권한 검사는 런타임까지 지연됩니다. 따라서 기본 개체를 수정, 삭제 또는 삭제 후 원래 기본 개체와 같은 이름을 가진 다른 개체로 바꿀 수 있습니다. 예를 들어 **의**Person.Contact **테이블을 참조하는 동의어** MyContacts [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]를 고려해 보십시오. **Contact** 테이블을 삭제한 후 **Person.Contact**라는 뷰로 바꾸면 **MyContacts** 는 **Person.Contact** 뷰를 참조합니다.  
  
 동의어에 대한 참조는 스키마에 바인딩되지 않습니다. 따라서 동의어는 언제라도 삭제할 수 있습니다. 그러나 동의어를 삭제하면 삭제된 동의어에 대한 참조가 현수 참조로 남게 될 위험이 있습니다. 이러한 참조는 런타임에만 발견됩니다.  
  
## <a name="synonyms-and-schemas"></a>동의어 및 스키마  
 소유하지 않은 기본 스키마가 있는데 동의어를 만들려면 소유한 스키마 이름을 사용하여 동의어 이름을 적합하게 지정해야 합니다. 예를 들어 **x**스키마를 소유하지만 **y** 스키마가 기본 스키마이고 CREATE SYNONYM 문을 사용할 경우에는 단일 부분으로 된 이름을 사용하여 동의어 이름을 지정하는 대신 **x**스키마를 동의어 이름 접두사로 지정해야 합니다. 동의어를 만드는 방법은 [CREATE SYNONYM&#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)테이블을 검토해 보십시오.  
  
## <a name="granting-permissions-on-a-synonym"></a>동의어에 대한 권한 부여  
 **db_owner**의 멤버나 **db_ddladmin** 의 멤버인 동의어 소유자만 동의어에 대한 권한을 부여 받을 수 있습니다.  
  
 동의어에 대한 다음과 같은 모든 권한에 대해 GRANT, DENY 및 REVOKE를 수행할 수 있습니다.  
  
|||  
|-|-|  
|CONTROL|Delete|  
|CREATE 문을 실행하기 전에|INSERT|  
|SELECT|TAKE OWNERSHIP|  
|UPDATE|VIEW DEFINITION|  
  
## <a name="using-synonyms"></a>동의어 사용  
 여러 SQL 문 및 식 컨텍스트에서 동의어를 해당 참조 기준 개체 대신 사용할 수 있습니다. 다음 표에서는 이러한 문 및 식 컨텍스트를 나열합니다.  
  
|||  
|-|-|  
|SELECT|INSERT|  
|UPDATE|Delete|  
|CREATE 문을 실행하기 전에|하위 SELECT|  
  
 앞에서 설명한 컨텍스트에서 동의어를 사용하면 기준 개체가 영향을 받습니다. 예를 들어 동의어가 테이블 기준 개체를 참조하며 동의어에 행을 삽입한 경우 실제로 참조되는 테이블에 행이 삽입됩니다.  
  
> [!NOTE]  
>  연결된 서버에 있는 동의어는 참조할 수 없습니다.  
  
 동의어를 OBJECT_ID 함수의 매개 변수로 사용할 수 있습니다. 그러나 함수는 기본 개체가 아닌 동의어의 개체 ID를 반환합니다.  
  
 DDL 문에서는 동의어를 참조할 수 없습니다. 예를 들어 `dbo.MyProduct`라는 동의어를 참조하는 다음 문은 오류를 생성합니다.  
  
```  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
 사용 권한 제어를 위한 다음 문은 동의어에만 관련되며 기준 개체와는 관련되지 않습니다.  
  
|||  
|-|-|  
|GRANT|DENY|  
|REVOKE||  
  
 동의어는 스키마 바운드가 아니므로 다음과 같은 스키마 바운드 식 컨텍스트에서 참조할 수 없습니다.  
  
|||  
|-|-|  
|CHECK 제약 조건|계산 열|  
|기본 식|규칙 식|  
|스키마 바운드 뷰|스키마 바운드 함수|  
  
 스키마 바운드 함수에 대한 자세한 내용은 [사용자 정의 함수 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)를 참조하세요.  
  
## <a name="getting-information-about-synonyms"></a>동의어에 대한 정보 가져오기  
 sys.synonyms 카탈로그 뷰에는 지정된 데이터베이스의 각 동의어에 대한 항목이 들어 있습니다. 이 카탈로그 뷰는 동의어 이름과 기본 개체 이름과 같은 동의어 메타데이터를 노출합니다. **sys.synonyms** 카탈로그 뷰에 대한 자세한 내용은 [sys.synonyms&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)를 참조하세요.  
  
 확장 속성을 사용하면 설명이나 지시 텍스트, 입력 마스크, 서식 설정 규칙을 동의어 속성으로 추가할 수 있습니다. 속성이 데이터베이스에 저장되기 때문에 속성을 읽는 모든 응용 프로그램은 개체를 같은 방식으로 평가할 수 있습니다. 자세한 내용은 [sp_addextendedproperty&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)를 참조하세요.  
  
 동의어 기본 개체의 기본 유형을 찾으려면 OBJECTPROPERTYEX 함수를 사용합니다. 자세한 내용은 [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)를 참조하세요.  
  
### <a name="examples"></a>예  
 다음 예에서는 로컬 개체인 동의어 기본 개체의 기본 유형을 반환합니다.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
 다음 예에서는 `Server1`서버에 위치한 원격 개체인 동의어 기본 개체의 기본 유형을 반환합니다.  
  
```  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>관련 내용  
 [동의어 만들기](../../relational-databases/synonyms/create-synonyms.md)  
  
 [CREATE SYNONYM&#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)  
  
 [DROP SYNONYM&#40;Transact-SQL&#41;](../../t-sql/statements/drop-synonym-transact-sql.md)  
  
  
