---
title: 콘솔 애플리케이션에서 폴링
description: 폴링을 사용하여 콘솔 애플리케이션에서 비동기 명령 실행이 완료될 때까지 대기하는 방법을 보여주는 예제를 제공합니다. 이 기술은 클래스 라이브러리나 사용자 인터페이스가 없는 다른 애플리케이션에서도 유효합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 4ff084d5-5956-4db1-8e18-c5a66b000882
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bf89d2d111452970955953132edd76e602590668
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247682"
---
# <a name="polling-in-console-applications"></a>콘솔 애플리케이션에서 폴링

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET의 비동기 작업을 사용하면 다른 스레드에서 다른 작업을 수행하는 동안 하나의 스레드에서 시간이 많이 걸리는 데이터베이스 작업을 시작할 수 있습니다. 그러나 대부분의 시나리오에서는 데이터베이스 작업이 완료될 때까지 애플리케이션을 계속 실행해서는 안 되는 지점에 도달하게 됩니다. 이러한 경우 비동기 작업을 폴링하여 작업의 완료 여부를 확인하는 것이 유용합니다.  
  
작업 완료 여부는 <xref:System.IAsyncResult.IsCompleted%2A> 속성으로 확인할 수 있습니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 **AdventureWorks** 샘플 데이터베이스에서 데이터를 비동기적으로 업데이트합니다. 이 예제에서는 장기 실행 프로세스를 에뮬레이트할 수 있도록 명령 텍스트에 WAITFOR 문을 삽입합니다. 일반적으로는 명령이 느리게 실행되도록 하지는 않겠지만 이 경우에는 명령이 비교적 느려야 비동기 동작을 더 쉽게 확인할 수 있습니다.  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
    [STAThread]  
    static void Main()  
    {  
        // The WAITFOR statement simply adds enough time to   
        // prove the asynchronous nature of the command.  
  
        string commandText =  
          "UPDATE Production.Product SET ReorderPoint = " +  
          "ReorderPoint + 1 " +  
          "WHERE ReorderPoint Is Not Null;" +  
          "WAITFOR DELAY '0:0:3';" +  
          "UPDATE Production.Product SET ReorderPoint = " +  
          "ReorderPoint - 1 " +  
          "WHERE ReorderPoint Is Not Null";  
  
        RunCommandAsynchronously(  
            commandText, GetConnectionString());  
  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  
    private static void RunCommandAsynchronously(  
      string commandText, string connectionString)  
    {  
        // Given command text and connection string, asynchronously  
        // execute the specified command against the connection.   
        // For this example, the code displays an indicator as it's   
        // working, verifying the asynchronous behavior.   
        using (SqlConnection connection =  
          new SqlConnection(connectionString))  
        {  
            try  
            {  
                int count = 0;  
                SqlCommand command =   
                    new SqlCommand(commandText, connection);  
                connection.Open();  
  
                IAsyncResult result =   
                    command.BeginExecuteNonQuery();  
                while (!result.IsCompleted)  
                {  
                    Console.WriteLine(  
                                    "Waiting ({0})", count++);  
                    // Wait for 1/10 second, so the counter  
                    // doesn't consume all available   
                    // resources on the main thread.  
                    System.Threading.Thread.Sleep(100);  
                }  
                Console.WriteLine(  
                    "Command complete. Affected {0} rows.",  
                command.EndExecuteNonQuery(result));  
            }  
            catch (SqlException ex)  
            {  
                Console.WriteLine("Error ({0}): {1}",   
                    ex.Number, ex.Message);  
            }  
            catch (InvalidOperationException ex)  
            {  
                Console.WriteLine("Error: {0}", ex.Message);  
            }  
            catch (Exception ex)  
            {  
                // You might want to pass these errors  
                // back out to the caller.  
                Console.WriteLine("Error: {0}", ex.Message);  
            }  
        }  
    }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
  
        // If you have not included "Asynchronous Processing=true"  
        // in the connection string, the command will not be able  
        // to execute asynchronously.  
        return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks; " +   
        "Asynchronous Processing=true";  
    }  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [비동기 작업](asynchronous-operations.md)
