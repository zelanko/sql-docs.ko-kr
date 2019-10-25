---
title: 콘솔 애플리케이션에서 폴링
description: 폴링을 사용 하 여 콘솔 응용 프로그램에서 비동기 명령 실행이 완료 될 때까지 대기 하는 방법을 보여 주는 예제를 제공 합니다. 이 기술은 클래스 라이브러리나 사용자 인터페이스가 없는 다른 응용 프로그램 에서도 유효 합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 4ff084d5-5956-4db1-8e18-c5a66b000882
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: e8dc5597743a277b53f36d0bfb1487a12cbd80d9
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452105"
---
# <a name="polling-in-console-applications"></a>콘솔 애플리케이션에서 폴링

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET의 비동기 작업을 사용 하면 다른 스레드에서 다른 작업을 수행 하는 동안 한 스레드에서 시간이 많이 걸리는 데이터베이스 작업을 시작할 수 있습니다. 그러나 대부분의 시나리오에서는 데이터베이스 작업이 완료 될 때까지 응용 프로그램을 계속 실행 하지 않아야 하는 지점에 도달 하 게 됩니다. 이러한 경우 비동기 작업을 폴링하여 작업이 완료 되었는지 여부를 확인 하는 것이 유용 합니다.  
  
@No__t_0 속성을 사용 하 여 작업이 완료 되었는지 여부를 확인할 수 있습니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 **AdventureWorks** 샘플 데이터베이스에서 데이터를 비동기적으로 업데이트합니다. 이 예에서는 장기 실행 프로세스를 에뮬레이트 하기 위해 명령 텍스트에 WAITFOR 문을 삽입 합니다. 일반적으로 명령이 느리게 실행 되는 것을 시도 하지는 않지만이 경우에는 비동기 동작을 보다 쉽게 보여 줄 수 있습니다.  
  
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
