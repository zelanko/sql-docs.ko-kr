---
title: ADR 미리 할당 인수 구성 옵션 | Microsoft Docs
description: ADR 미리 할당 인수의 SQL Server 인스턴스 구성 설정에 대해 설명합니다.
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR Preallocation Factor
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4e53c7c9d0d128c1697a301fc013469f5ac34c00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85698175"
---
# <a name="adr-preallocation-factor-configuration-option"></a>ADR 미리 할당 인수 구성 옵션

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019에서 도입되었습니다.

이 구성 설정은 [가속 데이터베이스 복구](../../relational-databases/accelerated-database-recovery-concepts.md)에 필요합니다.

ADR(가속 데이터베이스 복구)은 복구를 위해 데이터 버전을 유지 관리합니다. 이러한 버전은 다양한 DML(데이터 조작 언어) 작업의 일부로 생성됩니다. 버전은 PVS(영구 버전 저장소)라는 내부 테이블에 저장됩니다. 

## <a name="remarks"></a>설명  

포그라운드 사용자 DML 작업의 일부로 PVS 테이블에 페이지가 할당되면 성능이 저하될 수 있습니다. 이를 해결하기 위해 페이지를 미리 할당하고 DML 트랜잭션에 쉽게 사용할 수 있도록 유지하는 백그라운드 스레드가 있습니다. 백그라운드 스레드가 충분한 페이지를 미리 할당하고 포그라운드 PVS 할당의 백분율이 0에 근접하는 경우 성능이 가장 좋습니다. 이 백분율이 높고 성능에 영향을 주는 경우 오류 로그에 태그 `PreallocatePVS`가 표시된 항목이 포함됩니다.

백그라운드 스레드가 미리 할당하는 페이지 수는 다양한 워크로드 추론을 기반으로 하지만 주로 512페이지 청크로 페이지를 할당합니다. ADR 미리 할당 인수는 청크의 배수입니다. 기본적으로 이 인수는 4입니다. 즉, 필요한 경우 한 번에 2,048페이지를 미리 할당합니다. 

백그라운드 스레드는 워크로드 패턴을 고려하지만, 필요한 경우 성능을 향상시키기 위해 이 인수를 증가시킬 수 있습니다.

> [!CAUTION]
> PVS 미리 할당이 너무 많이 증가하는 경우 시스템의 다른 할당과 경합하게 되며 실제로 전체 성능을 저하시킬 수 있습니다.
>
> 이 설정을 수정하기 전에 시스템 전반의 성능을 테스트합니다.

## <a name="examples"></a>예제  

다음 예제에서는 미리 할당 인수를 4로 설정합니다.

```tsql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO 
sp_configure 'ADR Preallocation Factor', 4;
RECONFIGURE;
GO
```

## <a name="see-also"></a>참고 항목  

- [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [가속 데이터베이스 복구](../../relational-databases/accelerated-database-recovery-concepts.md)
- [가속 데이터베이스 복구 관리](../../relational-databases/accelerated-database-recovery-management.md)