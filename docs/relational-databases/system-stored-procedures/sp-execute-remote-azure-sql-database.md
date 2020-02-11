---
title: sp_execute_remote (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 021a6e689dfc109f8a58ca080956aec7efc49291
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124469"
---
# <a name="sp_execute_remote-azure-sql-database"></a>sp_execute_remote(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  단일 원격 [!INCLUDE[tsql](../../includes/tsql-md.md)] Azure SQL Database 또는 행 분할 체계에서 분할 역할을 하는 데이터베이스 집합에 대해 문을 실행 합니다.  
  
 저장 프로시저는 탄력적 쿼리 기능의 일부입니다.  분할에 대 한 탄력적 [데이터베이스 쿼리 개요](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) 및 [탄력적 데이터베이스 쿼리 (행 분할)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/)를 Azure SQL Database 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>인수  
 [ \@data_source_name =] *datasourcename*  
 문이 실행 되는 외부 데이터 원본을 식별 합니다. [CREATE EXTERNAL DATA SOURCE &#40;transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조 하세요. 외부 데이터 원본은 "RDBMS" 또는 "SHARD_MAP_MANAGER" 형식일 수 있습니다.  
  
 [ \@stmt =] *문*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이나 일괄 처리를 포함 하는 유니코드 문자열입니다. \@stmt는 유니코드 상수 또는 유니코드 변수 여야 합니다. + 연산자로 두 문자열을 연결한 식처럼 더 복잡한 유니코드 식은 사용할 수 없습니다. 문자 상수도 사용할 수 없습니다. 유니코드 상수를 지정 하는 경우에는 접두사 **N**을 접두사로 사용 해야 합니다. 예를 들어 유니코드 상수 **N ' sp_who '** 는 올바르지만 **' sp_who '** 문자 상수는 유효 하지 않습니다. 문자열의 크기는 사용 가능한 데이터베이스 서버 메모리의 용량에 따라서만 제한됩니다. 64 비트 서버에서 문자열 크기는 최대 **nvarchar (max)** 크기인 2gb로 제한 됩니다.  
  
> [!NOTE]  
>  \@stmt는 변수 이름과 같은 형식의 매개 변수를 포함할 수 있습니다. 예를 들면 다음과 같습니다.`N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Stmt에 \@포함 된 각 매개 변수에는 \@params 매개 변수 정의 목록과 매개 변수 값 목록 모두에 해당 하는 항목이 있어야 합니다.  
  
 [ \@params =] N '\@*parameter_name * * data_type* [,... *n* ] '  
 Stmt에 \@포함 된 모든 매개 변수의 정의를 포함 하는 하나의 문자열입니다. 문자열은 유니코드 상수 또는 유니코드 변수 여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. *n* 은 추가 매개 변수 정의를 나타내는 자리 표시자입니다. Stmtmust에 \@지정 된 모든 매개 변수는 \@params에 정의 되어 있습니다. Stmt의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 \@에 매개 변수가 없는 경우 \@params가 필요 하지 않습니다. 이 매개 변수의 기본값은 NULL입니다.  
  
 [ \@param1 =] '*value1*'  
 매개 변수 문자열에 정의된 첫 번째 매개 변수의 값입니다. 값은 유니코드 상수 또는 유니코드 변수가 될 수 있습니다. Stmt에 \@포함 된 모든 매개 변수에 대해 제공 되는 매개 변수 값이 있어야 합니다. Stmt의 [!INCLUDE[tsql](../../includes/tsql-md.md)] \@문 또는 일괄 처리에 매개 변수가 없는 경우에는 값이 필요 하지 않습니다.  
  
 *n*  
 추가 매개 변수의 값에 대한 자리 표시자입니다. 값은 상수 또는 변수만 가능합니다. 함수 또는 연산자를 사용하여 작성한 식처럼 더 복잡한 식은 값으로 사용할 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 값(실패)  
  
## <a name="result-sets"></a>결과 집합  
 첫 번째 SQL 문의 결과 집합을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 `ALTER ANY EXTERNAL DATA SOURCE` 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 `sp_execute_remote`위의 구문 섹션에 설명 된 대로 매개 변수를 특정 순서로 입력 해야 합니다. 매개 변수 순서가 잘못되면 오류 메시지가 나타납니다.  
  
 `sp_execute_remote`는 일괄 처리 및 이름 범위와 관련 하 여 [&#40;transact-sql&#41;를 실행](../../t-sql/language-elements/execute-transact-sql.md) 하는 것과 동일한 동작을 수행 합니다. Sp_execute_remote * \@stmt* 매개 변수의 transact-sql 문이나 일괄 처리는 sp_execute_remote 문을 실행할 때까지 컴파일되지 않습니다.  
  
 `sp_execute_remote`행을 생성 한 원격 데이터베이스의 이름을 포함 하는 ' $ShardName ' 이라는 결과 집합에 추가 열을 추가 합니다.  
  
 `sp_execute_remote`[sp_executesql &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)와 유사 하 게 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
### <a name="simple-example"></a>간단한 예  
 다음 예에서는 원격 데이터베이스에 대해 간단한 SELECT 문을 만들고 실행 합니다.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>여러 매개 변수를 사용 하는 예제  
Master 데이터베이스에 대 한 관리자 자격 증명을 지정 하 여 사용자 데이터베이스에 데이터베이스 범위 자격 증명을 만듭니다. Master 데이터베이스를 가리키고 데이터베이스 범위 자격 증명을 지정 하는 외부 데이터 원본을 만듭니다. 그런 다음 사용자 데이터베이스의 예를 따라 master 데이터베이스에서 `sp_set_firewall_rule` 프로시저를 실행 합니다. 프로시저 `sp_set_firewall_rule` 에는 3 개의 매개 변수가 필요 하며 `@name` , 매개 변수는 유니코드로 되어 있어야 합니다.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>참고 항목:

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
