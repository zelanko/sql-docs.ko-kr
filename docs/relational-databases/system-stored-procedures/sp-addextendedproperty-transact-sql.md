---
description: sp_addextendedproperty(Transact-SQL)
title: sp_addextendedproperty (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproperty
- sp_addextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproperty
ms.assetid: 565483ea-875b-4133-b327-d0006d2d7b4c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 184328e9b6d5c197b06f89f151942535a90f7f91
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474654"
---
# <a name="sp_addextendedproperty-transact-sql"></a>sp_addextendedproperty(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  데이터베이스 개체에 새 확장 속성을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addextendedproperty  
    [ @name = ] { 'property_name' }  
    [ , [ @value = ] { 'value' }   
        [ , [ @level0type = ] { 'level0_object_type' }   
          , [ @level0name = ] { 'level0_object_name' }   
                [ , [ @level1type = ] { 'level1_object_type' }   
                  , [ @level1name = ] { 'level1_object_name' }   
                        [ , [ @level2type = ] { 'level2_object_type' }   
                          , [ @level2name = ] { 'level2_object_name' }   
                        ]   
                ]  
        ]   
    ]   
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @name ] = {'*property_name*'}  
 추가할 속성의 이름입니다. *property_name* 는 **sysname** 이며 NULL 일 수 없습니다. 또한 이름은 영숫자가 아닌 문자열 또는 공백 및 이진 값을 포함할 수 있습니다.  
  
 [ @value =] {'*value*'}  
 속성과 연결할 값입니다. *값* 은 **sql_variant** 이며 기본값은 NULL입니다. *value* 의 크기는 7,500바이트보다 클 수 없습니다.  
  
 [ @level0type =] {'*level0_object_type*'}  
 수준 0 개체의 유형입니다. *level0_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다.  
  
 유효한 입력은 ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE, PLAN GUIDE 및 NULL입니다.  
  
> [!IMPORTANT]  
>  수준 1 유형 개체의 확정 속성에서 USER를 수준 0 유형으로 지정하는 기능은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 대신 SCHEMA를 수준 0 유형으로 사용합니다. 예를 들어 테이블에 확장 속성을 정의할 때 사용자 이름 대신 테이블의 스키마를 지정합니다. TYPE을 수준 0 유형으로 지정하는 기능은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. TYPE의 경우 수준 0 유형으로 SCHEMA를 사용하고 수준 1 유형으로 TYPE을 사용합니다.  
  
 [ @level0name =] {'*level0_object_name*'}  
 지정된 수준 0 개체 유형의 이름입니다. *level0_object_name* 는 **sysname** 이며 기본값은 NULL입니다.  
  
 [ @level1type =] {'*level1_object_type*'}  
 수준 1 개체의 유형입니다. *level1_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SEQUENCE, 동의어, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION 및 NULL입니다.    
 [ @level1name =] {'*level1_object_name*'}  
 지정된 수준 1 개체 유형의 이름입니다. *level1_object_name* 는 **sysname** 이며 기본값은 NULL입니다.  
  
 [ @level2type =] {'*level2_object_type*'}  
 수준 2 개체의 유형입니다. *level2_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER 및 NULL입니다.  
  
 [ @level2name =] {'*level2_object_name*'}  
 지정된 수준 2 개체 유형의 이름입니다. *level2_object_name* 는 **sysname** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 확장 속성을 지정하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 개체는 세 수준(0, 1, 2)으로 분류됩니다. 수준 0은 최고 수준이며 데이터베이스 범위에 포함된 개체로 정의됩니다. 수준 1 개체는 스키마나 USER 범위에 포함되어 있고 수준 2 개체는 수준 1 개체에 포함되어 있습니다. 모든 수준의 개체에 대해 확장 속성을 정의할 수 있습니다.  
  
 한 수준에 있는 개체를 참조할 때는 해당 개체를 소유하거나 포함하는 더 높은 수준의 개체 이름을 지정해야 합니다. 예를 들어 확장 속성을 테이블 열(수준 2)에 추가할 때 열을 포함하는 테이블 이름(수준 1)과 테이블을 포함하는 스키마(수준 0)도 지정해야 합니다.  
  
 모든 개체 유형과 이름이 Null인 경우 속성은 현재 업데이트 자체에 속하게 됩니다.  
  
 확장 속성은 시스템 개체, 사용자 정의 데이터베이스 범위 밖의 개체 또는 인수에 유효한 입력으로 나열되지 않은 개체에 대해 허용되지 않습니다.  
  
 메모리 최적화 테이블에는 확장 속성을 사용할 수 없습니다.  
  
## <a name="replicating-extended-properties"></a>확장 속성 복제  
 확장 속성은 게시자와 구독자 간의 초기 동기화 수행 시에만 복제됩니다. 초기 동기화 후에 확장 속성을 추가하거나 수정하면 변경 내용이 복제되지 않습니다. 데이터베이스 개체를 복제 하는 방법에 대 한 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)를 참조 하세요.  
  
