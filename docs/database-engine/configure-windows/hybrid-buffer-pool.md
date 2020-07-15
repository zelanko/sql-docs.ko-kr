---
title: 하이브리드 버퍼 풀 | Microsoft Docs
description: 하이브리드 버퍼 풀이 메모리 버스를 통해 영구 메모리 장치에 액세스하게 하는 방법을 확인합니다. 이 SQL Server 2019 기능을 설정하거나 해제하고 모범 사례를 확인합니다.
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: 73f4abc0c1b2a7cd6943ab6b216133812c145d19
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772425"
---
# <a name="hybrid-buffer-pool"></a>하이브리드 버퍼 풀
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

하이브리드 버퍼 풀을 사용하면 버퍼 풀 개체가 휘발성 DRAM에 캐시된 데이터 페이지의 복사본 대신, PMEM(영구 메모리) 디바이스에 있는 데이터베이스 파일의 데이터 페이지를 참조할 수 있습니다. 이 기능은 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)]에 도입되었습니다.

![하이브리드 버퍼 풀](./media/hybrid-buffer-pool.png)

PMEM(영구 메모리) 디바이스는 바이트 주소를 지정할 수 있으며, DAX(직접 액세스) 영구 메모리 인식 파일 시스템(예: XFS, EXT4 또는 NTFS)을 사용하는 경우 OS의 일반적인 파일 시스템 API를 통해 파일 시스템의 파일에 액세스할 수 있습니다. 또는 디바이스에 있는 파일의 메모리 맵에 대해 로드 및 저장 작업을 수행할 수 있습니다. 이렇게 하면 SQL Server 등의 PMEM 인식 애플리케이션에서 기존의 스토리지 스택을 트래버스하지 않고 디바이스의 파일에 액세스할 수 있습니다.

하이브리드 버퍼 풀은 이 기능을 사용하여 메모리 매핑된 파일에 대해 로드 및 저장 작업을 수행하고, PMEM 디바이스를 버퍼 풀의 캐시와 데이터베이스 파일 저장에 활용합니다. 이 경우 논리적 읽기와 물리적 읽기가 근본적으로 동일한 작업을 수행하는 고유한 상황이 생성됩니다. 영구 메모리 디바이스는 일반 휘발성 DRAM처럼 메모리 버스를 통해 액세스할 수 있습니다.

클린 데이터 페이지만 디바이스의 하이브리드 버퍼 풀에 대해 캐시됩니다. 더티로 표시된 페이지는 DRAM 버퍼 풀에 복사된 후에 최종적으로 PMEM 디바이스에 다시 쓰고 다시 클린으로 표시됩니다. 이 작업은 표준 블록 디바이스의 경우와 비슷한 방식으로 일반 검사점 작업 중에 수행됩니다.

하이브리드 버퍼 풀 기능은 Windows와 Linux에서 모두 사용할 수 있습니다. PMEM 디바이스는 DAX(DirectAccess)를 지원하는 파일 시스템을 사용하여 포맷해야 합니다. XFS, EXT4 및 NTFS 파일 시스템은 모두 DAX를 지원합니다. SQL Server는 데이터 파일이 적절히 포맷된 PMEM 디바이스에 있는지를 자동으로 탐지하고, 새 데이터베이스가 연결, 복원 또는 생성된 경우 시작 시 데이터베이스 파일의 메모리 매핑을 수행합니다.

자세한 내용은 다음을 참조하세요.

* [영구 메모리 이해 및 배포(Windows)](/windows-server/storage/storage-spaces/deploy-pmem/)
* [SQL Server on Linux의 PMEM(영구 메모리) 구성](../../linux/sql-server-linux-configure-pmem.md)


## <a name="enable-hybrid-buffer-pool"></a>하이브리드 버퍼 풀 사용

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)]는 하이브리드 버퍼 풀을 제어하기 위한 DDL(동적 데이터 언어)을 도입합니다.

다음 예제에서는 SQL Server의 인스턴스에 대해 하이브리드 버퍼 풀을 사용하도록 설정합니다.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

기본적으로 하이브리드 버퍼 풀은 인스턴스 범위에서 사용하지 않도록 설정되어 있습니다. 설정 변경 내용을 적용하려면 SQL Server 인스턴스를 다시 시작해야 합니다. 서버의 총 PMEM 용량에 해당하는 충분한 해시 페이지 할당을 용이하게 하기 위해 다시 시작이 필요합니다.

다음 예제에서는 특정 데이터베이스에 대해 하이브리드 버퍼 풀을 사용하도록 설정합니다.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

기본적으로 하이브리드 버퍼 풀은 데이터베이스 범위에서 사용하도록 설정되어 있습니다.

## <a name="disable-hybrid-buffer-pool"></a>하이브리드 버퍼 풀을 사용하지 않도록 설정

다음 예제에서는 인스턴스 수준에서 하이브리드 버퍼 풀을 사용하지 않도록 설정합니다.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

기본적으로 하이브리드 버퍼 풀은 인스턴스 수준에서 사용하지 않도록 설정되어 있습니다. 이 변경 내용을 적용하려면 인스턴스를 다시 시작해야 합니다. 이렇게 하면 서버의 PMEM 용량을 고려해야 하므로 버퍼 풀에 충분한 해시 페이지가 할당됩니다.

다음 예제에서는 특정 데이터베이스에 대해 하이브리드 버퍼 풀을 사용하지 않도록 설정합니다.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

기본적으로 하이브리드 버퍼 풀은 데이터베이스 범위에서 사용하도록 설정되어 있습니다.

## <a name="view-hybrid-buffer-pool-configuration"></a>하이브리드 버퍼 풀 구성 보기

다음 예제에서는 인스턴스의 현재 하이브리드 버퍼 풀 구성 상태를 반환합니다.

```sql
SELECT * FROM
sys.server_memory_optimized_hybrid_buffer_pool_configuration;
```

다음 예제에서는 데이터베이스와 하이브리드 버퍼 풀의 데이터베이스 수준 설정(`is_memory_optimized_enabled`)을 나열합니다.

```sql
SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>하이브리드 버퍼 풀 모범 사례

 - Windows에서 PMEM 디바이스를 포맷할 때 NTFS에 가능한 가장 큰 할당 단위 크기(Windows Server 2019에서 2MB)를 사용하고 디바이스에서 DAX(Direct Access)에 적합하게 포맷되었는지 확인합니다.

 - Windows에서 [메모리의 잠긴 페이지](./enable-the-lock-pages-in-memory-option-windows.md)를 사용합니다.

 - 파일 크기가 2MB의 배수여야 합니다(modulo 2MB가 0이어야 함).

 - 하이브리드 버퍼 풀의 서버 범위 설정을 사용하지 않도록 설정한 경우에는 모든 사용자 데이터베이스에서 이 기능이 사용되지 않습니다.

 - 하이브리드 버퍼 풀의 서버 범위 설정을 사용하도록 설정한 경우, 데이터베이스 범위 설정을 사용하여 개별 사용자 데이터베이스에 대해 기능을 해제할 수 있습니다.
