---
title: sp_dropextendedproperty (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproperty_TSQL
- sp_dropextendedproperty
dev_langs: TSQL
helpviewer_keywords: sp_dropextendedproperty
ms.assetid: 4851865a-86ca-4823-991a-182dd1934075
caps.latest.revision: "45"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: efb717db1c6e6bbe42faba15fffe524ac2e55ade
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spdropextendedproperty-transact-sql"></a>sp_dropextendedproperty(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존의 확장 속성을 삭제합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropextendedproperty   
    [ @name = ] { 'property_name' }  
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
```  
  
## <a name="arguments"></a>인수  
 [ @name=] {'*property_name*'을 (를)  
 삭제할 속성의 이름입니다. *property_name* 은 **sysname** NULL 일 수 없습니다.  
  
 [ @level0type=] {'*level0_object_type*'을 (를)  
 지정된 수준 0 개체 유형의 이름입니다. *level0_object_type* 은 **varchar (128)**, 기본값은 NULL입니다.  
  
 유효한 입력은 ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, USER, TRIGGER, TYPE 및 NULL입니다.  
  
> [!IMPORTANT]  
>  수준 0 유형 USER와 TYPE은 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. USER 대신 SCHEMA를 수준 0 유형으로 사용합니다. TYPE의 경우 수준 0 유형으로 SCHEMA를 사용하고 수준 1 유형으로 TYPE을 사용합니다.  
  
 [ @level0name=] {'*level0_object_name*'을 (를)  
 지정된 수준 0 개체 유형의 이름입니다. *level0_object_name* 은 **sysname** 기본값은 NULL입니다.  
  
 [ @level1type=] {'*level1_object_type*'을 (를)  
 수준 1 개체의 유형입니다. *level1_object_type* 은 **varchar (128)** 기본값은 NULL입니다. 유효한 입력은 AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION 및 NULL입니다.  
  
 [ @level1name=] {'*level1_object_name*'을 (를)  
 지정된 수준 1 개체 유형의 이름입니다. *level1_object_name* 은 **sysname** 기본값은 NULL입니다.  
  
 [ @level2type=] {'*level2_object_type*'을 (를)  
 수준 2 개체의 유형입니다. *level2_object_type* 은 **varchar (128)** 기본값은 NULL입니다. 유효한 입력은 COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER 및 NULL입니다.  
  
 [ @level2name=] {'*level2_object_name*'을 (를)  
 지정된 수준 2 개체 유형의 이름입니다. *level2_object_name* 은 **sysname** 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 확장 속성을 지정하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 개체는 세 수준(0, 1, 2)으로 분류됩니다. 수준 0은 최고 수준이며 데이터베이스 범위에 포함된 개체로 정의됩니다. 수준 1 개체는 스키마나 USER 범위에 포함되어 있고 수준 2 개체는 수준 1 개체에 포함되어 있습니다. 모든 수준의 개체에 대해 확장 속성을 정의할 수 있습니다. 한 수준에 있는 개체를 참조할 때는 모든 상위 수준 개체의 유형과 이름으로 한정해야 합니다.  
  
 지정 된 유효한 *property_name*, 모든 개체 유형과 이름이 null이 고 속성이 현재 데이터베이스에 있는 경우, 해당 속성이 삭제 됩니다. 이 항목의 뒷부분에 나오는 예 2를 참조하십시오.  
  
## <a name="permissions"></a>Permissions  
 Db_owner 및 db_ddladmin 고정 데이터베이스 역할의 멤버는 예외가 발생 하 여 모든 개체의 확장된 속성을 삭제할 수 있습니다: db_ddladmin은 데이터베이스 자체 또는 사용자나 역할에 속성을 추가 하지 않을 수 있습니다.  
  
 사용자는 자신이 소유하고 있거나 ALTER 또는 CONTROL 권한을 가지고 있는 개체에 대한 확장 속성을 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-an-extended-property-on-a-column"></a>1. 열의 확장 속성 삭제  
 다음 예에서는 `caption` 스키마에 포함되어 있는 `id` 테이블의 `T1` 열에서 `dbo` 속성을 제거합니다.  
  
```  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
     @name = 'caption'   
    ,@value = 'Employee ID'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
EXEC sp_dropextendedproperty   
     @name = 'caption'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
DROP TABLE T1;  
GO  
```  
  
### <a name="b-dropping-an-extended-property-on-a-database"></a>2. 데이터베이스의 확장 속성 삭제  
 다음 예에서는 라는 속성을 제거 `MS_Description` 에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스. 이 속성은 데이터베이스 자체에 있으므로 개체 유형과 이름이 지정되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_dropextendedproperty   
@name = N'MS_Description';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40; Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
