---
title: FileTable 관리 | Microsoft 문서
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cf899960d8e3025c9c7218990260fcbcd1394c87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922091"
---
# <a name="manage-filetables"></a>FileTable 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable을 관리하는 데 사용되는 일반적인 관리 태스크에 대해 설명합니다.  
  
##  <a name="HowToEnumerate"></a> 방법: FileTable 및 관련 개체 목록 가져오기  
 FileTable 목록을 가져오려면 다음 카탈로그 뷰 중 하나를 쿼리합니다.  
  
-   [sys.filetables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
  
-   [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)(**is_filetable** 열의 값 확인)  
  
```sql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 연결된 FileTable을 만들 때 생성된 시스템 정의 개체 목록을 가져오려면 카탈로그 뷰 [sys.filetable_system_defined_objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)를 쿼리합니다.  
  
```sql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
FROM sys.filetable_system_defined_objects;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> 데이터베이스 수준에서 비트랜잭션 액세스 사용 해제 및 다시 설정  
 특정 관리 태스크에 필요한 단독 액세스 권한을 획득하려면 비트랜잭션 액세스를 일시적으로 사용하지 않도록 설정해야 할 수 있습니다.  
  
 **비트랜잭션 액세스 수준을 변경할 경우 ALTER DATABASE 문의 동작**  
  
-   비트랜잭션 액세스를 READ_ONLY 또는 OFF로 설정하면 ALTER DATABASE 명령은 요청한 작업과 충돌하는 열려 있는 파일 핸들이 있는 동안에는 사용자에게 제어를 반환하지 않습니다. 이 작업과 충돌하는 파일 핸들에는 다음과 같은 것이 있습니다.  
  
    -   액세스를 **NONE**으로 설정하는 경우 모든 열려 있는 파일 핸들  
  
    -   액세스를 **READ_ONLY**로 설정하는 경우 쓰기 액세스를 위해 열린 모든 파일 핸들  
  
     열려 있는 파일 핸들을 중지하는 방법은 이 항목의 [FileTable과 연결된 열려 있는 파일 핸들 중지](#BasicsKilling) 를 참조하세요.  
  
     ALTER DATABASE 명령이 취소되거나 시간 초과로 종료된 경우에는 트랜잭션 액세스 수준이 변경되지 않습니다.  
  
-   WITH \<termination> 절(ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT)이 포함된 ALTER DATABASE 문을 호출하면 열려 있는 모든 비트랜잭션 파일 핸들이 중지됩니다.  
  
> [!WARNING]  
>  열려 있는 파일 핸들을 중지하면 저장하지 않은 데이터가 손실될 수 있습니다. 이 동작은 파일 시스템 자체의 동작과 일치합니다.  
  
 **비트랜잭션 액세스를 사용하지 않도록 설정할 경우의 효과**  
  
 데이터베이스 수준에서 비트랜잭션 액세스 수준을 변경하면 데이터베이스 수준 디렉터리에 다음과 같은 영향을 줍니다.  
  
-   액세스를 **NONE**으로 설정한 경우 모든 FileTable 디렉터리와 내용이 더 이상 액세스할 수 없거나 표시되지 않습니다.  
  
-   액세스를 **READ_ONLY**로 설정한 경우 모든 FileTable 디렉터리와 내용도 읽기 전용이 됩니다.  
  
 인스턴스 수준에서 FILESTREAM을 사용하지 않도록 설정하면 해당 인스턴스의 데이터베이스 수준 디렉터리와 이 디렉터리 아래의 FileTable 디렉터리에 다음과 같은 영향을 줍니다.  
  
-   인스턴스 수준에서 FILESTREAM을 사용하지 않도록 설정한 경우 인스턴스에 대한 데이터베이스 수준 디렉터리가 표시되지 않습니다.  
  
###  <a name="HowToDisable"></a> 방법: 데이터베이스 수준에서 비트랜잭션 액세스 사용 해제 및 다시 설정  
 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
 **전체 비트랜잭션 액세스를 사용하지 않도록 설정하려면**  
 **ALTER DATABASE** 문을 호출하고 **NON_TRANSACTED_ACCESS** 값을 **READ_ONLY** 또는 **OFF**로 설정합니다.  
  
```sql  
-- Disable write access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **전체 비트랜잭션 액세스를 다시 사용하도록 설정하려면**  
 **ALTER DATABASE** 문을 호출하고 **NON_TRANSACTED_ACCESS** 값을 **FULL**로 설정합니다.  
  
```sql  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> 방법: 데이터베이스에서 FileTable의 가시성 보장  
 다음 조건에 모두 해당하는 경우 데이터베이스 수준 디렉터리와 이 디렉터리 아래의 FileTable 디렉터리가 표시됩니다.  
  
1.  인스턴스 수준에서 FILESTREAM을 사용하도록 설정한 경우  
  
2.  데이터베이스 수준에서 비트랜잭션 액세스를 사용하도록 설정한 경우  
  
3.  데이터베이스 수준에서 유효한 디렉터리를 지정한 경우  
  
##  <a name="BasicsEnabling"></a> 테이블 수준에서 FileTable 네임스페이스 사용 해제 및 다시 설정  
 FileTable 네임스페이스를 사용하지 않도록 설정하면 FileTable과 함께 만들어진 모든 시스템 정의 제약 조건 및 트리거도 사용하지 않도록 설정됩니다. 이는 FileTable 의미 체계를 적용해야 하는 부담 없이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업을 사용하여 FileTable을 대규모로 다시 구성해야 하는 경우에 유용합니다. 하지만 이러한 작업으로 인해 FileTable이 일관성 없는 상태가 되고 FILETABLE 네임스페이스를 다시 사용하도록 설정하는 작업을 수행하지 못하게 될 수 있습니다.  
  
 FileTable 네임스페이스를 사용하지 않도록 설정하면 다음과 같은 결과가 나타납니다.  
  
-   FileTable 열과 데이터는 테이블에서 실제로 삭제되지 않습니다.  
  
-   FileTable 디렉터리와 이 디렉터리에 포함된 파일 및 디렉터리가 파일 시스템에서 사라지고 파일 I/O 액세스 기능에 대해 사용할 수 없습니다.  
  
-   시스템 정의 FileTable 열은 삭제하거나 다시 만들 수 없지만 DML 작업 시 일반 열과 동일하게 동작합니다.  
  
-   열려 있는 파일 핸들이 있으면 FileTable 제약 조건을 사용하지 않도록 설정할 수 없습니다. 그렇게 하려면 테이블에 대한 스키마 잠금이 필요합니다.  
  
-   FileTable 네임스페이스를 사용하지 않도록 설정하면 시스템 정의 제약 조건 및 트리거를 포함한 모든 FileTable 의미 체계의 적용이 중지됩니다.  
  
 FileTable 네임스페이스를 다시 사용하도록 설정하면 다음과 같은 결과가 나타납니다.  
  
-   FileTable의 일관성이 검사됩니다. 불일치가 발견되면 오류가 발생하고 FileTable이 사용되지 않는 상태로 유지되고, 그렇지 않으면 FileTable이 다시 사용하도록 설정됩니다.  
  
-   시스템 정의 제약 조건 및 트리거를 포함하여 FileTable 의미 체계의 적용이 복원됩니다.  
  
-   FileTable 디렉터리와 이 디렉터리에 포함된 파일 및 디렉터리가 파일 시스템에 표시되고 파일 I/O 액세스 기능을 사용할 수 있습니다.  
  
###  <a name="HowToEnableNS"></a> 방법: 테이블 수준에서 FileTable 네임스페이스 사용 해제 및 다시 설정  
 **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** 옵션을 사용하여 ALTER TABLE 문을 호출합니다.  
  
 **FileTable 네임스페이스를 사용하지 않도록 설정하려면**  
 ```sql  
ALTER TABLE filetable_name  
DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **FileTable 네임스페이스를 다시 사용하도록 설정하려면**  
 ```sql  
ALTER TABLE filetable_name  
ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> FileTable과 연결된 열려 있는 파일 핸들 중지  
 FileTable에 저장된 파일에 대해 열려 있는 핸들이 있으면 특정 관리 태스크에 필요한 단독 액세스가 허용되지 않습니다. 긴급 태스크를 수행할 수 있도록 하려면 하나 이상의 FileTable과 연결된 열려 있는 파일 핸들을 중지해야 할 수 있습니다.  
  
> [!WARNING]  
>  열려 있는 파일 핸들을 중지하면 저장하지 않은 데이터가 손실될 수 있습니다. 이 동작은 파일 시스템 자체의 동작과 일치합니다.  
  
###  <a name="HowToListOpen"></a> 방법: FileTable과 연결된 열려 있는 파일 핸들 목록 가져오기  
 카탈로그 뷰 [sys.dm_filestream_non_transacted_handles&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)를 쿼리합니다.  
  
```sql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> 방법: FileTable과 연결된 열려 있는 파일 핸들 중지  
 적절한 인수로 저장 프로시저 [sp_kill_filestream_non_transacted_handles&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)를 호출하여 데이터베이스 또는 FileTable에 열려 있는 모든 파일 핸들을 중지하거나 특정 핸들을 중지합니다.  
  
```sql  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> 방법: FileTable이 보유한 잠금 식별  
 FileTable이 보유한 대부분의 잠금은 응용 프로그램에서 연 파일에 해당합니다.  
  
 **열려 있는 파일과 연결된 잠금을 식별하려면**  
 동적 관리 뷰 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)의 **request_owner_id** 필드와 [sys.dm_filestream_non_transacted_handles&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)의 **fcb_id** 필드를 조인합니다. 잠금이 열려 있는 하나의 열려 있는 파일 핸들에 해당하지 않는 경우도 있습니다.  
  
```sql  
SELECT opened_file_name  
FROM sys.dm_filestream_non_transacted_handles  
WHERE fcb_id IN  
    ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> FileTable 보안  
 FileTable에 저장되는 파일과 디렉터리에는 SQL Server 보안만 적용됩니다. 테이블 및 열 기반 보안은 파일 시스템 액세스와 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에도 적용됩니다. Windows 파일 시스템 보안 API 및 ACL 설정은 지원되지 않습니다.  
  
 파일 데이터는 FileTable에 FILESTREAM 열로 저장되므로 FILESTREAM 파일 그룹과 컨테이너에 적용 가능한 보안 및 액세스 권한이 FileTable에도 적용됩니다.  
  
 **FileTable 보안 및 Transact-SQL 액세스**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스는 FileTable의 데이터에 대해 다른 테이블과 동일한 방식으로 보호됩니다. 데이터를 액세스하거나 변경하는 모든 작업에 대해 적절한 테이블 및 열 수준 보안 검사가 수행됩니다.  
  
 **FileTable 보안 및 파일 시스템 액세스**  
 파일 시스템 API를 통해 FileTable에 저장된 파일 또는 디렉터리에 대한 핸들을 열려면 FileTable의 전체 행에 대한 적절한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한(테이블 수준 권한)이 있어야 합니다. 사용자에게 FileTable의 모든 열에 대한 적절한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 없으면 파일 시스템 액세스가 거부됩니다.  
  
##  <a name="OtherBackup"></a> 백업과 FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 FileTable을 백업하면 FILESTREAM 데이터가 데이터베이스에 구조화된 데이터와 함께 백업됩니다. FILESTREAM 데이터를 관계형 데이터와 함께 백업하지 않으려면 부분 백업을 사용하여 FILESTREAM 파일 그룹을 제외할 수 있습니다.  
  
 **FileTable 백업의 트랜잭션 일관성**  
  
 백업, 로그 백업 및 트랜잭션 복제를 비롯한 많은 관리 도구와 작업에서는 트랜잭션 로그를 읽음으로써 트랜잭션 차원에서 일관된 데이터를 읽습니다. 이때 트랜잭션의 일부로 업데이트된 FILESTREAM 데이터를 읽게 됩니다. 데이터베이스 수준에서 비트랜잭션 액세스가 사용하도록 설정되지 않은 경우 이러한 도구 및 작업은 전체 트랜잭션에 일관되게 작동합니다.  
  
 그러나 전체 비트랜잭션 액세스가 사용하도록 설정되어 있으면 FileTable에는 도구 또는 프로세스가 트랜잭션 로그에서 읽고 있는 트랜잭션보다 더 최근에 비트랜잭션 업데이트를 통해 업데이트된 데이터가 포함될 수 있습니다. 즉, 특정 트랜잭션에 대한 "지정 시간" 복원 작업에 해당 트랜잭션보다 최신 상태인 FILESTREAM 데이터가 포함될 수 있습니다. 이는 FileTable에 대한 비트랜잭션 업데이트가 허용될 때의 예상 동작입니다.  
  
##  <a name="Monitor"></a> SQL Server Profiler와 FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler는 FileTable에 저장되는 파일에 대한 추적 출력에서 Windows 파일 열기 및 파일 닫기 작업을 캡처할 수 있습니다.  
  
##  <a name="OtherAuditing"></a> 감사와 FileTable  
 다른 테이블과 마찬가지로 FileTable을 감사할 수 있습니다. 그러나 Win32 액세스 패턴은 집합 기반 작업이 아닙니다. 파일 시스템의 단일 동작은 여러 개의 Transact-SQL DML 작업으로 변환됩니다. 예를 들어 Microsoft Word에서 파일을 여는 동작은 여러 개의 열기/닫기/만들기/이름 바꾸기/삭제 작업과 해당하는 Transact-SQL DML 작업으로 변환됩니다. 이로 인해 파일 시스템 동작 간의 레코드와 해당하는 Transact-SQL DML 감사 레코드 간의 상관 관계를 파악하기가 어려운 복잡한 감사 레코드가 만들어집니다.  
  
##  <a name="OtherDBCC"></a> DBCC와 FileTable  
 DBCC CHECKCONSTRAINTS를 사용하여 시스템 정의 제약 조건을 비롯한 FileTable의 제약 조건을 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [FileTable과 기타 SQL Server 기능 간 호환성](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)   
 [FileTable DDL, 함수, 저장 프로시저 및 뷰](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
