---
title: 데이터베이스 식별자 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- regular identifiers [SQL Server]
- identifiers [SQL Server]
- names [SQL Server], identifiers
- identifiers [SQL Server], about identifiers
- SQL Server identifiers
- Transact-SQL identifiers
- database objects [SQL Server], names
ms.assetid: 171291bb-f57f-4ad1-8cea-0b092d5d150c
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ea619fe016adff016241964c605e4db6c3c70377
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32932428"
---
# <a name="database-identifiers"></a>데이터베이스 식별자
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  데이터베이스 개체 이름을 그 개체의 식별자라고 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 모든 개체에는 식별자가 있습니다. 서버, 데이터베이스 그리고 테이블, 뷰, 열, 인덱스, 트리거, 프로시저, 제약 조건, 규칙 등과 같은 데이터베이스 개체도 식별자를 가질 수 있습니다. 식별자는 대부분의 개체에서 필수 항목이지만 제약 조건과 같은 일부 개체에서는 옵션입니다.  
  
 개체의 식별자는 개체를 정의할 때 만들어집니다. 만들어진 식별자는 개체를 참조하는 데 사용됩니다. 예를 들어 다음 문은 식별자가 `TableX`인 테이블과 식별자가 `KeyCol` 및 `Description`인 두 열을 만듭니다.  
  
```  
CREATE TABLE TableX  
(KeyCol INT PRIMARY KEY, Description nvarchar(80))  
```  
  
 이 테이블에는 이름 없는 제약 조건도 있습니다. `PRIMARY KEY` 제약 조건에는 식별자가 없습니다.  
  
 식별자의 데이터 정렬은 식별자가 정의된 수준에 따라 달라집니다. 로그인과 데이터베이스 이름 등 인스턴스 수준 개체의 식별자에는 인스턴스의 기본 데이터 정렬이 할당됩니다. 테이블, 뷰, 열 이름 등 데이터베이스에 있는 개체의 식별자에는 데이터베이스의 기본 데이터 정렬이 할당됩니다. 예를 들어 대/소문자만 다르고 이름은 동일한 두 테이블은 데이터 정렬이 대/소문자를 구분하는 데이터베이스에서는 만들 수 있지만 데이터 정렬이 대/소문자를 구분하지 않는 데이터베이스에서는 만들 수 없습니다.  
  
> [!NOTE]  
>  변수의 이름 또는 함수와 저장 프로시저의 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자의 규칙을 따라야 합니다.  
  
## <a name="classes-of-identifiers"></a>식별자 클래스  
 다음과 같이 두 가지 식별자 클래스가 있습니다.  
  
 일반 식별자  
 식별자 형식에 대한 규칙을 따릅니다. 일반 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 사용될 때 구분되지 않습니다.  
  
```  
SELECT *  
FROM TableX  
WHERE KeyCol = 124  
```  
  
 구분 식별자  
 큰따옴표(")나 대괄호([])로 묶여져 있습니다. 식별자 형식 규칙을 따르는 식별자는 구분되지 않을 수도 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT *  
FROM [TableX]         --Delimiter is optional.  
WHERE [KeyCol] = 124  --Delimiter is optional.  
```  
  
 모든 식별자 규칙을 따르지 않는 식별자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 구분되어야 합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT *  
FROM [My Table]      --Identifier contains a space and uses a reserved keyword.  
WHERE [order] = 10   --Identifier is a reserved keyword.  
```  
  
 일반 식별자 및 구분 식별자 모두는 1-128자의 문자로 이루어져야 합니다. 로컬 임시 테이블의 경우에는 식별자에 116자까지 포함할 수 있습니다.  
  
## <a name="rules-for-regular-identifiers"></a>일반 식별자 규칙  
 변수, 함수 및 저장 프로시저의 이름은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자의 다음 규칙을 따라야 합니다.  
  
1.  첫 문자는 다음 중 하나여야 합니다.  
  
    -   Unicode Standard 3.2에서 정의한 문자. 문자의 유니코드 정의에는 a-z, A-Z의 라틴어 문자와 다른 언어의 문자가 포함되어 있습니다.  
  
    -   밑줄(_), at 기호(@) 또는 숫자 기호(#)  
  
         특정 기호는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 식별자의 맨 앞에 올 때 특별한 의미를 갖습니다. at 기호로 시작하는 일반 식별자는 항상 지역 변수나 매개 변수를 표시하며 다른 개체 유형의 이름으로 사용할 수 없습니다. # 기호로 시작하는 식별자는 임시 테이블 또는 프로시저를 나타냅니다. 이중 숫자 기호(##)로 시작하는 식별자는 전역 임시 개체를 나타냅니다. 숫자 기호나 이중 숫자 기호를 사용하여 다른 개체 유형의 이름을 시작할 수 있지만 이 방법은 사용하지 않는 것이 좋습니다.  
  
         일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수는 두 개의 at 기호(@@)로 시작하는 이름을 사용합니다. 이러한 함수와 혼동하지 않도록 @@으로 시작하는 이름을 사용하지 않아야 합니다.  
  
2.  후속 문자는 다음을 포함할 수 있습니다.  
  
    -   Unicode Standard 3.2에서 정의한 문자  
  
    -   기본 라틴 또는 기타 국가 스크립트의 10진수  
  
    -   at 기호(@), 달러 기호($), 숫자 기호 또는 밑줄  
  
3.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 예약어는 식별자로 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 예약어는 대문자와 소문자가 모두 예약됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 식별자를 사용하는 경우 이러한 규칙을 따르지 않는 식별자는 큰따옴표나 대괄호로 구분해야 합니다. 예약되는 단어는 데이터베이스 호환성 수준에 따라 다릅니다. 이 수준은 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 문을 사용하여 설정할 수 있습니다.  
  
4.  포함된 공백이나 특수 문자는 사용할 수 없습니다.  
  
5.  보충 문자도 사용할 수 없습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 식별자를 사용하는 경우 이러한 규칙을 따르지 않는 식별자는 큰따옴표나 대괄호로 구분해야 합니다.  
  
> [!NOTE]  
>  일반 식별자 형식의 일부 규칙은 데이터베이스 호환성 수준에 따라 달라집니다. 이 수준은 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)를 사용하여 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [예약 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
