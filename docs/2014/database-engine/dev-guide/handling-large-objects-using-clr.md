---
title: CLR을 사용 하 여 큰 개체 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 4140d6b1-51cb-4d23-a4b6-8155360034fe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c7230150807b5bdd0849ea7ad5af00dbedb4ff3
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155669"
---
# <a name="handling-large-objects-using-clr"></a>CLR을 사용하여 큰 개체 처리
  SQL Server의 `HandlingLOBUsingCLR` 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 CLR(공용 언어 런타임) 저장 프로시저를 사용하여 서버에서 사용할 수 있는 파일 시스템 간의 LOB(Large Object) 전송을 보여 줍니다. 이 예제에서는 서버 쪽 코드의 파일에 액세스하고 CLR 기반 저장 프로시저로부터 동적 쿼리와 저장 프로시저를 모두 호출하는 방법을 보여 줍니다. 또한 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 CLR 메서드와 어셈블리를 등록 및 등록 해제하는 방법을 보여 줍니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 프로젝트를 만들고 실행하려면 다음 소프트웨어가 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 설명서 및 예제 [웹 사이트](https://go.microsoft.com/fwlink/?LinkId=31046)에서 무료로 구할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개발자 [웹 사이트](https://go.microsoft.com/fwlink/?linkid=62796)에서 제공되는 AdventureWorks 데이터베이스  
  
-   .NET Framework SDK 2.0 이상 또는 Microsoft Visual Studio 2005 이상. .NET Framework SDK는 무료로 구할 수 있습니다.  
  
-   또한 다음 조건을 충족해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 CLR 통합이 설정되어 있어야 합니다.  
  
-   CLR 통합을 설정하려면 다음 단계를 수행합니다.  
  
    #### <a name="enabling-clr-integration"></a>CLR 통합 사용  
  
    -   다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행합니다.  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  CLR을 사용하도록 설정하려면 `ALTER SETTINGS` 서버 수준 사용 권한이 있어야 합니다. 이 사용 권한은 `sysadmin` 및 `serveradmin` 고정 서버 역할의 멤버가 암시적으로 소유합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 AdventureWorks 데이터베이스를 설치해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자가 아닌 경우 설치를 완료하기 위해 관리자로부터 **CreateAssembly**  권한을 부여 받아야 합니다.  
  
## <a name="building-the-sample"></a>예제 빌드  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>다음 지침을 사용하여 예제를 만들고 실행합니다.  
  
1.  Visual Studio 또는 .NET Framework 명령 프롬프트를 엽니다.  
  
2.  필요한 경우 예제에 대한 디렉터리를 만듭니다. 이 예에서는 C:\MySample을 사용합니다.  
  
3.  이 예에는 서명된 어셈블리가 필요하므로 다음 명령을 입력하여 비대칭 키를 만듭니다.  
  
## <a name="sample-code"></a>예제 코드  
 다음은 이 예제에 대한 코드 목록입니다.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.IO;  
using System.Globalization;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
  
    public sealed class LargeObjectBinary  
    {  
        //Recommended chunk size for processing large amounts of data  
        private const int bufferSize = 4000;  
  
        /// <summary>  
        ///This class only contains static members, therefore it needs no public constructor.  
        /// </summary>  
        private LargeObjectBinary()  
        {  
        }  
  
        /// <summary>  
        /// Retrieves a thumbnail photograph from the database into a file assessible to the server.    
        /// </summary>  
        /// <param name="photoId">Unique identifier for a product picture.</param>  
        /// <param name="currentDirectory">Which folder to put the picture into.</param>  
        /// <param name="fileName">What to call the picture in the specified folder.</param>  
        public static void GetPhotoFromDB(Int32 photoId, string currentDirectory, string fileName)  
        {  
            SqlDataReader sqlReader = null;  
  
            SqlConnection conn = new SqlConnection("context connection = true");  
            conn.Open();  
  
            SqlCommand sprocCommand = conn.CreateCommand();  
            //Even though we are supply an int, it is a good habit to use parameters to insert  
            //values into command text rather than using String.Format.  In the case of string parameters, it can  
            //help prevent injection attacks.  
            sprocCommand.CommandText = "SELECT ThumbNailPhoto FROM Production.ProductPhoto WHERE ProductPhotoID = @ProductPhotoID";  
            sprocCommand.Parameters.Add("@ProductPhotoID", SqlDbType.Int);  
            sprocCommand.Parameters[0].Value = photoId;  
  
            //TODO: Is getting chunks the best way to retrieve LOB from the database?  Is there a limit?  
            try  
            {  
                sqlReader = sprocCommand.ExecuteReader( //CommandBehavior.SequentialAccess  
                    );  
                if (sqlReader == null)  
                {  
                    LogError(currentDirectory, "ExecuteReader failed!");  
                }  
                else  
                {  
                    if (sqlReader.Read())  
                    {  
                        // Create a file to hold the output.  
                        if (!Directory.Exists(currentDirectory))  
                            Directory.CreateDirectory(currentDirectory);  
                        fileName = currentDirectory + fileName;  
                        using (FileStream fileStream = new FileStream(fileName,  
                                                                      FileMode.  
                                                                      OpenOrCreate,  
                                                                      FileAccess.  
                                                                      Write))  
                        {  
                            using (BinaryWriter binaryWriter =  
                                                new BinaryWriter(  
                                fileStream))  
                            {  
                                // The BLOB byte[] buffer to be filled by GetBytes.  
                                byte[] outbyte = new byte[bufferSize];  
  
                                // The starting position in the BLOB output.  
                                long startIndex = 0;  
  
                                // Read the bytes into outbyte[] and retain the number of bytes returned.  
                                long retval = sqlReader.GetBytes(0, startIndex,  
                                                                 outbyte, 0,  
                                                                 bufferSize);  
  
                                // Continue reading and writing while there are bytes beyond the size of the buffer.  
                                while (retval == bufferSize)  
                                {  
                                    binaryWriter.Write(outbyte);  
  
                                    // Reposition the start index to the end of the last buffer and fill the buffer.  
                                    startIndex += bufferSize;  
                                    retval = sqlReader.GetBytes(0, startIndex,  
                                                                outbyte, 0,  
                                                                bufferSize);  
                                }  
  
                                // Write the remaining buffer.  
                                binaryWriter.Write(outbyte);  
                                //TODO:  Shouldn't need to flush here because the close will do it for me?  
                                //binaryWriter.Flush();  
                            }  
                        }  
                    }  
                    else  
                        LogError(currentDirectory, "No row returned!");  
                }  
            }  
            catch (SqlException e)  
            {  
                LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, "Unable to copy binary contents from database.  Error: {0}", e.ToString()));  
            }  
            finally  
            {  
                if (sqlReader != null)  
                    sqlReader.Close();  
  
                //dispose the conn  
                if (conn != null)  
                {  
                    conn.Close();  
                    conn.Dispose();  
                }  
            }  
        }  
  
        /// <summary>  
        /// Saves a thumbnail picture into the database from a file accessible to the server.  
        /// </summary>  
        /// <param name="photoId">Unique identifier for a product picture.</param>  
        /// <param name="currentDirectory">Which folder to get the picture from.</param>  
        /// <param name="fileName">What the picture in the specified folder is called.</param>  
        public static void PutPhotoIntoDB(Int32 photoId, string currentDirectory, string fileName)  
        {  
            //TODO: Is there a limit on how large the LOB can be?  
            string fullFileName = currentDirectory + fileName;  
            byte[] bytes = ReadFile(fullFileName);  
  
            try  
            {  
                SqlConnection conn = new SqlConnection("context connection = true");  
                conn.Open();  
  
                SqlCommand sprocCommand = conn.CreateCommand();  
                sprocCommand.CommandText = "dbo.usp_UpdateImage";  
                sprocCommand.CommandType = CommandType.StoredProcedure;  
  
                sprocCommand.Parameters.Add(new SqlParameter("@ProductPhotoID", SqlDbType.Int));  
                // Add time to the short name because there is an unique constraint on this column.  
                sprocCommand.Parameters[0].Value = photoId;  
                sprocCommand.Parameters.Add(new SqlParameter("@ThumbNailPhoto", SqlDbType.VarBinary));  
                sprocCommand.Parameters[1].Value = bytes;  
                sprocCommand.ExecuteNonQuery();  
            }  
            catch (SqlException e)  
            {  
                LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, "Unable to update binary contents into the database.  Error: {0}", e.ToString()));  
            }  
        }  
  
        /// <summary>  
        /// Read the contents of a file and return the bytes.  
        /// </summary>  
        /// <param name="fileName">The name of the file to be read.</param>  
        /// <returns></returns>  
        private static byte[] ReadFile(string fileName)  
        {  
            // Open the file assuming the file is in ASCII format.  
            using (BinaryReader binaryReader = new BinaryReader((Stream)File.OpenRead(fileName), System.Text.Encoding.ASCII))  
            {  
                long fileSize = binaryReader.BaseStream.Length;  
                byte[] bytes = new Byte[fileSize];  
                binaryReader.Read(bytes, 0, (int)fileSize);  
                return bytes;  
            }  
        }  
  
        /// <summary>  
        ///Appends a message to a file accessible to the server.  When System.Diagnostics is available from  
        /// CLR Sprocs this should be changed to use the event log.  
        /// </summary>  
        /// <param name="currentDirectory">Which folder the message log file resides in</param>  
        /// <param name="errorMessage">The text to add to the message log file</param>  
        private static void LogError(string currentDirectory, string errorMessage)  
        {  
            using (FileStream errorLogStream = new FileStream(currentDirectory + "error.log", FileMode.Append, FileAccess.Write))  
            {  
                using (StreamWriter errorLogWriter = new StreamWriter(errorLogStream))  
                {  
                    errorLogWriter.WriteLine(errorMessage);  
                }  
            }  
        }  
    }  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Diagnostics  
