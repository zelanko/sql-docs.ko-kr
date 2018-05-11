---
title: GET_FILESTREAM_TRANSACTION_CONTEXT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GET_FILESTREAM_TRANSACTION_CONTEXT_TSQL
- GET_FILESTREAM_TRANSACTION_CONTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- GET_FILESTREAM_TRANSACTION_CONTEXT FILESTREAM [SQL Server]
ms.assetid: 459e6b79-4420-41e6-85bf-89d90f43b4f1
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: de1709f83d00cf8afae0e6bedde156f3d9458889
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="getfilestreamtransactioncontext-transact-sql"></a>GET_FILESTREAM_TRANSACTION_CONTEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  세션의 현재 트랜잭션 컨텍스트를 나타내는 토큰을 반환합니다. 응용 프로그램은 이 토큰을 사용하여 FILESTREAM 파일 시스템 스트리밍 작업을 트랜잭션에 바인딩합니다. FILESTREAM 토픽의 목록은 [Binary Large Object&#40;Blob&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GET_FILESTREAM_TRANSACTION_CONTEXT ()  
```  
  
## <a name="return-type"></a>반환 형식  
 **varbinary(max)**  
  
## <a name="return-value"></a>반환 값  
 트랜잭션이 시작되지 않았거나 취소 또는 커밋된 경우 NULL이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 트랜잭션은 명시적이어야 합니다. BEGIN TRANSACTION을 사용한 다음 COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION을 사용합니다.  
  
 GET_FILESTREAM_TRANSACTION_CONTEXT를 호출하면 호출자에게 트랜잭션 기간 동안 트랜잭션에 대한 파일 시스템 액세스 권한이 부여됩니다. 다른 사용자가 파일 시스템을 통해 트랜잭션에 액세스할 수 있도록 하려면 EXECUTE AS를 사용하여 GET_FILESTREAM_TRANSACTION_CONTEXT를 다른 사용자로 실행합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 트랜잭션에 `GET_FILESTREAM_TRANSACTION_CONTEXT`를 사용하여 트랜잭션 컨텍스트를 구합니다.  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using System.Data;  
  
namespace ConsoleApplication  
{  
    /// <summary>  
    /// This class is a wrapper that contains methods for:  
    ///   
    ///     GetTransactionContect() - Returns the current transaction context.  
    ///     BeginTransaction() - Begins a transaction.  
    ///     CommmitTransaction() - Commits the current transaction.  
    ///   
    /// </summary>  
  
    class SqlAccessWrapper  
    {  
        /// <summary>  
        /// Returns a byte array that contains the current transaction  
        /// context.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the instance of SQL Server  
        /// from which to obtain the transaction context.   
        /// </param>  
        /// <returns>  
        /// If there is a current transaction context, the return  
        /// value is an Object that represents the context.  
        /// If there is not a current transaction context, the  
        /// value returned is DBNull.Value.  
        /// </returns>  
  
        public Object GetTransactionContext(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
            cmd.CommandText = "SELECT GET_FILESTREAM_TRANSACTION_CONTEXT()";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            return cmd.ExecuteScalar();  
  
        }  
  
        /// <summary>  
        /// Begins the transaction.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the server  
        /// on which to run the BEGIN TRANSACTION statement.  
        /// </param>  
  
        public void BeginTransaction(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
  
            cmd.CommandText = "BEGIN TRANSACTION";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            cmd.ExecuteNonQuery();  
        }  
  
        /// <summary>  
        /// Commits the transaction.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the instance of SQL Server  
        /// on which to run the COMMIT statement.  
        /// </param>  
  
        public void CommitTransaction(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
  
            cmd.CommandText = "COMMIT TRANSACTION";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            cmd.ExecuteNonQuery();  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            //Open a connection to the local instance of SQL Server.  
  
            SqlConnection sqlConnection = new SqlConnection("Integrated Security=true;server=(local)");  
            sqlConnection.Open();  
  
            SqlAccessWrapper sql = new SqlAccessWrapper();  
  
            //Create a transaction so that sql.GetTransactionContext() will succeed.  
            sql.BeginTransaction(sqlConnection);  
  
            //The transaction context will be stored in this array.  
            Byte[] transactionToken;     
  
            Object txObj = sql.GetTransactionContext(sqlConnection);  
            if (DBNull.Value != txObj)  
            {  
                transactionToken = (byte[])txObj;  
                Console.WriteLine("Transaction context obtained.\n");  
            }  
  
            sql.CommitTransaction(sqlConnection);  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data  
  
Namespace ConsoleApplication  
    ''' <summary>   
    ''' This class is a wrapper that contains methods for:   
    '''   
    ''' GetTransactionContect() - Returns the current transaction context.   
    ''' BeginTransaction() - Begins a transaction.   
    ''' CommmitTransaction() - Commits the current transaction.   
    '''   
    ''' </summary>   
  
    Class SqlAccessWrapper  
        ''' <summary>   
        ''' Returns a byte array that contains the current transaction   
        ''' context.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the instance of SQL Server   
        ''' from which to obtain the transaction context.   
        ''' </param>   
        ''' <returns>   
        ''' If there is a current transaction context, the return   
        ''' value is an Object that represents the context.   
        ''' If there is not a current transaction context, the   
        ''' value returned is DBNull.Value.   
        ''' </returns>   
  
        Public Function GetTransactionContext(ByVal sqlConnection As SqlConnection) As Object  
            Dim cmd As New SqlCommand()  
            cmd.CommandText = "SELECT GET_FILESTREAM_TRANSACTION_CONTEXT()"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            Return cmd.ExecuteScalar()  
  
        End Function  
  
        ''' <summary>   
        ''' Begins the transaction.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the server   
        ''' on which to run the BEGIN TRANSACTION statement.   
        ''' </param>   
  
        Public Sub BeginTransaction(ByVal sqlConnection As SqlConnection)  
            Dim cmd As New SqlCommand()  
  
            cmd.CommandText = "BEGIN TRANSACTION"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            cmd.ExecuteNonQuery()  
        End Sub  
  
        ''' <summary>   
        ''' Commits the transaction.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the instance of SQL Server   
        ''' on which to run the COMMIT statement.   
        ''' </param>   
  
        Public Sub CommitTransaction(ByVal sqlConnection As SqlConnection)  
            Dim cmd As New SqlCommand()  
  
            cmd.CommandText = "COMMIT TRANSACTION"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            cmd.ExecuteNonQuery()  
        End Sub  
    End Class  
  
    Class Program  
        Shared Sub Main()  
            '''Open a connection to the local instance of SQL Server.  
  
            Dim sqlConnection As New SqlConnection("Integrated Security=true;server=(local)")  
            sqlConnection.Open()  
  
            Dim sql As New SqlAccessWrapper()  
  
            '''Create a transaction so that sql.GetTransactionContext() will succeed.   
            sql.BeginTransaction(sqlConnection)  
  
            '''The transaction context will be stored in this array.   
            Dim transactionToken As Byte()  
  
            Dim txObj As Object = sql.GetTransactionContext(sqlConnection)  
  
            '''If the returned object is not NULL, there is a valid transaction  
            '''token, and it must be converted into a format that is usable within  
            '''the application.  
  
            If Not txObj.Equals(DBNull.Value) Then  
                transactionToken = DirectCast(txObj, Byte())  
                Console.WriteLine("Transaction context obtained." & Chr(10) & "")  
            End If  
  
            sql.CommitTransaction(sqlConnection)  
        End Sub  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a>참고 항목  
 [PathName&#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  
  
  
