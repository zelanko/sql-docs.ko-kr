---
title: sp_settriggerorder (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
caps.latest.revision: "54"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 116c9c8506b5ca09455631ab0cfc3a29cc4d9faa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spsettriggerorder-transact-sql"></a>sp_settriggerorder(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  첫 번째 또는 마지막으로 실행되는 AFTER 트리거를 지정합니다. 첫 번째 트리거와 마지막 트리거 사이에 실행되는 AFTER 트리거는 정의되지 않은 순서로 실행됩니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@triggername=** ] **'**[ *triggerschema***.**] *트리거 이름***'**  
 트리거 및 트리거가 속한 스키마의 이름입니다. 해당되는 경우 이 순서가 설정 또는 변경됩니다. [*triggerschema***.**] *트리거 이름* 은 **sysname**합니다. 이름이 트리거와 일치하지 않거나 INSTEAD OF 트리거와 일치하는 경우에는 프로시저가 오류를 반환합니다. *triggerschema* DDL 또는 logon 트리거에 대해서는 지정할 수 없습니다.  
  
 [ **@order=** ] **'***value***'**  
 트리거의 새 순서 설정입니다. *값* 은 **varchar (10)** 이며 다음 값 중 하나를 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  **첫 번째** 및 **마지막** 트리거는 서로 다른 트리거 여야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**첫째**|트리거가 첫 번째로 실행됩니다.|  
|**마지막**|트리거가 마지막으로 실행됩니다.|  
|**없음**|트리거가 정의되지 않은 순서로 실행됩니다.|  
  
 [  **@stmttype=** ] **'***statement_type***'**  
 트리거를 실행시키는 SQL 문을 지정합니다. *statement_type* 은 **varchar (50)** INSERT, UPDATE, DELETE, LOGON 또는 모두 일 수 있습니다 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 이벤트에 나열 된 [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)합니다. 이벤트 그룹은 지정할 수 없습니다.  
  
 트리거로 지정할 수는 **첫 번째** 또는 **마지막** 해당 트리거를 해당 문 유형의 트리거로 정의 된 후에 문 형식에 대 한 트리거. 예를 들어 트리거 **TR1** 지정 될 수 있습니다 **첫 번째** 테이블에 삽입을 위한 **T1** 경우 **TR1** INSERT 트리거로 정의 됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 경우 오류가 반환 **TR1**로 설정 되어 있는 정의한를 INSERT 트리거로는 **첫 번째**, 또는 **마지막**, UPDATE 문에 대 한 트리거. 자세한 내용은 주의 섹션을 참조하세요.  
  
 **@namespace=** { **'DATABASE'** | **'SERVER'** | NULL}  
 때 *트리거 이름* 이 DDL 트리거인 경우  **@namespace**  지정 여부 *트리거 이름* 이 데이터베이스 범위 또는 서버 범위에서 생성 합니다. 경우 *트리거 이름* 이 로그온 트리거인 경우 서버를 지정 해야 합니다. DDL 트리거 범위에 대 한 자세한 내용은 참조 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)합니다. 지정 하지 않거나 NULL을 지정 하는 경우 *트리거 이름* 은 DML 트리거입니다.  
  
||  
|-|  
|서버에 적용: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>주의  
  
## <a name="dml-triggers"></a>DML 트리거  
 하나만 있을 수 있습니다 **첫 번째** 하나의 **마지막** 단일 테이블에서 각 문에 대 한 트리거.  
  
 경우는 **첫 번째** 트리거는 테이블, 데이터베이스 또는 서버에 이미 정의 된, 새 트리거를 지정할 수 없습니다 **첫 번째** 동일한 테이블, 데이터베이스 또는 서버에서 같은 대 한 *statement_type* . 이러한 제한도 적용 됩니다. **마지막** 트리거.  
  
 복제 시 즉시 업데이트 구독이나 지연 업데이트 구독에 포함된 테이블에 대해 첫 번째 트리거가 자동으로 생성됩니다. 복제의 트리거는 첫 번째 트리거여야 합니다. 첫 번째 트리거가 있는 테이블을 즉시 업데이트 구독이나 지연 업데이트 구독에 포함시키면 복제 시 오류가 발생합니다. 테이블이 구독에 포함된 후 트리거를 첫 번째 트리거로 만들려고 하면 **sp_settriggerorder** 에서 오류가 반환됩니다. 복제 트리거에 ALTER TRIGGER를 사용 하거나 사용 하기 **sp_settriggerorder** 복제 트리거를 변경 하는 **마지막** 또는 **None** 트리거 구독 않습니다 제대로 작동 하지 않습니다.  
  
## <a name="ddl-triggers"></a>DDL 트리거  
 데이터베이스 범위의 DDL 트리거와 서버 범위의 DDL 트리거는 동일한 이벤트에 존재 하는 경우 두 트리거 지정할 수 있습니다는 **첫 번째** 트리거 또는 **마지막** 트리거. 그러나 서버 범위 트리거가 항상 먼저 실행됩니다. 일반적으로 같은 이벤트에 있는 DDL 트리거의 실행 순서는 다음과 같습니다.  
  
1.  표시 된 서버 수준 트리거 **첫 번째**합니다.  
  
2.  다른 서버 수준 트리거  
  
3.  표시 된 서버 수준 트리거 **마지막**합니다.  
  
4.  표시 된 데이터베이스 수준 트리거 **첫 번째**합니다.  
  
5.  다른 데이터베이스 수준 트리거  
  
6.  표시 된 데이터베이스 수준 트리거 **마지막**합니다.  
  
## <a name="general-trigger-considerations"></a>일반적인 트리거 고려 사항  
 ALTER TRIGGER 문에서 첫 번째 트리거나 마지막 트리거가 변경 되 면는 **첫 번째** 또는 **마지막** 트리거에 설정 되었던 특성은 삭제 되며 값으로 대체 됩니다 **None**합니다. 순서 값을 사용 하 여 다시 설정 해야 **sp_settriggerorder**합니다.  
  
 동일한 트리거는 둘 이상의 문 유형에 대 한 첫 번째 또는 마지막 순서로 지정 해야 하는 경우 **sp_settriggerorder** 각 문 유형에 대해 실행 해야 합니다. 또한 트리거가 먼저 먼저 정의 해야 문 유형에 대해로 지정할 수는 **첫 번째** 또는 **마지막** 트리거를 해당 문 유형에 대해 발생 합니다.  
  
## <a name="permissions"></a>Permissions  
 서버 범위(ON ALL SERVER)의 DDL 트리거 또는 로그온 트리거의 순서를 설정하려면 CONTROL SERVER 권한이 필요합니다.  
  
 데이터베이스 범위(ON DATABASE)의 DDL 트리거 순서를 설정하려면 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
 DML 트리거의 순서를 설정하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>1. DML 트리거의 실행 순서 설정  
 다음 예에서는 `uSalesOrderHeader` 트리거를 `UPDATE` 테이블에서 `Sales.SalesOrderHeader` 작업이 발생한 후 실행되는 첫 번째 트리거로 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>2. DML 트리거의 실행 순서 설정  
 다음 예에서는 `ddlDatabaseTriggerLog` 트리거를 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `ALTER_TABLE` 이벤트가 발생한 후 실행되는 첫 번째 트리거로 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