Imports System.Globalization  
Imports System.IO  
Imports System.Reflection  
  
Public NotInheritable Class LargeObjectBinary  
    'Recommended chunk size for processing large amounts of data  
    Private Const bufferSize As Integer = 4000  
  
    ''' <summary>  
    '''    This class only contains static members, therefore it needs no public constructor.  
    ''' </summary>  
    Private Sub New()  
    End Sub  
  
    ''' <summary>  
    ''' Retrieves a thumbnail photograph from the database into a file assessible to the server.    
    ''' </summary>  
    ''' <param name="photoId">Unique identifier for a product picture.</param>  
    ''' <param name="currentDirectory">Which folder to put the picture into.</param>  
    ''' <param name="fileName">What to call the picture in the specified folder.</param>  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub GetPhotoFromDB(ByVal photoId As Integer, _  
        ByVal currentDirectory As String, ByVal fileName As String)  
        Dim sqlReader As SqlDataReader = Nothing  
  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")  
        conn.Open()  
  
        Dim sprocCommand As SqlCommand = conn.CreateCommand()  
        'Even though we are supply an int, it is a good habit to use parameters to insert  
        'values into command text rather than using String.Format.  In the   
        'case of string parameters, it can help prevent injection attacks.  
        sprocCommand.CommandText = "SELECT ThumbNailPhoto FROM Production.ProductPhoto " _  
            & "WHERE ProductPhotoID = @ProductPhotoID"  
        sprocCommand.Parameters.Add("@ProductPhotoID", SqlDbType.Int)  
        sprocCommand.Parameters(0).Value = photoId  
  
        'TODO: Is getting chunks the best way to retrieve LOB from the database?  Is there a limit?  
        Try  
            sqlReader = sprocCommand.ExecuteReader() 'CommandBehavior.SequentialAccess  
            If sqlReader Is Nothing Then  
                LogError(currentDirectory, "ExecuteReader failed!")  
            Else  
                If sqlReader.Read() Then  
                    ' Create a file to hold the output.  
                    If (Not Directory.Exists(currentDirectory)) Then  
                        Directory.CreateDirectory(currentDirectory)  
                    End If  
  
                    fileName = currentDirectory + fileName  
                    Dim fileStream As New FileStream(fileName, FileMode.OpenOrCreate, FileAccess.Write)  
                    Try  
                        Dim binaryWriter As New BinaryWriter(fileStream)  
                        Try  
                            ' The BLOB byte() buffer to be filled by GetBytes.  
                            Dim outbyte(bufferSize) As Byte  
  
                            ' The starting position in the BLOB output.  
                            Dim startIndex As Long = 0  
  
                            ' Read the bytes into outbyte() and retain the number of bytes returned.  
                            Dim retval As Long = sqlReader.GetBytes(0, startIndex, outbyte, 0, bufferSize)  
  
                            ' Continue reading and writing while there are   
                            ' bytes beyond the size of the buffer.  
                            While retval = bufferSize  
                                binaryWriter.Write(outbyte)  
  
                                ' Reposition the start index to the end of   
                                ' the last buffer and fill the buffer.  
                                startIndex += bufferSize  
                                retval = sqlReader.GetBytes(0, startIndex, outbyte, 0, bufferSize)  
                            End While  
  
                            ' Write the remaining buffer.  
                            binaryWriter.Write(outbyte)  
                        Finally  
                            binaryWriter.Close()  
                        End Try  
                    Finally  
                        fileStream.Close()  
                    End Try 'binaryWriter.Flush();  
                Else  
                    LogError(currentDirectory, "No row returned!")  
                End If  
            End If  
        Catch e As SqlException  
            LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, _  
                "Unable to copy binary contents from database.  Error: {0}", e.ToString()))  
        Finally  
            If Not (sqlReader Is Nothing) Then  
                sqlReader.Close()  
            End If  
            'dispoae the conn  
            If Not (conn Is Nothing) Then  
                conn.Close()  
                conn.Dispose()  
            End If  
        End Try  
    End Sub  
  
    ''' <summary>  
    ''' Saves a thumbnail picture into the database from a file accessible to the server.  
    ''' </summary>  
    ''' <param name="photoId">Unique identifier for a product picture.</param>  
    ''' <param name="currentDirectory">Which folder to get the picture from.</param>  
    ''' <param name="fileName">What the picture in the specified folder is called.</param>  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub PutPhotoIntoDB(ByVal photoId As Integer, _  
        ByVal currentDirectory As String, ByVal fileName As String)  
        'TODO: Is there a limit on how large the LOB can be?  
        Dim fullFileName As String = currentDirectory + fileName  
        Dim bytes As Byte() = ReadFile(fullFileName)  
  
        Try  
            Dim conn As SqlConnection = New SqlConnection("context connection = true")  
            conn.Open()  
  
            Dim sprocCommand As SqlCommand = conn.CreateCommand()  
            sprocCommand.CommandText = "dbo.usp_UpdateImage"  
            sprocCommand.CommandType = CommandType.StoredProcedure  
  
            sprocCommand.Parameters.Add(New SqlParameter("@ProductPhotoID", SqlDbType.Int))  
            ' Add time to the short name because there is an unique constraint on this column.  
            sprocCommand.Parameters(0).Value = photoId  
            sprocCommand.Parameters.Add(New SqlParameter("@ThumbNailPhoto", SqlDbType.VarBinary))  
            sprocCommand.Parameters(1).Value = bytes  
            sprocCommand.ExecuteNonQuery()  
        Catch e As SqlException  
            LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, _  
                "Unable to update binary contents into the database.  Error: {0}", e.ToString()))  
        End Try  
    End Sub  
  
    ''' <summary>  
    ''' Read the contents of a file and return the bytes.  
    ''' </summary>  
    ''' <param name="fileName">The name of the file to be read.</param>  
    ''' <returns></returns>  
    Private Shared Function ReadFile(ByVal fileName As String) As Byte()  
        ' Open the file assuming the file is in ASCII format.  
        'Dim binaryReader As New BinaryReader(CType(File.OpenRead(fileName), Stream), System.Text.Encoding.ASCII)  
        'Try  
        '    Dim fileSize As Long = binaryReader.BaseStream.Length  
        '    Dim bytes() As Byte = New Byte(CType(fileSize, Integer)) {}  
        '    binaryReader.Read(bytes, 0, CType(fileSize, Integer))  
        '    Return bytes  
        'Finally  
        '    binaryReader.Close()  
        'End Try  
  
        Dim binaryReader As New BinaryReader(CType(File.OpenRead(fileName), Stream), System.Text.Encoding.ASCII)  
        Using (binaryReader)  
            Dim fileSize As Long = binaryReader.BaseStream.Length  
            Dim bytes() As Byte = New Byte(CType(fileSize, Integer)) {}  
            binaryReader.Read(bytes, 0, CType(fileSize, Integer))  
            Return bytes  
        End Using  
  
    End Function  
  
    ''' <summary>  
    '''        Appends a message to a file accessible to the server.  When System.Diagnostics is available from  
    '''        CLR Sprocs this should be changed to use the event log.  
    ''' </summary>  
    ''' <param name="currentDirectory">Which folder the message log file resides in</param>  
    ''' <param name="errorMessage">The text to add to the message log file</param>  
    Private Shared Sub LogError(ByVal currentDirectory As String, ByVal errorMessage As String)  
        Dim errorLogStream As New FileStream(currentDirectory + "error.log", FileMode.Append, FileAccess.Write)  
        Try  
            Dim errorLogWriter As New StreamWriter(errorLogStream)  
            Try  
                errorLogWriter.WriteLine(errorMessage)  
            Finally  
                errorLogWriter.Close()  
            End Try  
        Finally  
            errorLogStream.Close()  
        End Try  
    End Sub  
