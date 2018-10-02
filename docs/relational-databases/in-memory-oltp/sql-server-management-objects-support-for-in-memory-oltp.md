---
title: 메모리 내 OLTP에 대한 SQL Server 관리 개체 지원 | Microsoft 문서
description: 메모리 내 OLTP를 지원하는 SMO(SQL Server 관리 개체) 항목을 설명합니다.
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2b67292d-6d8e-4016-9063-a97461ffe57a
author: CarlRabeler
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 957e5a385f40f25bc608088b981853e23daf1dec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741601"
---
# <a name="sql-server-management-objects-support-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 SQL Server 관리 개체 지원
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
이 항목에서는 메모리 내 OLTP를 지원하는 SMO(SQL Server 관리 개체) 항목을 설명합니다.  

## <a name="smo-types-and-members"></a>SMO 형식 및 멤버

다음 형식과 멤버는 네임스페이스 **Microsoft.SqlServer.Management.Smo**에 있으며 메모리 내 OLTP를 지원합니다.

- **<xref:Microsoft.SqlServer.Management.Smo.DurabilityType>**(열거형)
- FileGroup.**<xref:Microsoft.SqlServer.Management.Smo.FileGroup.FileGroupType%2A>** (속성)
- FileGroup.**<xref:Microsoft.SqlServer.Management.Smo.FileGroup.%23ctor%2A>** (생성자)
- **<xref:Microsoft.SqlServer.Management.Smo.FileGroupType>**(열거형)
- Index.**<xref:Microsoft.SqlServer.Management.Smo.Index.BucketCount%2A>** (속성)
- IndexType.**<xref:Microsoft.SqlServer.Management.Smo.IndexType.NonClusteredHashIndex>** (열거형 멤버)
- Index.**<xref:Microsoft.SqlServer.Management.Smo.Index.IsMemoryOptimized%2A>** (속성)
- Server.**<xref:Microsoft.SqlServer.Management.Smo.Server.IsXTPSupported%2A>** (속성)
- StoredProcedure.**<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.IsNativelyCompiled%2A>** (속성)
- StoredProcedure.**<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.IsSchemaBound%2A>** (속성)
- Table.**<xref:Microsoft.SqlServer.Management.Smo.Table.Durability%2A>** (속성)
- Table.**<xref:Microsoft.SqlServer.Management.Smo.Table.IsMemoryOptimized%2A>** (속성)
- UserDefinedTableType.**<xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType.IsMemoryOptimized%2A>** (속성)

## <a name="c-code-example"></a>C# 코드 예제

#### <a name="assemblies-referenced-by-the-compiled-code-example"></a>컴파일된 코드 예제에서 참조되는 어셈블리

- Microsoft.SqlServer.ConnectionInfo.dll
- Microsoft.SqlServer.Management.Sdk.Sfc.dll
- Microsoft.SqlServer.Smo.dll
- Microsoft.SqlServer.SqlEnum.dll

#### <a name="actions-taken-in-the-code-example"></a>코드 예제에서 수행된 작업

1. 메모리 최적화 파일 그룹 및 메모리 최적화 파일이 있는 데이터베이스를 만듭니다.  
2. 기본 키, 비클러스터형 인덱스 및 비클러스터형 해시 인덱스가 있는 내구성 있는 메모리 최적화 테이블을 만듭니다.  
3. 열 및 인덱스를 만듭니다.  
4. 사용자 정의 메모리 최적화 테이블 형식을 만듭니다.  
5. 고유하게 컴파일된 저장 프로시저를 만듭니다.

#### <a name="source-code"></a>소스 코드
  
