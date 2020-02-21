---
title: 대량 복사 예제 설정
description: 대량 복사 예제에 사용된 테이블에 대해 설명하고 AdventureWorks 데이터베이스에서 테이블을 만들기 위한 SQL 스크립트를 제공합니다.
ms.date: 09/30/2019
dev_langs:
- sql
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 129dc64fc9bac2111cd0bc5cb61f3ce7f1d98ee1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247871"
---
# <a name="bulk-copy-example-setup"></a>대량 복사 예제 설정

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 이 항목에 표시된 코드 샘플에서는 SQL Server 샘플 데이터베이스 **AdventureWorks**를 사용합니다. 기존 테이블 코드 샘플이 변경되지 않도록 하려면 먼저 만들어야 하는 테이블에 데이터를 씁니다.  
  
**BulkCopyDemoMatchingColumns** 및 **BulkCopyDemoDifferentColumns** 테이블은 모두 **AdventureWorks** **Production.Products** 테이블을 기반으로 합니다. 이러한 테이블을 사용하는 코드 샘플에서 데이터는 **Production.Products** 테이블에서 이러한 샘플 테이블 중 하나에 추가됩니다. **BulkCopyDemoDifferentColumns** 테이블은 샘플에서 원본 데이터의 열을 대상 테이블에 매핑하는 방법을 보여 주는 경우에 사용되고, **BulkCopyDemoMatchingColumns**는 대부분의 다른 샘플에서 사용됩니다.  
  
일부 코드 샘플에서는 하나의 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하여 여러 테이블에 쓰는 방법을 보여 줍니다. 이러한 샘플에서는 **BulkCopyDemoOrderHeader** 및 **BulkCopyDemoOrderDetail** 테이블이 대상 테이블로 사용됩니다. 이러한 테이블은 **AdventureWorks**의 **Sales.SalesOrderHeader** 및 **Sales.SalesOrderDetail** 테이블을 기반으로 합니다.  
  
> [!NOTE]
>  **SqlBulkCopy** 코드 샘플은 **SqlBulkCopy**를 사용하는 구문을 보여 주기 위한 용도로만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL `INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
## <a name="table-setup"></a>테이블 설정  
코드 샘플을 올바르게 실행하는 데 필요한 테이블을 만들려면 SQL Server 데이터베이스에서 다음 TRANSACT-SQL 문을 실행해야 합니다.  
  
```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server에서 대량 복사 작업](bulk-copy-operations-sql-server.md)
