---
title: FILESTREAM 데이터
description: FILESTREAM 특성을 사용 하 여 SQL Server 2008에 저장 된 대량 값 데이터로 작업 하는 방법을 설명 합니다.
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 83e793fac40a8e41850f2a45e138dd125130c13e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452214"
---
# <a name="filestream-data"></a>FILESTREAM 데이터

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

FILESTREAM 저장소 특성은 varbinary (max) 열에 저장 된 이진 (BLOB) 데이터에 대 한 것입니다. FILESTREAM 이전에는 이진 데이터를 저장 하는 데 특별 한 처리가 필요 했습니다. 텍스트 문서, 이미지 및 비디오와 같은 구조화 되지 않은 데이터는 종종 데이터베이스 외부에 저장 되어 관리가 어려워집니다.

> [!NOTE]
> SqlClient를 사용 하 여 FILESTREAM 데이터 작업을 수행 하려면 .NET Framework 3.5 SP1 (또는 이상) 또는 .NET Core를 설치 해야 합니다.

varbinary(max) 열에 FILESTREAM 특성을 지정하면 SQL Server에서는 데이터베이스 파일 대신 로컬 NTFS 파일 시스템에 데이터를 저장합니다. 별도로 데이터가 저장되지만 데이터베이스에 저장된 varbinary(max) 데이터로 작업할 때와 동일한 Transact-SQL 문을 사용할 수 있습니다.

## <a name="sqlclient-support-for-filestream"></a>FILESTREAM에 대 한 SqlClient 지원

Microsoft SqlClient Data Provider for SQL Server인 <xref:Microsoft.Data.SqlClient>에서는 <xref:System.Data.SqlTypes> 네임스페이스에 정의된 <xref:Microsoft.Data.SqlTypes.SqlFileStream> 클래스를 사용하여 FILESTREAM 데이터에 대한 읽기와 쓰기를 지원합니다. `SqlFileStream`은 데이터 스트림에 대 한 읽기 및 쓰기 메서드를 제공 하는 <xref:System.IO.Stream> 클래스에서 상속 됩니다. 스트림에서 읽으면 스트림의 데이터를 바이트 배열과 같은 데이터 구조로 전송 합니다. 쓰기는 데이터 구조에서 스트림으로 데이터를 전송 합니다.

### <a name="creating-the-sql-server-table"></a>SQL Server 테이블 만들기

다음 Transact-SQL 문은 employees라는 테이블을 만들어 데이터 행을 삽입합니다. FILESTREAM 저장소를 사용 하도록 설정한 후에는 다음 코드 예제와 함께이 테이블을 사용할 수 있습니다. SQL Server 온라인 설명서의 리소스 링크는 이 항목의 맨 마지막에 나옵니다.

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>예제: FILESTREAM 데이터 읽기, 덮어쓰기 및 삽입

다음 샘플에서는 FILESTREAM에서 데이터를 읽는 방법을 보여 줍니다. 이 코드는 파일에 대 한 논리적 경로를 가져와 `Read` `FileAccess`을 설정 하 고 `SequentialScan` `FileOptions`를 설정 합니다. 그런 다음 코드는 SqlFileStream에서 버퍼로 바이트를 읽습니다. 그러면 바이트가 콘솔 창에 기록 됩니다.

또한이 샘플에서는 모든 기존 데이터를 덮어쓰는 FILESTREAM에 데이터를 쓰는 방법을 보여 줍니다. 이 코드는 파일에 대 한 논리적 경로를 가져오고 `SqlFileStream`를 만들어 `FileAccess` `Write`으로 설정 하 고 `FileOptions`를 `SequentialScan`로 설정 합니다. 단일 바이트는 `SqlFileStream`에 기록 되 고 파일의 모든 데이터를 대체 합니다.

예제에서는 Seek 메서드를 사용하여 파일 끝에 데이터를 추가하는 방법으로 FILESTREAM에 데이터를 쓰는 방법도 보여 줍니다. 이 코드는 파일에 대 한 논리적 경로를 가져오고 `SqlFileStream`를 만들어 `FileAccess` `ReadWrite`으로 설정 하 고 `FileOptions`를 `SequentialScan`로 설정 합니다. 이 코드는 Seek 메서드를 사용 하 여 파일의 끝을 검색 하 고, 기존 파일에 싱글바이트를 추가 합니다.

```csharp
using System;
using Microsoft.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

다른 샘플은 [파일 스트림 열에 이진 데이터를 저장 및 페치하는 방법](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str)을 참조하세요.

## <a name="resources-in-sql-server-books-online"></a>SQL Server 온라인 설명서의 리소스

FILESTREAM에 대한 자세한 설명은 SQL Server 온라인 설명서의 다음 섹션에 나와 있습니다.

|항목|설명|
|-----------|-----------------|
|[FILESTREAM [SQL Server]](../../../relational-databases/blob/filestream-sql-server.md)|FILESTREAM 저장소를 사용 하는 시기와 NTFS 파일 시스템과 SQL Server 데이터베이스 엔진를 통합 하는 방법을 설명 합니다.|
|[FILESTREAM 데이터용 클라이언트 애플리케이션 만들기](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|FILESTREAM 데이터 작업을 위한 Windows API 함수에 대해 설명 합니다.|
|[다른 SQL Server 기능과 함께 FILESTREAM 사용](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|SQL Server의 다른 기능과 함께 FILESTREAM 데이터 사용에 대 한 고려 사항, 지침 및 제한 사항을 제공 합니다.|

## <a name="next-steps"></a>다음 단계
- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-large-value-data.md)