```csharp
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   static void Main(string[] args) {  
      Server server = new Server("(local)");  
  
      // Create a database with memory-optimized filegroup and memory-optimized file.
      Database db = new Database(server, "MemoryOptimizedDatabase");  
      db.Create();  
      FileGroup fg = new FileGroup(
         db,
         "memOptFilegroup",
         FileGroupType.MemoryOptimizedDataFileGroup);  
      db.FileGroups.Add(fg);  
      fg.Create();  
      // Change this path if needed.
      DataFile file = new DataFile(
         fg,
         "memOptFile",
         @"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\MSSQLmemOptFileName");  
      file.Create();  
  
      // Create a durable memory-optimized table with primary key, nonclustered index and nonclustered hash index.
      // Define the table as memory optimized and set the durability.
      Table table = new Table(db, "memOptTable");  
      table.IsMemoryOptimized = true;  
      table.Durability = DurabilityType.SchemaAndData;  
  
      // Create columns.
      Column col1 = new Column(table, "col1", DataType.Int);  
      col1.Nullable = false;  
      table.Columns.Add(col1);  
      Column col2 = new Column(table, "col2", DataType.Float);  
      col2.Nullable = false;  
      table.Columns.Add(col2);  
      Column col3 = new Column(table, "col3", DataType.Decimal(2, 10));  
      col3.Nullable = false;  
      table.Columns.Add(col3);  
  
      // Create indexes.
      Index pk = new Index(table, "PK_memOptTable");  
      pk.IndexType = IndexType.NonClusteredIndex;  
      pk.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      pk.IndexedColumns.Add(new IndexedColumn(pk, col1.Name));  
      table.Indexes.Add(pk);  
  
      Index ixNonClustered = new Index(table, "ix_nonClustered");  
      ixNonClustered.IndexType = IndexType.NonClusteredIndex;  
      ixNonClustered.IndexKeyType = IndexKeyType.None;  
      ixNonClustered.IndexedColumns.Add(
         new IndexedColumn(ixNonClustered, col2.Name));  
      table.Indexes.Add(ixNonClustered);  
  
      Index ixNonClusteredHash = new Index(table, "ix_nonClustered_Hash");  
      ixNonClusteredHash.IndexType = IndexType.NonClusteredHashIndex;  
      ixNonClusteredHash.IndexKeyType = IndexKeyType.None;  
      ixNonClusteredHash.BucketCount = 1024;  
      ixNonClusteredHash.IndexedColumns.Add(
         new IndexedColumn(ixNonClusteredHash, col3.Name));  
      table.Indexes.Add(ixNonClusteredHash);  
  
      table.Create();  
  
      // Create a user-defined memory-optimized table type.
      UserDefinedTableType uDTT = new UserDefinedTableType(db, "memOptUDTT");  
      uDTT.IsMemoryOptimized = true;  
  
      // Add columns.
      Column udTTCol1 = new Column(uDTT, "udtCol1", DataType.Int);  
      udTTCol1.Nullable = false;  
      uDTT.Columns.Add(udTTCol1);  
      Column udTTCol2 = new Column(uDTT, "udtCol2", DataType.Float);  
      udTTCol2.Nullable = false;  
      uDTT.Columns.Add(udTTCol2);  
      Column udTTCol3 = new Column(uDTT, "udtCol3", DataType.Decimal(2, 10));  
      udTTCol3.Nullable = false;  
      uDTT.Columns.Add(udTTCol3);  
  
      // Add index.
      Index ix = new Index(uDTT, "IX_UDT");  
      ix.IndexType = IndexType.NonClusteredHashIndex;  
      ix.BucketCount = 1024;  
      ix.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      ix.IndexedColumns.Add(new IndexedColumn(ix, udTTCol1.Name));  
      uDTT.Indexes.Add(ix);  
  
      uDTT.Create();  
  
      // Create a natively compiled stored procedure.
      StoredProcedure sProc = new StoredProcedure(db, "nCSProc");  
      sProc.TextMode = false;  
      sProc.TextBody = "--Type body here";  
      sProc.IsNativelyCompiled = true;  
      sProc.IsSchemaBound = true;  
      sProc.ExecutionContext = ExecutionContext.Owner;  
      sProc.Create();  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  

- [메모리 내 OLTP에 대한 SQL Server 지원](sql-server-support-for-in-memory-oltp.md)
- [SMO 개요](../server-management-objects-smo/overview-smo.md)
