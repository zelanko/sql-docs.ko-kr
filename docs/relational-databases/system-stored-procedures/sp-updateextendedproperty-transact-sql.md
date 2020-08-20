---
description: sp_updateextendedproperty(Transact-SQL)
title: sp_updateextendedproperty (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f8bedf71c6ec255aa0b81117c80e9aca6f5b1f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473496"
---
# <a name="sp_updateextendedproperty-transact-sql"></a>sp_updateextendedproperty(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  기존 확장 속성의 값을 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>인수  
 [ @name =] {'*property_name*'}  
 업데이트할 속성의 이름입니다. *property_name* 는 **sysname**이며 NULL 일 수 없습니다.  
  
 [ @value =] {'*value*'}  
 속성에 연결된 값입니다. *값* 은 **sql_variant**이며 기본값은 NULL입니다. *값* 의 크기는 7500 바이트를 초과할 수 없습니다.  
  
 [ @level0type =] {'*level0_object_type*'}  
 사용자 또는 사용자 정의 형식입니다. *level0_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, PLAN GUIDE, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE 및 NULL입니다.  
  
> [!IMPORTANT]  
>  수준 0 유형 USER와 TYPE은 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. USER 대신 SCHEMA를 수준 0 유형으로 사용합니다. TYPE의 경우 수준 0 유형으로 SCHEMA를 사용하고 수준 1 유형으로 TYPE을 사용합니다.  
  
 [ @level0name =] {'*level0_object_name*'}  
 지정된 수준 1 개체 유형의 이름입니다. *level0_object_name* 는 **sysname** 이며 기본값은 NULL입니다.  
  
 [ @level1type =] {'*level1_object_type*'}  
 수준 1 개체의 유형입니다. *level1_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION 및 NULL입니다.  
  
 [ @level1name =] {'*level1_object_name*'}  
 지정된 수준 1 개체 유형의 이름입니다. *level1_object_name* 는 **sysname** 이며 기본값은 NULL입니다.  
  
 [ @level2type =] {'*level2_object_type*'}  
 수준 2 개체의 유형입니다. *level2_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER 및 NULL입니다.  
  
 [ @level2name =] {'*level2_object_name*'}  
 지정된 수준 2 개체 유형의 이름입니다. *level2_object_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 확장 속성을 지정하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 개체는 세 수준(0, 1, 2)으로 분류됩니다. 수준 0은 최고 수준이며 데이터베이스 범위에 포함된 개체로 정의됩니다. 수준 1 개체는 스키마나 USER 범위에 포함되어 있고 수준 2 개체는 수준 1 개체에 포함되어 있습니다. 모든 수준의 개체에 대해 확장 속성을 정의할 수 있습니다. 한 수준에 있는 개체를 참조할 때는 해당 개체를 소유하거나 포함하는 더 높은 수준의 개체 이름을 지정해야 합니다.  
  
 유효한 *property_name* 및 *값*이 지정 된 경우 모든 개체 형식 및 이름이 null 이면 업데이트 된 속성이 현재 데이터베이스에 속합니다.  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 및 db_ddladmin 고정 데이터베이스 역할의 멤버는 개체의 확장 속성을 업데이트할 수 있습니다. 단, 데이터베이스 자체 나 사용자 또는 역할에는 속성을 추가할 수 없습니다 db_ddladmin.  
  
 사용자는 자신이 소유하거나 ALTER 또는 CONTROL 권한이 있는 개체의 확장 속성을 업데이트할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>A. 열의 확장 속성 업데이트  
 다음 예에서는 `Caption` 테이블의 `ID` 열에서 `T1` 속성의 값을 업데이트합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. 데이터베이스의 확장 속성 업데이트  
 다음 예에서는 먼저 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에 확장 속성을 만든 다음 이 속성 값을 업데이트합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [fn_listextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sp_addextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sp_dropextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [extended_properties &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
