---
title: sp_settriggerorder (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ad5239e2761ed1cc788f7826a054ac0e038d9e79
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824298"
---
# <a name="sp_settriggerorder-transact-sql"></a>sp_settriggerorder(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  첫 번째 또는 마지막으로 실행되는 AFTER 트리거를 지정합니다. 첫 번째 트리거와 마지막 트리거 사이에 실행되는 AFTER 트리거는 정의되지 않은 순서로 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>인수  
`[ @triggername = ] '[ _triggerschema.] _triggername'`트리거의 이름 및 트리거가 속한 스키마 (해당 하는 경우)를 설정 하거나 변경할 수 있는 스키마입니다. [_triggerschema_**.**] *triggername* 는 **sysname**입니다. 이름이 트리거와 일치하지 않거나 INSTEAD OF 트리거와 일치하는 경우에는 프로시저가 오류를 반환합니다. DDL 또는 logon 트리거에 대해 *triggerschema* 를 지정할 수 없습니다.  
  
`[ @order = ] 'value'`트리거의 새 순서에 대 한 설정입니다. *값* 은 **varchar (10)** 이며 다음 값 중 하나일 수 있습니다.  
  
> [!IMPORTANT]  
>  **첫 번째** 트리거와 **마지막** 트리거는 서로 다른 두 트리거 여야 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**기본**|트리거가 첫 번째로 실행됩니다.|  
|**마지막**|트리거가 마지막으로 실행됩니다.|  
|**없음**|트리거가 정의되지 않은 순서로 실행됩니다.|  
  
`[ @stmttype = ] 'statement_type'`트리거를 실행 하는 SQL 문을 지정 합니다. *statement_type* 는 **varchar (50)** 이며 [!INCLUDE[tsql](../../includes/tsql-md.md)] [DDL 이벤트](../../relational-databases/triggers/ddl-events.md)에 나열 된 INSERT, UPDATE, DELETE, LOGON 또는 statement 이벤트 일 수 있습니다. 이벤트 그룹은 지정할 수 없습니다.  
  
 트리거를 문 형식에 대 한 트리거로 정의한 후에만 트리거를 문 형식에 대 한 **첫 번째** 또는 **마지막** 트리거로 지정할 수 있습니다. 예를 들어 **tr1** 이 insert 트리거로 정의 된 **경우 Tr1 트리거** 는 **T1** 테이블에서 insert에 대해 **처음** 으로 지정할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]INSERT 트리거로만 정의 된 **TR1**이 UPDATE 문의 **First**또는 **Last**트리거로 설정 된 경우는 오류를 반환 합니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
 ** \@ namespace =** { **' DATABASE '**  |  **' SERVER '** | N  
 *Triggername* 가 DDL 트리거 이면 ** \@ 네임 스페이스** 는 데이터베이스 범위 또는 서버 범위를 사용 하 여 *triggername* 를 만들었는지 여부를 지정 합니다. *Triggername* 가 logon 트리거 이면 서버를 지정 해야 합니다. DDL 트리거 범위에 대 한 자세한 내용은 [Ddl 트리거](../../relational-databases/triggers/ddl-triggers.md)를 참조 하세요. 지정 하지 않거나 NULL을 지정 하면 *triggername* 는 DML 트리거입니다.  
  
||  
|-|  
|서버 적용 대상: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 및 1(실패)  
  
## <a name="remarks"></a>설명  
  
## <a name="dml-triggers"></a>DML 트리거  
 단일 테이블의 각 문에 대해 **첫 번째** 트리거와 **마지막** 트리거 중 하나만 있을 수 있습니다.  
  
 테이블, 데이터베이스 또는 서버에 **첫 번째** 트리거가 이미 정의 되어 있는 경우 동일한 *statement_type*에 대해 동일한 테이블, 데이터베이스 또는 서버에 대해 새 트리거를 **먼저** 지정할 수 없습니다. 이 제한 사항은 **마지막** 트리거도 적용 됩니다.  
  
 복제 시 즉시 업데이트 구독이나 지연 업데이트 구독에 포함된 테이블에 대해 첫 번째 트리거가 자동으로 생성됩니다. 복제의 트리거는 첫 번째 트리거여야 합니다. 첫 번째 트리거가 있는 테이블을 즉시 업데이트 구독이나 지연 업데이트 구독에 포함시키면 복제 시 오류가 발생합니다. 테이블이 구독에 포함된 후 트리거를 첫 번째 트리거로 만들려고 하면 **sp_settriggerorder** 에서 오류가 반환됩니다. 복제 트리거에서 ALTER TRIGGER를 사용 하거나 **sp_settriggerorder** 를 사용 하 여 복제 트리거를 **마지막** 또는 **없음** 트리거로 변경 하면 구독이 제대로 작동 하지 않습니다.  
  
## <a name="ddl-triggers"></a>DDL 트리거  
 데이터베이스 범위가 있는 ddl 트리거와 서버 범위가 있는 DDL 트리거가 동일한 이벤트에 존재 하는 경우 두 트리거가 **첫 번째** 트리거나 **마지막** 트리거로 지정할 수 있습니다. 그러나 서버 범위 트리거가 항상 먼저 실행됩니다. 일반적으로 같은 이벤트에 있는 DDL 트리거의 실행 순서는 다음과 같습니다.  
  
1.  **First**로 표시 된 서버 수준 트리거입니다.  
  
2.  다른 서버 수준 트리거  
  
3.  **Last**로 표시 된 서버 수준 트리거입니다.  
  
4.  **First**로 표시 된 데이터베이스 수준 트리거입니다.  
  
5.  다른 데이터베이스 수준 트리거  
  
6.  **Last**로 표시 된 데이터베이스 수준 트리거입니다.  
  
## <a name="general-trigger-considerations"></a>일반적인 트리거 고려 사항  
 ALTER TRIGGER 문에서 첫 번째 트리거나 마지막 트리거를 변경 하면 원래 트리거에 설정 된 **첫 번째** 또는 **마지막** 특성이 삭제 되 고 값은 **None**으로 바뀝니다. **Sp_settriggerorder**를 사용 하 여 순서 값을 다시 설정 해야 합니다.  
  
 둘 이상의 문 형식에 대해 동일한 트리거를 첫 번째 또는 마지막 순서로 지정 해야 하는 경우 각 문 형식에 대해 **sp_settriggerorder** 를 실행 해야 합니다. 또한 트리거를 해당 문 형식에 대해 실행할 **첫 번째** 트리거나 **마지막** 트리거로 지정할 수 있으려면 먼저 문 형식에 대해 트리거를 먼저 정의 해야 합니다.  
  
## <a name="permissions"></a>권한  
 서버 범위(ON ALL SERVER)의 DDL 트리거 또는 로그온 트리거의 순서를 설정하려면 CONTROL SERVER 권한이 필요합니다.  
  
 데이터베이스 범위(ON DATABASE)의 DDL 트리거 순서를 설정하려면 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
 DML 트리거의 순서를 설정하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. DML 트리거의 실행 순서 설정  
 다음 예에서는 `uSalesOrderHeader` 트리거를 `UPDATE` 테이블에서 `Sales.SalesOrderHeader` 작업이 발생한 후 실행되는 첫 번째 트리거로 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>B. DML 트리거의 실행 순서 설정  
 다음 예에서는 `ddlDatabaseTriggerLog` 트리거를 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 `ALTER_TABLE` 이벤트가 발생한 후 실행되는 첫 번째 트리거로 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
