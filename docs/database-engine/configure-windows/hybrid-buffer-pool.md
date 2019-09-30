---
title: 하이브리드 버퍼 풀 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
ms.openlocfilehash: 8bbc7670f3a4d6d8a017e7284c5a661d38594f08
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251054"
---
# <a name="hybrid-buffer-pool"></a>하이브리드 버퍼 풀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

하이브리드 버퍼 풀을 사용하면 데이터베이스 엔진이 영구 메모리(PMEM) 디바이스에 저장된 데이터베이스 파일의 데이터 페이지에 직접 액세스할 수 있습니다. 이 기능은 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)]에 도입되었습니다.

PMEM이 없는 기존 시스템에서는 SQL Server가 버퍼 풀에 데이터 페이지를 캐시합니다. 하이브리드 버퍼 풀을 사용하면 SQL Server가 페이지를 버퍼 풀의 DRAM 부분에 복사하는 대신에, PMEM 디바이스에 상주하는 데이터베이스 파일에서 직접 페이지를 액세스합니다. 하이브리드 버퍼 풀에 대한 PMEM 디바이스의 데이터 파일에 대한 읽기 액세스는 PMEM 디바이스의 데이터 페이지로 포인터를 따라 직접 수행됩니다.  

클린 페이지만 PMEM 디바이스에서 직접 액세스할 수 있습니다. 더티로 표시된 페이지는 최종적으로 PMEM 디바이스에 다시 쓰고 다시 클린으로 표시하기 전에 DRAM 버퍼 풀에 복사됩니다. 이 작업은 검사점 작업 중에 이루어집니다. PMEM 디바이스에서 DRAM으로 파일을 복사하는 메커니즘은 직접 메모리 매핑된 I/O(MMIO)이며 SQL Server 내에서 데이터 파일의 *향상 기능*이라고도 합니다.


하이브리드 버퍼 풀 기능은 Windows와 Linux에서 모두 사용할 수 있습니다. PMEM 디바이스는 DAX(DirectAccess)를 지원하는 파일 시스템을 사용하여 포맷해야 합니다. XFS, EXT4 및 NTFS 파일 시스템은 모두 DAX를 지원합니다. SQL Server는 데이터 파일이 적절하게 서식이 지정된 PMEM 디바이스에 상주하는지 자동으로 검색하고, 사용자 공간에서 메모리 매핑을 수행합니다. 이 매핑은 시작할 때, 새 데이터베이스가 연결되거나 복원되거나 만들어졌을 때, 또는 데이터베이스에 대해 하이브리드 버퍼 풀 기능을 사용할 때 발생합니다.

Windows Server에서의 PMEM 지원에 대한 자세한 내용은 [Windows Server에서 영구 메모리 배포](/windows-server/storage/storage-spaces/deploy-pmem/)를 참조하세요.

Linux에서 PMEM 디바이스에 대해 SQL Server를 구성하는 자세한 내용은 [영구 메모리 배포](../../linux/sql-server-linux-configure-pmem.md)를 참조하세요.

## <a name="enable-hybrid-buffer-pool"></a>하이브리드 버퍼 풀 사용

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)]는 하이브리드 버퍼 풀을 제어하기 위한 DDL(동적 데이터 언어)을 도입합니다.

다음 예제에서는 SQL Server의 인스턴스에 대해 하이브리드 버퍼 풀을 사용하도록 설정합니다.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

기본적으로 하이브리드 버퍼 풀은 인스턴스 범위에서 사용하지 않도록 설정됩니다. 설정 변경 내용을 적용하려면 SQL Server 인스턴스를 다시 시작해야 합니다. 서버의 총 PMEM 용량에 해당하는 충분한 해시 페이지 할당을 용이하게 하기 위해 다시 시작이 필요합니다.

다음 예제에서는 특정 데이터베이스에 대해 하이브리드 버퍼 풀을 사용하도록 설정합니다.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

기본적으로 하이브리드 버퍼 풀은 데이터베이스 범위에서 사용하도록 설정됩니다.

## <a name="disable-hybrid-buffer-pool"></a>하이브리드 버퍼 풀을 사용하지 않도록 설정

다음 예제에서는 SQL Server의 인스턴스에 대해 하이브리드 버퍼 풀을 사용하지 않도록 설정합니다.

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

기본적으로 하이브리드 버퍼 풀은 인스턴스 범위에서 사용하지 않도록 설정됩니다. 설정 변경 내용을 적용하려면 SQL Server 인스턴스를 다시 시작해야 합니다. 서버의 PMEM 용량을 고려할 필요가 없으므로 해시 페이지의 초과 할당을 방지하기 위해 다시 시작이 필요합니다.

다음 예제에서는 특정 데이터베이스에 대해 하이브리드 버퍼 풀을 사용하지 않도록 설정합니다.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

기본적으로 하이브리드 버퍼 풀은 데이터베이스 범위에서 사용하도록 설정됩니다.

## <a name="view-hybrid-buffer-pool-configuration"></a>하이브리드 버퍼 풀 구성 보기

다음 예제는 SQL Server의 인스턴스에 대해 하이브리드 버퍼 풀 시스템 구성의 현재 상태를 반환합니다.

```sql
SELECT *
FROM sys.configurations
WHERE
    name = 'hybrid_buffer_pool';
```

다음 예제는 테이블 두 개를 반환합니다.

- 첫 번째 테이블은 SQL Server의 인스턴스에 대한 하이브리드 버퍼 풀 시스템 구성의 현재 상태를 보여줍니다.
- 두 번째 테이블은 데이터베이스 및 하이브리드 버퍼 풀에 대한 데이터베이스 수준 설정(`is_memory_optimized_enabled`)을 나열합니다.

```sql
SELECT * FROM sys.configurations WHERE name = 'hybrid_buffer_pool';

SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>하이브리드 버퍼 풀 모범 사례

16GB RAM 미만인 상태에서 인스턴스에서 하이브리드 버퍼 풀을 할당하지 않는 것이 좋습니다.

Windows에서 PMEM 디바이스를 포맷할 때 NTFS에 가능한 가장 큰 할당 단위 크기(Windows Server 2019에서 2MB)를 사용하고 디바이스에서 DAX(Direct Access)에 적합하게 포맷되었는지 확인합니다.

파일 크기가 2MB의 배수여야 합니다(modulo 2MB가 0이어야 함).

하이브리드 버퍼 풀에 대한 서버 범위 설정이 사용하지 않도록 설정된 경우 어떤 사용자 데이터베이스에서도 하이브리드 버퍼 풀을 사용하지 않습니다.

하이브리드 버퍼에 대한 서버 범위 설정이 사용하도록 설정된 경우 개별 사용자 데이터베이스에 대해 데이터베이스 범위 수준에서 하이브리드 버퍼 풀을 사용하지 않도록 설정하는 단계를 수행하여 해당 사용자 데이터베이스에 대해 하이브리드 버퍼 풀 사용을 사용하지 않도록 설정할 수 있습니다.
