---
title: SQL Server, User Settable 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- User Settable object
- SQLServer:User Settable
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cb3c412361acf4e3c059f902c2fc0ae498601d36
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522988"
---
# <a name="sql-server-user-settable-object"></a>SQL Server, User Settable 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft **의** User Settable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 사용하면 사용자 지정 카운터 인스턴스를 만들 수 있습니다. 사용자 지정 카운터 인스턴스를 사용하여 사용자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 고유한 구성 요소 같이 기존 카운터로 모니터링할 수 없는 서버 측면(예: 로그된 고객의 주문 수나 제품 정보)를 모니터링할 수 있습니다.  
  
 **User Settable** 개체는 **사용자 카운터 1** 에서 **사용자 카운터 10**까지 10개의 쿼리 카운터 인스턴스를 가집니다. 이러한 카운터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 **sp_user_counter1** 에서 **sp_user_counter10**까지 매핑됩니다. 사용자 애플리케이션에서 이러한 저장 프로시저를 실행할 때 저장 프로시저로 설정된 값이 시스템 모니터에 표시됩니다. 카운터는 특정 제품에 대한 주문이 하루에 발생하는 횟수를 계산하는 저장 프로시저와 같은 모든 단일 정수 값을 모니터링할 수 있습니다.  
  
> [!NOTE]  
>  사용자 카운터 저장 프로시저는 시스템 모니터에서 자동으로 폴링되지 않습니다. 사용자 애플리케이션에서 업데이트할 카운터 값에 대해 명시적으로 실행해야 합니다. 트리거를 사용하여 카운터 값을 자동으로 업데이트할 수 있습니다. 예를 들어 테이블에 있는 행 수를 모니터링하는 카운터를 만들려면 테이블에 `SELECT COUNT(*) FROM table`문을 실행하는 INSERT 및 DELETE 트리거를 만드십시오. INSERT나 DELETE 작업이 테이블에서 수행되어 트리거가 시작될 때마다 시스템 모니터 카운터가 자동으로 업데이트됩니다.  
  
 이 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **User Settable** 개체에 대해 설명합니다.  
  
|SQL Server User Settable 카운터|설명|  
|---------------------------------------|-----------------|  
|**쿼리**|**User Settable** 개체는 쿼리 카운터를 포함합니다. 사용자는 쿼리 개체에서 **사용자 카운터** 를 구성합니다.|  
  
 이 표에서는 **Query** 카운터의 **인스턴스** 에 대해 설명합니다.  
  
|쿼리 카운터 인스턴스|설명|  
|-----------------------------|-----------------|  
|**사용자 카운터 1**|**sp_user_counter1**을 사용하여 정의합니다.|  
|**사용자 카운터 2**|**sp_user_counter2**를 사용하여 정의합니다.|  
|**사용자 카운터 3**|**sp_user_counter3**을 사용하여 정의합니다.|  
|...||  
|**사용자 카운터 10**|**sp_user_counter10**을 사용하여 정의합니다.|  
  
 사용자 카운터 저장 프로시저를 이용하려면 새 카운터 값을 나타내는 하나의 정수로 된 매개 변수로 애플리케이션을 실행하십시오. 예를 들어 **사용자 카운터 1** 에 10이라는 값을 설정하려면 다음 Transact-SQL 문을 실행하세요.  
  
```  
EXECUTE sp_user_counter1 10  
```  
  
 사용자 카운터 저장 프로시저는 사용자 고유의 저장 프로시저와 같은 다른 저장 프로시저를 호출할 수 있는 곳 어디서나 호출할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작한 후의 연결 횟수와 연결 시도 횟수를 계산하는 다음과 같은 저장 프로시저를 만들 수도 있습니다.  
  
```  
DROP PROC My_Proc  
GO  
CREATE PROC My_Proc  
AS   
   EXECUTE sp_user_counter1 @@CONNECTIONS  
GO  
```  
  
 @@CONNECTIONS 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작한 후의 연결 및 연결 시도 횟수를 반환합니다. 이 값은 **sp_user_counter1** 저장 프로시저에 매개 변수로 전달됩니다.  
  
> [!IMPORTANT]  
>  사용자 카운터 저장 프로시저에서 정의한 쿼리는 가능한 한 단순한 것이 좋습니다. I/O를 많이 사용하는 실제 배열, 해시 작업 또는 쿼리를 실행하는 메모리 집중형 쿼리는 실행하는 데 비용이 많이 들며 성능에도 영향을 미칩니다.  
  
## <a name="permissions"></a>Permissions  
 **sp_user_counter** 는 모든 사용자에 대해 사용할 수 있지만 쿼리 카운터로 제한될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
