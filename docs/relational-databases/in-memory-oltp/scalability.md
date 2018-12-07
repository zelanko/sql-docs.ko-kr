---
title: 확장성 | Microsoft 문서
ms.custom: ''
ms.date: 08/27/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4f672c1b3d7ff8d4480e6fb1647058c50715b657
ms.sourcegitcommit: 1f10e9df1c523571a8ccaf3e3cb36a26ea59a232
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2018
ms.locfileid: "51858568"
---
# <a name="scalability"></a>확장성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 메모리 최적화 테이블용 디스크의 스토리지 확장성이 향상되었습니다. 

## <a name="multiple-threads-to-persist-memory-optimized-tables"></a>여러 스레드에 메모리 최적화 테이블 유지  
  
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서는 단일 오프라인 검사점 스레드가 트랜잭션 로그에서 메모리 최적화 테이블 변경 내용을 검사하여 데이터 및 델타 파일과 같은 검사점 파일에 이러한 변경 내용을 유지했습니다. 코어 수가 많은 머신에서 오프라인 검사점 스레드 하나로는 변경 내용을 검사하여 빠르게 유지할 수가 없었습니다.  
  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 여러 동시 스레드가 메모리 최적화 테이블의 변경 내용을 유지합니다.  
  
## <a name="multi-threaded-recovery"></a>다중 스레드 복구
이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스에서는 복구 작업의 일부분으로 수행되는 로그 적용이 단일 스레드에서 진행되었습니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 로그 적용이 다중 스레드로 수행됩니다.  
  
## <a name="merge-operation"></a>병합 작업  
이제 병합 작업이 다중 스레드로 수행됩니다.  
   
> [!NOTE]
> 다중 스레드 병합을 통해 로드를 처리할 수 있으므로 수동 병합은 사용하지 않도록 설정되었습니다. 

## <a name="dynamic-management-views"></a>동적 관리 뷰  
DMV [sys.dm_db_xtp_checkpoint_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) 및 [sys.dm_db_xtp_checkpoint_files&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)가 크게 변경되었습니다.  

## <a name="storage-management"></a>스토리지 관리
메모리 내 OLTP 엔진은 계속해서 FILESTREAM을 기반으로 하여 메모리 최적화 파일 그룹을 사용하지만, 파일 그룹의 개별 파일은 FILESTREAM에서 분리됩니다. 메모리 내 OLTP 엔진을 통해 파일 만들기, 삭제, 가비지 수집 등 이러한 파일에 대한 작업을 완전하게 관리할 수 있습니다. 

> [!NOTE]
> [DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)은 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목   
[메모리 액세스에 최적화된 개체의 스토리지 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)     
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[ALTER DATABASE 파일 및 파일 그룹 옵션(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)    
