---
title: TRIGGER_NESTLEVEL (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRIGGER_NESTLEVEL
- TRIGGER_NESTLEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- triggers [SQL Server], number executed
- number of triggers
- TRIGGER_NESTLEVEL function
ms.assetid: 6a33e74a-0cf9-4ae1-a1e4-4a137a3ea39d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0416b80079ac4c1dfb6dc10b507fd85800dd3a27
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="triggernestlevel-transact-sql"></a>TRIGGER_NESTLEVEL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  트리거를 발생시킨 문에 대해 실행된 트리거의 수를 반환합니다. TRIGGER_NESTLEVEL는 DML 및 DDL 트리거에서 현재 중첩 수준을 확인하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
## <a name="arguments"></a>인수  
 *object_id*  
 트리거의 개체 ID입니다. 경우 *object_id* 지정 된 문이 반환에 대 한 지정한 트리거의 실행 된 횟수입니다. 경우 *object_id* 을 지정 하지 않으면 문이 반환에 대 한 모든 트리거 실행 된 횟수입니다.  
  
 **'** *trigger_type* **'**  
 TRIGGER_NESTLEVEL을 AFTER 트리거에 적용할지 아니면 INSTEAD OF 트리거에 적용할지를 지정합니다. 지정 **AFTER** AFTER 트리거에 합니다. 지정 **IOT** INSTEAD OF 트리거에 대 한 합니다. 경우 *trigger_type* 지정 된 *trigger_event_category* 도 지정 해야 합니다.  
  
 **'** *trigger_event_category* **'**  
 TRIGGER_NESTLEVEL을 DML 또는 DDL 트리거 중 어디에 적용할지를 지정합니다. 지정 **DML** DML 트리거에 대 한 합니다. 지정 **DDL** DDL 트리거에 대 한 합니다. 경우 *trigger_event_category* 지정 된 *trigger_type* 도 지정 해야 합니다. 만 **AFTER** 지정 될 수 있습니다 **DDL**이므로 DDL 트리거는 AFTER 트리거만 될 수 있습니다.  
  
## <a name="remarks"></a>주의  
 매개 변수를 지정하지 않은 경우 TRIGGER_NESTLEVEL은 호출 스택에 있는 총 트리거 수를 반환합니다. 여기에는 해당 트리거도 포함됩니다. 트리거가 다른 트리거를 발생시키면서 명령을 실행하거나 트리거를 연속적으로 발생시키는 경우 매개 변수를 생략할 수 있습니다.  
  
 특정 트리거 형식 및 이벤트 범주에 대 한 호출 스택에 있는 총 트리거 수를 반환 하려면 지정 *object_id* = 0.  
  
 TRIGGER_NESTLEVEL는 트리거 밖에서 실행되고 모든 매개 변수가 NULL이 아닌 경우 0을 반환합니다.  
  
 명시적으로 NULL로 지정된 매개 변수가 있는 경우 TRIGGER_NESTLEVEL가 사용된 위치가 트리거 내부이든 외부이든 관계없이 NULL이 반환됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>1. 특정 DML 트리거의 중첩 수준 테스트  
  
```  
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>2. 특정 DML 트리거의 중첩 수준 테스트  
  
```  
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>3. 실행한 모든 트리거의 중첩 수준 테스트  
  
```  
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
