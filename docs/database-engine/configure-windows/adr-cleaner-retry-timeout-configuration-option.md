---
title: " ADR 클리너 다시 시도 시간 제한(분) 구성 옵션 | Microsoft Docs"
description: ADR 클리너 다시 시도 시간 제한을 위한 SQL Server 인스턴스 구성 설정에 대해 설명합니다.
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR cleaner retry timeout (min)
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 25d7df032b0606a324d98d14258cbbd40602bae7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85698161"
---
# <a name="adr-cleaner-retry-timeout-min-configuration-option"></a>ADR 클리너 다시 시도 시간 제한(분) 구성 옵션

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019에서 도입되었습니다.

이 구성 설정은 [가속 데이터베이스 복구](../../relational-databases/accelerated-database-recovery-concepts.md)에 필요합니다. 클리너는 정기적으로 절전 모드를 해제하고 필요하지 않은 페이지 버전을 정리하는 비동기 프로세스입니다.

경우에 따라 클리너가 비우기를 수행하는 도중 사용자 워크로드와의 충돌로 인해 개체 수준 잠금을 획득할 때 문제가 발생할 수 있습니다. 클리너는 별도의 목록에서 이러한 페이지를 추적합니다. ADR 클리너 다시 시도 시간 제한(기본값 15)은 비우기 중단 전에 페이지의 개체 잠금 획득 및 정리를 배타적으로 다시 시도하는 데 소요되는 시간을 제어합니다. 중단된 트랜잭션 맵에서 중단된 트랜잭션을 계속 증가시키려면 100% 성공으로 비우기를 완료해야 합니다. 지정된 시간 제한 내에 별도 목록을 정리할 수 없는 경우 현재 비우기가 중단되고 다음 비우기가 시작됩니다.

## <a name="remarks"></a>설명  

클리너는 SQL Server 2019에서 단일 스레드이므로 SQL Server 인스턴스 하나는 한 번에 하나의 데이터베이스에서 작동할 수 있습니다. ADR을 사용하도록 설정된 사용자 데이터베이스가 인스턴스에 두 개 이상 있는 경우 시간 제한을 큰 값으로 늘리지 마세요. 한 데이터베이스에서 다시 시도가 수행되는 동안 다른 데이터베이스에서 정리가 지연될 수 있습니다.

## <a name="examples"></a>예제

다음 예제는 클리너 다시 시도 시간 제한을 설정합니다.

```tsql
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'ADR cleaner retry timeout', 15;  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>참고 항목  

- [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [가속 데이터베이스 복구](../../relational-databases/accelerated-database-recovery-concepts.md)
- [가속 데이터베이스 복구 관리](../../relational-databases/accelerated-database-recovery-management.md)