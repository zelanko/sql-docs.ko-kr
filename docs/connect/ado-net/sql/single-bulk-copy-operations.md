---
title: 단일 대량 복사 작업
description: SqlBulkCopy 클래스를 사용하여 SQL Server 인스턴스에 데이터의 단일 대량 복사를 수행하는 방법 및 Transact-SQL 문과 SqlCommand 클래스를 사용하여 대량 복사 작업을 수행하는 방법을 각각 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 85d24b6695dfe9f592bfefabb13c2042cf3450c3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251176"
---
# <a name="single-bulk-copy-operations"></a>단일 대량 복사 작업

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 대량 복사 작업을 수행하는 가장 간단한 방법은 데이터베이스에 대해 단일 작업을 수행하는 것입니다. 기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 복사 작업은 트랜잭션되지 않은 방식으로 수행되어 롤백할 수 없습니다.  
  
> [!NOTE]
>  오류가 발생하여 대량 복사의 일부 또는 전체를 롤백해야 하는 경우 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 관리형 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행할 수 있습니다. 연결이 **System.Transactions** 트랜잭션에 암시적으로나 명시적으로 등록된 경우 **SqlBulkCopy**에서도 <xref:System.Transactions>을 사용합니다.  
>   
>  자세한 내용은 [트랜잭션 및 대량 복사 작업](transaction-bulk-copy-operations.md)을 참조하세요.  
  
대량 복사 작업을 수행하는 일반적인 단계는 다음과 같습니다.  
  
1. 원본 서버에 연결하고 복사할 데이터를 가져옵니다. <xref:System.Data.IDataReader> 또는 <xref:System.Data.DataTable> 개체에서 데이터를 검색할 수 있는 경우, 다른 원본에서 데이터를 가져올 수도 있습니다.  
  
2. **SqlBulkCopy**를 통해 자동으로 연결하지 않으려는 경우 대상 서버에 연결합니다.  
  
3. 필요한 속성을 설정하면서 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 개체를 만듭니다.  
  
4. **DestinationTableName** 속성이 대량 삽입 작업의 대상 테이블을 나타내도록 설정합니다.  
  
5. **WriteToServer** 메서드 중 하나를 호출합니다.  
  
6. 필요에 따라 속성을 업데이트하고 **WriteToServer**를 다시 호출합니다.  
  
7. <xref:Microsoft.Data.SqlClient.SqlBulkCopy.Close%2A>를 호출하거나 `Using` 문 내에서 대량 복사 작업을 래핑합니다.  
  
> [!CAUTION]
>  원본 열과 대상 열의 데이터 형식은 일치하는 것이 좋습니다. 데이터 형식이 일치하지 않으면 **SqlBulkCopy**는 <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>에서 사용되는 규칙과 동일한 규칙을 사용하여 각 원본 값을 대상 데이터 형식으로 변환하려고 시도합니다. 변환은 성능에 영향을 줄 수 있으며 예기치 않은 오류가 발생할 수도 있습니다. 예를 들어 `Double` 데이터 형식은 대부분의 경우 `Decimal` 데이터 형식으로 변환할 수 있지만 항상 그렇지는 않습니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하여 데이터를 로드하는 방법을 보여줍니다. 이 예제에서는 <xref:Microsoft.Data.SqlClient.SqlDataReader>를 사용하여 SQL Server **AdventureWorks** 데이터베이스에 있는 **Production.Product** 테이블의 데이터를 같은 데이터베이스의 비슷한 테이블로 복사합니다.  
  
> [!IMPORTANT]
>  이 샘플은 가져올 [대량 복사 샘플 설정](bulk-copy-example-setup.md)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 **SqlBulkCopy**를 사용하는 구문을 보여 주는 용도로 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL `INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
[!code-csharp[DataWorks SqlBulkCopy_WriteToServer#1](~/../sqlclient/doc/samples/SqlBulkCopy_WriteToServer.cs#1)]
  
## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>Transact-SQL 및 Command 클래스를 사용하여 대량 복사 작업 수행  
다음 예제에서는 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 메서드를 사용하여 BULK INSERT 문을 실행하는 방법을 보여 줍니다.  
  
> [!NOTE]
>  데이터 원본의 파일 경로는 서버에 상대적입니다. 대량 복사 작업이 성공하려면 서버 프로세스에서 해당 경로에 액세스할 수 있어야 합니다.  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server에서 대량 복사 작업](bulk-copy-operations-sql-server.md)
