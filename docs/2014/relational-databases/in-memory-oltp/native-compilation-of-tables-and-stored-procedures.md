---
title: 테이블과 저장 프로시저의 네이티브 컴파일 | Microsoft 문서
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: rothja
ms.author: jroth
ms.openlocfilehash: 32c5b04610d894e06278fbeecdaf3bbebe850d60
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025953"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>테이블과 저장 프로시저의 네이티브 컴파일
  메모리 내 OLTP에서는 네이티브 컴파일이라는 개념이 도입됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 메모리 최적화 테이블에 액세스하는 저장 프로시저를 고유하게 컴파일할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 기본적으로 메모리 최적화 테이블을 컴파일할 수도 있습니다. 네이티브 컴파일을 사용하면 기존의 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]보다 빠르게 데이터에 액세스할 수 있으며 더 효율적으로 쿼리를 실행할 수 있습니다. 테이블과 저장 프로시저의 네이티브 컴파일은 DLL을 생성합니다.  
  
 메모리 액세스에 최적화된 테이블 형식의 네이티브 컴파일도 지원됩니다. 자세한 내용은 [Memory-Optimized Table Variables](../../database-engine/memory-optimized-table-variables.md)를 참조하세요.  
  
 네이티브 컴파일은 추가로 컴파일하거나 해석할 필요 없이 프로세서 명령으로 구성된 네이티브 코드로 프로그래밍 구문을 변환하는 프로세스를 말합니다.  
  
 메모리 내 OLTP에서는 메모리 최적화 테이블이 생성되고 고유하게 컴파일된 저장 프로시저가 로드될 때 네이티브 DLL로 컴파일됩니다. 또한 데이터베이스나 서버를 다시 시작한 후에도 DLL이 다시 컴파일됩니다. DLL을 다시 만드는 데 필요한 정보는 데이터베이스 메타데이터에 저장됩니다. DLL은 데이터베이스와 연결되어 있지만 데이터베이스의 일부는 아닙니다. 예를 들어, DLL은 데이터베이스 백업에 포함되지 않습니다.  
  
> [!NOTE]  
>  메모리 액세스에 최적화된 테이블은 서버 재시작 중 다시 컴파일됩니다. 데이터베이스 복구 속도를 높이기 위해 고유하게 컴파일된 저장 프로시저는 서버 재시작 중 다시 컴파일되지 않고 첫 번째 실행 시에 컴파일됩니다. 이렇게 지연되는 컴파일의 결과로, 고유하게 컴파일된 저장 프로시저는 첫 번째 실행 후 [sys.dm_os_loaded_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql)를 호출할 때만 나타납니다.  
  
## <a name="maintenance-of-in-memory-oltp-dlls"></a>메모리 내 OLTP DLL의 유지 관리  
 다음 쿼리에서는 서버의 메모리에 현재 로드된 모든 테이블 및 저장 프로시저 DLL을 보여 줍니다.  
  
```sql  
SELECT name, description FROM sys.dm_os_loaded_modules  
where description = 'XTP Native DLL'  
```  
  
 데이터베이스 관리자는 네이티브 컴파일에서 생성된 파일을 유지 관리할 필요가 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 생성된 파일 중에서 더 이상 필요 없는 파일을 자동으로 제거합니다. 예를 들어, 테이블과 저장 프로시저가 삭제되거나 데이터베이스가 삭제되면 생성된 파일이 삭제됩니다.  
  
> [!NOTE]  
>  컴파일이 실패하거나 중단된 경우 생성된 일부 파일이 제거되지 않습니다. 이러한 파일은 지원 가능성을 위해 의도적으로 남겨지며 데이터베이스를 삭제하면 제거됩니다.  
  
> [!NOTE]  
>  데이터베이스를 시작하는 중에 SQL Server가 데이터베이스 복구에 필요한 모든 테이블에 대한 DLL을 컴파일합니다. 데이터베이스를 다시 시작하기 직전에 테이블이 삭제된 경우, 파일의 체크포인트나 트랜잭션 로그에 테이블의 잔해가 남아있을 수 있으므로 데이터베이스를 시작하는 중에 테이블에 대한 DLL이 다시 컴파일될 가능성이 있습니다. 다시 시작한 후에 일반 정리 프로세스에 의해 DLL이 언로드되고 파일이 삭제됩니다.  
  
## <a name="native-compilation-of-tables"></a>테이블의 네이티브 컴파일  
 ph x="1" /&gt; 문을 사용하여 메모리 최적화 테이블을 만들면 데이터베이스 메타데이터에 테이블 정보가 기록되고 메모리에 테이블 및 인덱스 구조가 작성됩니다. 또한 테이블이 DLL로 컴파일됩니다.  
  
 다음 예제 스크립트에서는 데이터베이스와 메모리 최적화 테이블을 만듭니다.  
  
```sql  
use master  
go  
create database db1  
go  
alter database db1 add filegroup db1_mod contains memory_optimized_data  
go  
-- adapt filename as needed  
alter database db1 add file (name='db1_mod', filename='c:\data\db1_mod') to filegroup db1_mod  
go  
use db1  
go  
create table dbo.t1  
   (c1 int not null primary key nonclustered,  
    c2 INT)  
with (memory_optimized=on)  
go  
-- retrieve the path of the DLL for table t1  
select name, description FROM sys.dm_os_loaded_modules  
where name like '%xtp_t_' + cast(db_id() as varchar(10)) + '_' + cast(object_id('dbo.t1') as varchar(10)) + '.dll'  
go  
```  
  
 테이블을 만들면 테이블 DLL이 만들어지고 DLL이 메모리에 로드됩니다. CREATE TABLE 문 바로 뒤의 DMV 쿼리가 테이블 DLL의 경로를 검색합니다.  
  
 테이블 DLL은 테이블의 인덱스 구조와 행 형식을 이해합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 인덱스 순회, 행 검색뿐 아니라 행 내용 저장에도 DLL을 사용합니다.  
  
