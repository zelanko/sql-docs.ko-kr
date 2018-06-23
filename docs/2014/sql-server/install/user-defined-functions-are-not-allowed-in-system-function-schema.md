---
title: System_function_schema에서 사용자 정의 함수를 허용 되지 않는 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 16c6cf618028d56a3b09cdad8da4cfd9eb9309f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090990"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>system_function_schema에서 사용자 정의 함수가 허용되지 않습니다.
  업그레이드 관리자는 문서화 되지 않은 사용자가 소유 하는 사용자 정의 함수를 발견 했습니다. **system_function_schema**합니다. 이 사용자를 지정해서는 사용자 정의 시스템 함수를 만들 수 없습니다. **system_function_schema** 사용자 이름은 없고이 이름의 연결 된 사용자 ID (UID = 4)에 예약 되어는 **sys** 스키마 있으며 내부 에서만 사용 하도록 제한 됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 시스템 개체 저장소 및 액세스가 다음과 같이 변경되었습니다.  
  
-   시스템 개체의 읽기 전용에 저장 되며 **리소스** 데이터베이스로 전환한 직접 시스템 개체 업데이트는 허용 되지 않습니다.  
  
     시스템 개체에 논리적으로 나타납니다.는 **sys** 모든 데이터베이스의 스키마입니다. 이를 통해 모든 데이터베이스에서 한 부분으로 된 함수 이름을 지정하여 시스템 함수를 호출할 수 있는 기능이 유지됩니다. 예를 들어 모든 데이터베이스에서 `SELECT * FROM fn_helpcollations()` 문을 실행할 수 있습니다.  
  
-   문서화 되지 않은 사용자 **system_function_schema** 제거 되었습니다.  
  
-   ID에 연결 된 사용자 **system_function_schema** (UID = 4)에 예약 되어는 **sys** 스키마 있으며 내부 에서만 사용 하도록 제한 됩니다.  
  
 이러한 변경 사항은 사용자 정의 시스템 함수에 다음과 같은 영향을 줍니다.  
  
-   참조 하는 데이터 정의 언어 (DDL) 문을 **system_function_schema** 실패 합니다. 예를 들어 문을 `CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ... 실패 합니다.  
  
-   로 업그레이드 한 후 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]가 소유한 기존 개체 **system_function_schema** 에 포함 됩니다는 **sys** 의 스키마는 **마스터** 데이터베이스입니다. 시스템 개체는 수정할 수 없으므로 이러한 함수 수 되지 변경 또는 삭제할 수에서 **마스터** 데이터베이스입니다. 또한 이러한 함수는 다른 데이터베이스에서 한 부분으로 된 함수 이름을 지정하여 호출할 수 없습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드하기 전에 다음 태스크를 완료합니다.  
  
1.  기존 사용자 정의 함수를의 소유권을 변경할 **dbo** 를 사용 하 여는 **sp_changeobjectowner** 시스템 저장 프로시저입니다.  
  
2.  'fn_' 접두사를 사용하지 않도록 함수 이름을 변경하는 것이 좋습니다. 이렇게 하면 현재 또는 향후 시스템 함수와의 이름 충돌 가능성을 피할 수 있습니다.  
  
3.  수정된 함수를 사용하는 모든 데이터베이스에 해당 함수의 복사본을 추가합니다.  
  
4.  에 대 한 참조를 대체 **system_function_schema** 와 **dbo** 사용자 정의 함수 DDL 문이 포함 된 모든 스크립트에서 합니다.  
  
5.  중 하나는 두 부분으로 된 이름 dbo *를 사용 하기 위해 이러한 함수를 호출 하는 스크립트를 수정 *. * * * function_name*, 또는 세 부분으로 이루어진 이름 *a s e _ ***.** dbo입니다.* function_name * 합니다.  
  
 자세한 내용은 SQL Server 온라인 설명서에서 다음 항목을 참조하십시오.  
  
-   "sp_changeobjectowner"  
  
-   "사용자와 스키마 분리"  
  
-   "리소스 데이터베이스"  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)   
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [시스템 개체를 수정 하는 문을 제거 합니다.](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [시스템 개체를 삭제 하는 문을 제거 합니다.](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
