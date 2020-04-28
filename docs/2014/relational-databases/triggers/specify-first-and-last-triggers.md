---
title: 첫 번째 및 마지막 트리거 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a851a19a7f00afd055bb2ee8f00eaf4621a1e98f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62524139"
---
# <a name="specify-first-and-last-triggers"></a>첫 번째 및 마지막 트리거 지정
  테이블과 연결된 AFTER 트리거 중 하나를 각 INSERT, DELETE 및 UPDATE 트리거 동작에 대한 첫 번째 AFTER 트리거나 마지막 AFTER 트리거로 지정할 수 있습니다. 첫 번째 트리거와 마지막 트리거 사이에 실행되는 AFTER 트리거는 정의되지 않은 순서로 실행됩니다.  
  
 AFTER 트리거의 순서를 지정하려면 **sp_settriggerorder** 저장 프로시저를 사용합니다. **sp_settriggerorder** 에는 다음과 같은 옵션이 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**첫째**|DML 트리거를 트리거 동작에 대해 실행할 첫 번째 AFTER 트리거로 지정합니다.|  
|**마지막**|DML 트리거를 트리거 동작에 대해 실행할 마지막 AFTER 트리거로 지정합니다.|  
|**없음**|DML 트리거가 실행되는 특정 순서가 없음을 지정합니다. 주로 첫 번째 트리거나 마지막 트리거를 다시 설정하는 데 사용됩니다.|  
  
 다음 예에서는 **sp_settriggerorder**를 사용하는 방법을 보여 줍니다.  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  첫 번째 트리거와 마지막 트리거는 서로 다른 DML 트리거여야 합니다.  
  
 한 테이블에 INSERT, UPDATE 및 DELETE 트리거를 동시에 정의할 수 있습니다. 문 유형마다 자체의 첫 번째 트리거와 마지막 트리거가 있을 수 있지만 두 트리거가 서로 달라야 합니다.  
  
 테이블에 정의된 첫 번째 트리거나 마지막 트리거가 FOR UPDATE, FOR DELETE 또는 FOR INSERT에 적용되지 않는 경우와 같이 특정 트리거 동작에 적용되지 않으면 이렇게 누락된 작업에 대한 첫 번째 트리거나 마지막 트리거는 없습니다.  
  
 첫 번째 트리거나 마지막 트리거로 INSTEAD OF 트리거를 지정할 수 없습니다. INSTEAD OF 트리거는 기본 테이블이 업데이트되기 전에 시작됩니다. 기본 테이블이 INSTEAD OF 트리거에 의해 업데이트될 경우 테이블에 정의된 AFTER 트리거가 실행되기 전에 업데이트가 수행됩니다. 예를 들어 뷰의 INSTEAD OF INSERT 트리거가 기본 테이블에 데이터를 삽입하고 기본 테이블 자체에 한 개의 INSTEAD OF INSERT 트리거와 세 개의 AFTER INSERT 트리거가 있는 경우 삽입 동작 대신 기본 테이블의 INSTEAD OF INSERT 트리거가 실행되고 기본 테이블의 AFTER 트리거는 기본 테이블의 삽입 작업 후에 실행됩니다. 자세한 내용은 [DML Triggers](dml-triggers.md)을 참조하세요.  
  
 ALTER TRIGGER 문에 의해 첫 번째 트리거나 마지막 트리거가 변경되는 경우 **첫 번째** 나 **마지막** 특성이 삭제되고 순서 값은 **없음**으로 설정됩니다. 순서는 **sp_settriggerorder**를 사용하여 다시 설정해야 합니다.  
  
 OBJECTPROPERTY 함수의 **ExecIsFirstTrigger** 및 **ExecIsLastTrigger**속성을 통해 트리거가 첫 번째 트리거인지 또는 마지막 트리거인지 알 수 있습니다.  
  
 복제 시 즉시 업데이트 구독이나 지연 업데이트 구독에 포함된 테이블에 대해 첫 번째 트리거가 자동으로 생성됩니다. 복제의 트리거는 첫 번째 트리거여야 합니다. 첫 번째 트리거가 있는 테이블을 즉시 업데이트 구독이나 지연 업데이트 구독에 포함시키면 복제 시 오류가 발생합니다. 테이블이 구독에 포함된 후 트리거를 첫 번째 트리거로 만들려고 하면 **sp_settriggerorder** 에서 오류가 반환됩니다. 복제 트리거에 ALTER를 사용하거나 **sp_settriggerorder** 를 사용하여 복제 트리거를 마지막 트리거나 없음 트리거로 변경하면 구독이 제대로 작동하지 않게 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/objectpropertyex-transact-sql)   
 [sp_settriggerorder&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql)  
  
  