End Class  
  
```  
  
 이는 어셈블리를 배포하고 이 예에 필요한 저장 프로시저 및 보안 개체를 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 스크립트(`Install.sql`)입니다.  
  
```  
USE AdventureWorks  
GO  
  
-- Drop procedures defined in this script if they exist  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_UpdateImage')  
DROP PROCEDURE [dbo].[usp_UpdateImage];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'GetPhotoFromDB')  
DROP PROCEDURE [dbo].[GetPhotoFromDB];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'PutPhotoIntoDB')  
DROP PROCEDURE [dbo].[PutPhotoIntoDB];  
GO  
  
-- If the assembly we want to add already exists, drop it.  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'HandlingLOBUsingCLR')  
DROP ASSEMBLY HandlingLOBUsingCLR;  
GO  
use master  
go  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
--Before we register the assembly to SQL Server, we must arrange for the appropriate permissions.  
--Assemblies with unsafe or external_access permissions can only be registered and operate correctly  
--if either the database trustworthy bit is set or if the assembly is signed with a key,  
--that key is registered with SQL Server, a server principal is created from that key,  
--and that principal is granted the external access or unsafe assembly permission.  We choose  
--the latter approach as it is more granular, and therefore safer.  You should never  
--register an assembly with SQL Server (especially with external_access or unsafe permissions) without  
--thoroughly reviewing the source code of the assembly to make sure that its actions   
--do not pose an operational or security risk for your site.  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = N'C:\MySample\'  
  
