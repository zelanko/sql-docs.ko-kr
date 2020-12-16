---
title: 애플리케이션 수준 분할 | Microsoft 문서
description: 주문을 처리하는 이 예제를 검토합니다. 이 애플리케이션은 최근 주문을 메모리 최적화 테이블에 저장하고 이전 주문을 디스크 기반 테이블에 저장합니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 162d1392-39d2-4436-a4d9-ee5c47864c5a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cfa7f4c439ff886a07845605f0e07274068340f8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465424"
---
# <a name="application-level-partitioning"></a>애플리케이션 수준 분할
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 애플리케이션은 주문을 처리합니다. 최근 주문에 대한 처리 작업이 많습니다. 이전 주문에 대한 처리 작업이 많지 않습니다. 최근 주문이 메모리 최적화 테이블에 있습니다. 이전 명령이 디스크 기반 테이블에 있습니다. *hotDate* 이후의 모든 주문은 메모리 최적화 테이블에 있습니다. *hotDate* 이전의 모든 주문은 디스크 기반 테이블에 있습니다. 동시 트랜잭션이 많이 있는 극단적인 OLTP 작업을 가정합니다. 여러 개의 동시 트랜잭션이 *hotDate* 를 변경하려고 하는 경우에도 이 비즈니스 규칙(메모리 최적화 테이블에 있는 최근 주문)을 적용해야 합니다.  
  
 이 예제에서는 디스크 기반 테이블에 분할된 테이블을 사용하지 않지만 제 3의 테이블을 사용하여 두 테이블 간의 명시적 분할 지점을 추적합니다. 분할 지점을 사용하여 새로 삽입된 데이터가 날짜에 따라 적절한 테이블에 항상 삽입되도록 할 수 있으며 데이터를 찾을 위치를 결정할 수도 있습니다. 늦게 도착하는 데이터가 여전히 적절한 테이블로 이동합니다.  
  
 관련 샘플을 보려면 [메모리 액세스에 최적화된 테이블 분할을 위한 애플리케이션 패턴](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)을 참조하세요.  
  
## <a name="code-listing"></a>코드 목록  
  