## <a name="schema-vs-user"></a>SCHEMA와  사용자  
 확장 속성을 데이터베이스 개체에 적용할 때 USER를 수준 0 유형으로 지정하는 것은 이름 확인에 혼동을 일으킬 수 있으므로 사용하지 않는 것이 좋습니다. 예를 들어 사용자 Mary가 두 개의 스키마(Mary 및 MySchema)를 소유하고 있고 두 스키마 모두 MyTable이라는 테이블을 포함하고 있다고 가정합니다. Mary가 확장 속성을 MyTable 테이블에 추가 하 고 **@level0type = N'USER '**, **@level0name = Mary** 를 지정 하는 경우 확장 속성이 적용 되는 테이블을 명확 하 게 알 수 없습니다. 이전 버전과의 호환성을 유지하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 해당 속성을 Mary라는 스키마에 포함된 테이블에 적용합니다.  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 및 db_ddladmin 고정 데이터베이스 역할의 멤버는 확장 속성을 모든 개체에 추가할 수 있습니다. 단, 데이터베이스 자체 나 사용자 또는 역할에 속성을 추가할 수 db_ddladmin.  
  
 사용자는 자신이 소유하거나 ALTER 또는 CONTROL 권한이 있는 개체에 확장 속성을 추가할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-an-extended-property-to-a-database"></a>A. 데이터베이스에 확장 속성 추가  
 다음 예에서는 값이 `'Caption'` 인 `'AdventureWorks2012 Sample OLTP Database'` 속성 이름이 `AdventureWorks2012` 예제 데이터베이스에 추가됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
--Add a caption to the AdventureWorks2012 Database object itself.  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'AdventureWorks2012 Sample OLTP Database';  
```  
  
### <a name="b-adding-an-extended-property-to-a-column-in-a-table"></a>B. 테이블의 열에 확장 속성 추가  
 다음 예에서는 `PostalCode` 테이블의 `Address`열에 캡션 속성이 추가됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Caption',   
@value = 'Postal code is a required column.',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table',  @level1name = 'Address',  
@level2type = N'Column', @level2name = 'PostalCode';  
GO  
```  
  
### <a name="c-adding-an-input-mask-property-to-a-column"></a>C. 열에 입력 마스크 속성 추가  
 다음 예에서는`99999 or 99999-9999 or #### ###`테이블의 `PostalCode` 열에 ' `Address`' 입력 마스크 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'Input Mask ', @value = '99999 or 99999-9999 or #### ###',  
@level0type = N'Schema', @level0name = 'Person',  
@level1type = N'Table', @level1name = 'Address',   
@level2type = N'Column',@level2name = 'PostalCode';  
GO  
```  
  
### <a name="d-adding-an-extended-property-to-a-filegroup"></a>D. 파일 그룹에 확장 속성 추가  
 다음 예에서는 `PRIMARY` 파일 그룹에 확장 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Primary filegroup for the AdventureWorks2012 sample database.',   
@level0type = N'FILEGROUP', @level0name = 'PRIMARY';  
GO  
```  
  
### <a name="e-adding-an-extended-property-to-a-schema"></a>E. 스키마에 확장 속성 추가  
 다음 예에서는 `HumanResources` 스키마에 확장 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',  
@value = N'Contains objects related to employees and departments.',  
@level0type = N'SCHEMA',   
@level0name = 'HumanResources';  
```  
  
### <a name="f-adding-an-extended-property-to-a-table"></a>F. 테이블에 확장 속성 추가  
 다음 예에서는 `Address` 스키마의 `Person` 테이블에 확장 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_DescriptionExample',   
@value = N'Street address information for customers, employees, and vendors.',   
@level0type = N'SCHEMA', @level0name = 'Person',  
@level1type = N'TABLE',  @level1name = 'Address';  
GO  
```  
  
### <a name="g-adding-an-extended-property-to-a-role"></a>G. 역할에 확장 속성 추가  
 다음 예에서는 애플리케이션 역할을 만들고 해당 역할에 확장 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;   
GO  
CREATE APPLICATION ROLE Buyers  
WITH Password = '987G^bv876sPY)Y5m23';   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Application Role for the Purchasing Department.',  
@level0type = N'USER',  
@level0name = 'Buyers';  
```  
  
### <a name="h-adding-an-extended-property-to-a-type"></a>H. 유형에 확장 속성 추가  
 다음 예에서는 유형에 확장 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'Data type (alias) to use for any column that represents an order number. For example a sales order number or purchase order number.',   
@level0type = N'SCHEMA',   
@level0name = N'dbo',   
@level1type = N'TYPE',   
@level1name = N'OrderNumber';  
```  
  
### <a name="i-adding-an-extended-property-to-a-user"></a>9\. 사용자에 확장 속성 추가  
 다음 예에서는 사용자를 만들고 해당 사용자에 확장 속성을 추가합니다.  
  
```  
USE AdventureWorks2012;   
GO  
CREATE USER CustomApp WITHOUT LOGIN ;   
GO  
EXEC sys.sp_addextendedproperty   
@name = N'MS_Description',   
@value = N'User for an application.',   
@level0type = N'USER',   
@level0name = N'CustomApp';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sys.fn_listextendedproperty &#40;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sp_dropextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sp_updateextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