EXEC('CREATE ASYMMETRIC KEY ExternalSample_Key FROM EXECUTABLE FILE = ''' + @SamplesPath + 'HandlingLOBUsingCLR.dll'';');  
CREATE LOGIN ExternalSample_Login FROM ASYMMETRIC KEY ExternalSample_Key  
GRANT EXTERNAL ACCESS ASSEMBLY TO ExternalSample_Login  
GO  
  
USE AdventureWorks  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = N'C:\MySample\'  
CREATE ASSEMBLY HandlingLOBUsingCLR  
FROM @SamplesPath + 'HandlingLOBUsingCLR.dll'  
WITH permission_set = external_access;  
GO  
  
-- Register the CLR method for retrieving thumbnail photos from the ProductPhoto table  
  
CREATE PROCEDURE [dbo].[GetPhotoFromDB]  
(  
    @ProductPhotoID int  
    ,@CurrentDirectory nvarchar(1024)  
    ,@FileName nvarchar(1024)     
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.[LargeObjectBinary].GetPhotoFromDB;  
GO  
  
-- Register the CLR method for storing thumbnail photos into the ProductPhoto table  
  
CREATE PROCEDURE [dbo].[PutPhotoIntoDB]  
(  
    @ProductPhotoID int  
    ,@CurrentDirectory nvarchar(1024)  
    ,@FileName nvarchar(1024)     
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.[LargeObjectBinary].PutPhotoIntoDB;  
GO  
  
-- Add a helper T-SQL method which does the actual work of updating the row  
  
CREATE PROCEDURE [dbo].[usp_UpdateImage]  
/* **********************************************************************************  
   Date:    April 22, 2003  
   Purpose: Change a thumbnail picture stored in the ProductPhoto table.  
   ********************************************************************************** */  
    @ProductPhotoID int  
    ,@ThumbNailPhoto AS VARBINARY(max)  
AS  
BEGIN  
    SET NOCOUNT ON;  
  
BEGIN TRY  
    UPDATE Production.ProductPhoto   
        SET ThumbNailPhoto = @ThumbNailPhoto  
        WHERE ProductPhotoID = @ProductPhotoID;  
    IF(@@ROWCOUNT < 1)  
        RAISERROR ('Update failed.', 16, 1);  
END TRY  
BEGIN CATCH  
        SELECT   
ERROR_NUMBER() AS ErrorNumber,  
ERROR_SEVERITY() AS ErrorSeverity,  
ERROR_STATE() as ErrorState,  
ERROR_PROCEDURE() as ErrorProcedure,  
ERROR_LINE() as ErrorLine,  
ERROR_MESSAGE() as ErrorMessage;  
        RAISERROR ('Update failed.', 16, 1);  
END CATCH;  
END  -- END of sp_InsertDocument  
GO  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] (`test.sql`)에서는 저장 프로시저를 실행하여 예를 테스트합니다.  
  
```  
USE AdventureWorks  
GO  
  
EXEC GetPhotoFromDB 70, 'C:\Temp\', 'test6.gif';  
go  
  
EXEC PutPhotoIntoDB 70, 'C:\Temp\', 'test6.gif';  
go  
  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 은 데이터베이스에서 어셈블리, 로그인, 키 및 저장 프로시저를 제거합니다.  
  
```  
  
USE AdventureWorks  
GO  
  
-- Drop procedures defined in the install script if they exist  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_UpdateImage')  
DROP PROCEDURE [dbo].[usp_UpdateImage];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'GetPhotoFromDB')  
DROP PROCEDURE [dbo].[GetPhotoFromDB];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'PutPhotoIntoDB')  
DROP PROCEDURE [dbo].[PutPhotoIntoDB];  
GO  
  
-- If the assembly exists, drop it.  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'HandlingLOBUsingCLR')  
DROP ASSEMBLY HandlingLOBUsingCLR;  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
USE AdventureWorks  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