```sql  
USE MASTER  
GO  
IF NOT EXISTS(SELECT name FROM sys.databases WHERE name = 'hkTest')  
  
CREATE DATABASE hkTest  
-- enable for In-Memory OLTP - change file path as needed  
ALTER DATABASE hkTest ADD FILEGROUP hkTest_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hkTest ADD FILE( NAME = 'hkTest_mod' , FILENAME = 'c:\data\hkTest_mod') TO FILEGROUP hkTest_mod;  
GO  
  
use hkTest  
go  
  
-- create memory-optimized table   
if OBJECT_ID(N'hot',N'U') IS NOT NULL  
   drop table [hot]  
  
create table hot   
   (id int not null primary key nonclustered,  
   orderDate datetime not null,  
   custName nvarchar(10) not null  
) with (memory_optimized=on)  
go  
  
-- create disk-based table for older order data  
if OBJECT_ID(N'cold',N'U') IS NOT NULL  
   drop table [cold]  
  
create table cold (  
   id int not null primary key,   
   orderDate datetime not null,   
   custName nvarchar(10) not null  
)  
go  
  
-- the hotDate is maintained in this memory-optimized table. The current hotDate is always the single date in this table  
if OBJECT_ID(N'hotDataSplit') IS NOT NULL  
   drop table [hotDataSplit]  
  
create table hotDataSplit (  
   hotDate datetime not null primary key nonclustered hash with (bucket_count = 1)  
) with (memory_optimized=on)  
go  
  
--  Stored Procedures  
--  set the hotDate  
--  snapshot: if any other transaction tries to update the hotDate, it will fail immediately due to a  
--  write/write conflict  
if OBJECT_ID(N'usp_hkSetHotDate') IS NOT NULL  
   drop procedure usp_hkSetHotDate  
go  
  
create procedure usp_hkSetHotDate @newDate datetime  
   with native_compilation, schemabinding, execute as owner  
   as begin atomic with  
   (  
      transaction isolation level = snapshot,  
      language = N'english'  
   )  
  
   delete from dbo.hotDataSplit  
   insert dbo.hotDataSplit values (@newDate)  
   end  
go  
  
-- extract data up to a certain date [presumably the new hotDate]  
-- must be serializable, because you don't want to delete rows that are not returned  
if OBJECT_ID(N'usp_hkExtractHotData') IS NOT NULL  
   drop procedure usp_hkExtractHotData  
go  
create procedure usp_hkExtractHotData @hotDate datetime  
   with native_compilation, schemabinding, execute as owner  
   as begin atomic with  
   (  
      transaction isolation level = serializable,  
      language = N'english'  
)  
   select id, orderDate, custName from dbo.hot where orderDate < @hotDate  
   delete from dbo.hot where orderDate < @hotDate  
end  
go  
  
-- insert order  
-- inserts an order either in recent or older table, depending on the current hotDate  
-- it is important that the SP for retrieving the hotDate is repeatableread, in order to ensure that  
-- the hotDate is not changed before the decision is made where to insert the order  
-- note that insert operations [in both disk-based and memory-optimized tables] are always fully isolated, so the transaction  
-- isolation level has no impact on the insert operations; this whole transaction is effectively repeatableread  
if OBJECT_ID(N'usp_InsertOrder') IS NOT NULL  
   drop procedure usp_InsertOrder  
go  
  
create procedure usp_InsertOrder(@id int, @orderDate date, @custName nvarchar(10))  
   as begin  
   SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
   begin tran  
      -- get hot date under repeatableread isolation; this is to guarantee it does not change before the insert is executed  
      declare @hotDate datetime  
      set @hotDate = (select hotDate from hotDataSplit with (repeatableread))  
  
      if (@orderDate >= @hotDate) begin  
         insert into hot values (@id, @orderDate, @custName)  
      end  
      else begin  
         insert into cold values (@id, @orderDate, @custName)  
      end  
   commit tran  
end  
go  
  
-- change hot date  
-- changes the hotDate and moves the rows between the recent and older order tables as appropriate  
-- the hotDate is updated in this transaction; this means that if the hotDate is changed by another transaction  
--   the update will fail due to a write/write conflict and the transaction is rolled back  
--   therefore, the initial (snapshot) access of the hotDate is effectively repeatable read  
if OBJECT_ID(N'usp_ChangeHotDate') IS NOT NULL  
   drop procedure usp_ChangeHotDate  
go  
create procedure usp_ChangeHotDate(@newHotDate datetime)  
as  
begin  
   SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
   begin tran  
       declare @oldHotDate datetime  
      set @oldHotDate = (select hotDate from hotDataSplit with (snapshot))  
  
       -- get hot date under repeatableread isolation; this is to guarantee it does not change before the insert is executed  
      if (@oldHotDate < @newHotDate) begin  
         insert into cold exec usp_hkExtractHotData @newHotDate  
      end  
      else begin  
         insert into hot select * from cold with (serializable) where orderDate >= @newHotDate  
         delete from cold with (serializable) where orderDate >= @newHotDate  
      end  
      exec usp_hkSetHotDate @newHotDate  
   commit tran  
end  
go  
  
--  Deploy and populate tables  
-- cleanup  
delete from cold  
go  
  
-- init hotDataSplit  
exec usp_hkSetHotDate '2012-1-1'   
go  
  
-- verify hotDate  
select * from hotDataSplit  
go  
  
EXEC usp_InsertOrder 1, '2011-11-14', 'cust1'  
EXEC usp_InsertOrder 2, '2012-3-4', 'cust1'  
EXEC usp_InsertOrder 3, '2011-1-23', 'cust1'  
EXEC usp_InsertOrder 4, '2011-8-6', 'cust1'  
EXEC usp_InsertOrder 5, '2010-11-1', 'cust1'  
EXEC usp_InsertOrder 6, '2012-1-9', 'cust1'  
EXEC usp_InsertOrder 7, '2012-2-14', 'cust1'  
EXEC usp_InsertOrder 8, '2010-1-17', 'cust1'  
EXEC usp_InsertOrder 9, '2012-3-8', 'cust1'  
EXEC usp_InsertOrder 10, '2011-9-24', 'cust1'  
go  
  
--  Demo Portion  
-- verify contents of the tables  
-- hotDate is 2012-1-1  
-- all orders from 2012 are in the recent table  
-- all orders before 2012 are in the older order table  
  
-- query hot data  
select * from hot order by orderDate desc  
  
-- query cold date  
select * from cold order by orderDate desc  
  
-- move hot date to Mar 2012  
EXEC usp_ChangeHotDate '2012-03-01'  
  
-- Verify that all orders before Mar 2012 were moved to older order table  
-- query hot data  
select * from hot order by orderDate desc  
  
-- query old data  
select * from cold order by orderDate desc  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP 코드 예제](./sample-database-for-in-memory-oltp.md)  
  
