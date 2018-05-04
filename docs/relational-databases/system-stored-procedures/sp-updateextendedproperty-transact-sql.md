---
title: sp_updateextendedproperty (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 61ce9da4c904811708e70a8670ecf64271e98574
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spupdateextendedproperty-transact-sql"></a>sp_updateextendedproperty(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  기존 확장 속성의 값을 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @name=] {'*property_name*'을 (를)  
 업데이트할 속성의 이름입니다. *property_name* 은 **sysname**, NULL 일 수 없습니다.  
  
 [ @value=] {'*값*'을 (를)  
 속성에 연결된 값입니다. *값* 은 **sql_variant**, 기본값은 NULL입니다. 크기 *값* 7500 바이트를 초과할 수 없습니다.  
  
 [ @level0type=] {'*level0_object_type*'을 (를)  
 사용자 또는 사용자 정의 형식입니다. *level0_object_type* 은 **varchar (128)**, 기본값은 NULL입니다. 유효한 입력 어셈블리, 계약, 이벤트 알림, 파일 그룹, 메시지 유형, 파티션 함수, 파티션 구성표, 계획 지침, REMOTE SERVICE BINDING, 경로, 스키마, 서비스, 사용자, 트리거, 유형 및 NULL이 됩니다.  
  
> [!IMPORTANT]  
>  수준 0 유형 USER와 TYPE은 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. USER 대신 SCHEMA를 수준 0 유형으로 사용합니다. TYPE의 경우 수준 0 유형으로 SCHEMA를 사용하고 수준 1 유형으로 TYPE을 사용합니다.  
  
 [ @level0name=] {'*level0_object_name*'을 (를)  
 지정된 수준 1 개체 유형의 이름입니다. *level0_object_name* 은 **sysname** 기본값은 NULL입니다.  
  
 [ @level1type=] {'*level1_object_type*'을 (를)  
 수준 1 개체의 유형입니다. *level1_object_type* 은 **varchar (128)** 기본값은 NULL입니다. 유효한 입력은 AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION 및 NULL입니다.  
  
 [ @level1name=] {'*level1_object_name*'을 (를)  
 지정된 수준 1 개체 유형의 이름입니다. *level1_object_name* 은 **sysname** 기본값은 NULL입니다.  
  
 [ @level2type=] {'*level2_object_type*'을 (를)  
 수준 2 개체의 유형입니다. *level2_object_type* 은 **varchar (128)** 기본값은 NULL입니다. 유효한 입력은 COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER 및 NULL입니다.  
  
 [ @level2name=] {'*level2_object_name*'을 (를)  
 지정된 수준 2 개체 유형의 이름입니다. *level2_object_name* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 확장 속성을 지정하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 개체는 세 수준(0, 1, 2)으로 분류됩니다. 수준 0은 최고 수준이며 데이터베이스 범위에 포함된 개체로 정의됩니다. 수준 1 개체는 스키마나 USER 범위에 포함되어 있고 수준 2 개체는 수준 1 개체에 포함되어 있습니다. 모든 수준의 개체에 대해 확장 속성을 정의할 수 있습니다. 한 수준에 있는 개체를 참조할 때는 해당 개체를 소유하거나 포함하는 더 높은 수준의 개체 이름을 지정해야 합니다.  
  
 지정 된 유효한 *property_name* 및 *값*, 속성이 업데이트 현재 데이터베이스에 속하는 모든 개체 유형과 이름이 null 인 경우.  
  
## <a name="permissions"></a>Permissions  
 Db_owner 및 db_ddladmin 고정 데이터베이스 역할의 멤버는 예외가 발생 하 여 모든 개체의 확장된 속성을 업데이트할 수 있습니다: db_ddladmin은 데이터베이스 자체 또는 사용자나 역할에 속성을 추가 하지 않을 수 있습니다.  
  
 사용자는 자신이 소유하거나 ALTER 또는 CONTROL 권한이 있는 개체의 확장 속성을 업데이트할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>1. 열의 확장 속성 업데이트  
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
  
### <a name="b-updating-an-extended-property-on-a-database"></a>2. 데이터베이스의 확장 속성 업데이트  
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
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
