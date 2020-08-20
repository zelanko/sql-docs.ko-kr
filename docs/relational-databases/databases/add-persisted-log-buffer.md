---
description: 데이터베이스에 지속형 로그 버퍼 추가
title: 데이터베이스에 지속형 로그 버퍼 추가
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- PMEM
- persistent memory
- persisted log buffer
- add log file
- create log buffer
- remove log buffer
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: cf3289d9d233da56c22739d3912045c2cdaa7554
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476240"
---
# <a name="add-persisted-log-buffer-to-a-database"></a>데이터베이스에 지속형 로그 버퍼 추가
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 토픽에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)]의 데이터베이스에 지속형 로그 버퍼를 추가하는 방법을 설명합니다.  
  
## <a name="permissions"></a>사용 권한

데이터베이스에 대한 ALTER 권한이 필요합니다.  

## <a name="configure-persistent-memory-device-linux"></a>영구 메모리 디바이스 구성(Linux)

[Linux](../../linux/sql-server-linux-configure-pmem.md)에서 영구 메모리 디바이스를 구성합니다.

## <a name="configure-persistent-memory-device-windows"></a>영구 메모리 디바이스 구성(Windows)

[Windows](/windows-server/storage/storage-spaces/deploy-pmem/)에서 영구 메모리 디바이스를 구성합니다.
  
## <a name="add-a-persisted-log-buffer-to-a-database"></a>데이터베이스에 지속형 로그 버퍼 추가  

다음 예제에서는 지속형 로그 버퍼를 추가합니다.

```sql
ALTER DATABASE <MyDB> 
  ADD LOG FILE 
  (
    NAME = <DAXlog>, 
    FILENAME = '<Filepath to DAX Log File>', 
    SIZE = 20MB
  );
```

새 로그 파일이 배치되는 볼륨 또는 탑재를 DAX(NTFS)로 포맷하거나 DAX 옵션(XFS/EXT4)을 사용해서 탑재해야 합니다.

## <a name="remove-a-persisted-log-buffer"></a>지속형 로그 버퍼 제거

지속형 로그 버퍼를 안전하게 제거하려면 지속형 로그 버퍼를 드레이닝하기 위해 데이터베이스를 단일 사용자 모드로 배치해야 합니다.

다음 예제에서는 지속형 로그 버퍼를 제거합니다.

```sql
ALTER DATABASE <MyDB> SET SINGLE_USER;
ALTER DATABASE <MyDB> REMOVE FILE <DAXlog>;
ALTER DATABASE <MyDB> SET MULTI_USER;
```

## <a name="limitations"></a>제한 사항

[TDE(투명한 데이터 암호화)](../security/encryption/transparent-data-encryption.md)는 지속형 로그 버퍼와 호환되지 않습니다.

주 복제본에서는 기본 로그 작성 의미 체계가 필요하기 때문에 [가용성 그룹](../../t-sql/statements/create-availability-group-transact-sql.md)은 보조 복제본에서만 이 기능을 사용할 수 있습니다. 그러나 모든 노드에 작은 로그 파일을 만들어야 합니다(DAX 볼륨 또는 탑재에 적합함).

## <a name="backup-and-restore-operations"></a>백업 및 복원 작업

기본 복원 조건이 적용됩니다. 지속형 로그 버퍼를 DAX 볼륨 또는 탑재로 복원하는 경우 계속해서 작동하며, 그러지 않으면 안전하게 제거할 수 있습니다.
  
## <a name="next-steps"></a>다음 단계

- [작동 방식(빠르게 실행됨): NVDIMM의 비휘발성 메모리 SQL Server 비상 로그 캐싱](https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)
- [데이터 표시: SQL Server 2016의 대기 시간 및 내구성](https://channel9.msdn.com/Shows/Data-Exposed/Latency-and-Durability-with-SQL-Server-2016)
- [Windows Server 2016/SQL Server 2016 SP1에서 스토리지 클래스 메모리를 사용하는 트랜잭션 커밋 대기 시간 가속화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)