## <a name="native-compilation-of-stored-procedures"></a>저장 프로시저의 네이티브 컴파일  
 NATIVE_COMPILATION으로 표시된 저장 프로시저는 고유하게 컴파일됩니다. 성능에 중요한 영향을 미치는 비즈니스 논리를 효율적으로 실행하기 위해 프로시저의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 모두 네이티브 코드로 컴파일됩니다.  
  
 고유하게 컴파일된 저장 프로시저에 대한 자세한 내용은 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)를 참조하세요.  
  
 다음 예제 저장 프로시저에서는 이전 예제의 테이블 t1에 행을 삽입합니다.  
  
```sql  
create procedure dbo.native_sp  
with native_compilation, schemabinding, execute as owner  
as  
begin atomic  
with (transaction isolation level=snapshot, language=N'us_english')  
  
  declare @i int = 1000000  
  while @i > 0  
  begin  
    insert dbo.t1 values (@i, @i+1)  
    set @i -= 1  
  end  
  
end  
go  
exec dbo.native_sp  
go  
-- reset  
delete from dbo.t1  
go  
```  
  
 native_sp에 대한 DLL은 t1에 대한 DLL 및 메모리 내 OLTP 스토리지 엔진과 직접 상호 작용하여 행을 최대한 빠르게 삽입할 수 있습니다.  
  
 메모리 내 OLTP 컴파일러는 쿼리 최적화 프로그램을 이용하여 저장 프로시저의 각 쿼리에 대한 효율적인 실행 계획을 만듭니다. 테이블의 데이터가 변경되면 고유하게 컴파일된 저장 프로시저는 자동으로 다시 컴파일됩니다. 메모리 내 OLTP를 사용한 통계 및 저장 프로시저 유지 관리에 대한 자세한 내용은 [메모리 액세스에 최적화된 테이블에 대한 통계](memory-optimized-tables.md)를 참조하세요.  
  
## <a name="security-considerations-for-native-compilation"></a>네이티브 컴파일에 대한 보안 고려 사항  
 테이블 및 저장 프로시저의 네이티브 컴파일에서는 메모리 내 OLTP 컴파일러를 사용합니다. 이 컴파일러는 디스크에 기록되고 메모리에 로드되는 파일을 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다음과 같은 메커니즘을 사용하여 이러한 파일에 대한 액세스를 제한합니다.  
  
### <a name="native-compiler"></a>기본 컴파일러  
 컴파일러 실행 파일과 네이티브 컴파일에 필요한 이진 파일 및 헤더 파일은 MSSQL\Binn\Xtp 폴더 아래에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 일부로 설치됩니다. 따라서 기본 인스턴스가 c:\program files 아래에 설치 되는 경우 컴파일러 파일은 c:\program files \MSSQL12.에 설치 됩니다. \\ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSSQLSERVER\MSSQL\Binn\Xtp.  
  
 컴파일러에 대한 액세스를 제한하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 ACL(액세스 제어 목록)을 사용하여 이진 파일에 대한 액세스를 제한합니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이진 파일은 ACL을 통해 수정이나 변조로부터 보호됩니다. 기본 컴파일러의 ACL은 컴파일러의 사용도 제한합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 시스템 관리자에게만 기본 컴파일러 파일에 대한 읽기 및 실행 권한이 있습니다.  
  
### <a name="files-generated-by-a-native-compilation"></a>네이티브 컴파일에서 생성된 파일  
 테이블이나 저장 프로시저가 컴파일될 때 생성되는 파일에는 DDL과 .c, .obj, .xml 및 .pdb 확장명을 사용하는 파일을 비롯한 중간 파일이 있습니다. 생성된 파일은 기본 데이터 폴더의 하위 폴더에 저장됩니다. 하위 폴더를 Xtp라고 합니다. 기본 데이터 폴더를 사용 하 여 기본 인스턴스를 설치 하는 경우 생성 된 파일은 C:\Program files \\ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12.에 배치 됩니다. MSSQLSERVER\MSSQL\DATA\Xtp.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 생성된 DDL의 변조를 다음 세 가지 방법으로 방지합니다.  
  
-   테이블이나 저장 프로시저가 DLL로 컴파일될 때 이 DLL은 즉시 메모리에 로드되고 sqlserver.exe 프로세스에 링크됩니다. DLL은 프로세스에 링크되어 있는 동안 수정될 수 없습니다.  
  
-   데이터베이스가 다시 시작될 때 모든 테이블 및 저장 프로시저는 데이터베이스 메타데이터에 따라 다시 컴파일됩니다(제거되고 다시 만들어짐). 이에 따라 악성 에이전트가 생성된 파일에서 변경한 모든 내용이 제거됩니다.  
  
-   생성된 파일은 사용자 데이터의 일부로 간주되며 ACL을 통해 데이터베이스 파일과 동일한 보안 제한이 적용됩니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 시스템 관리자만 생성된 파일에 액세스할 수 있습니다.  
  
 생성된 파일을 관리하는 데는 사용자 개입이 필요하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 필요에 따라 이러한 파일을 만들고 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화 된 테이블](memory-optimized-tables.md)   
 [고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)  
  
  
