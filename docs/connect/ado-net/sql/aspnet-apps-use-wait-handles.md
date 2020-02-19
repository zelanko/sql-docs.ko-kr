---
title: 대기 핸들을 사용하는 ASP.NET 애플리케이션
description: 모든 명령이 완료될 때 대기 핸들로 작업을 관리해 ASP.NET 페이지의 동시 명령을 어떻게 실행할 수 있을지를 예제로 시연합니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 0550b67d32d18aa9095b316816ebcbf3494cf195
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250962"
---
# <a name="aspnet-applications-using-wait-handles"></a>대기 핸들을 사용하는 ASP.NET 애플리케이션

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

애플리케이션에서 한 번에 비동기 작업 하나만 처리할 때는 비동기 작업 처리를 위한 콜백 및 폴링 모델이 유용합니다. Wait 모델은 여러 비동기 작업을 보다 유연하게 처리하는 방법을 제공합니다. Wait 모델에는 두 가지가 있는데, 구현에 쓰이는 <xref:System.Threading.WaitHandle> 메서드의 이름을 따서 Wait(Any) 모델과 Wait(All) 모델로 불립니다.  
  
Wait 모델 둘 중 하나를 사용하려면 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 또는 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 메서드에서 반환되는 <xref:System.IAsyncResult> 개체의 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 속성을 사용해야 합니다. <xref:System.Threading.WaitHandle.WaitAny%2A> 및 <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드에서는 <xref:System.Threading.WaitHandle> 개체를 배열에 함께 그룹화된 인수로서 전송해야 합니다.  
  
두 Wait 모델은 모두 비동기 작업을 모니터링하며 완료까지 대기합니다. <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드는 작업이 완료되거나 시간이 초과되기를 기다립니다. 특정 작업이 완료되면 해당 결과를 처리한 다음 계속해서 다음 작업이 완료되거나 시간이 초과되기를 기다릴 수 있습니다. <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드는 <xref:System.Threading.WaitHandle> 인스턴스 배열의 모든 프로세스가 완료되거나 시간이 초과되기를 기다린 후 계속해서 프로세스를 진행합니다.  
  
Wait 모델은 다른 서버에서 특정 길이의 여러 작업을 실행해야 하는 경우, 또는 서버가 모든 쿼리를 동시에 처리할 수 있을 정도로 강력한 경우에 그 장점이 가장 두드러집니다. 여기의 예제에서는 3개의 쿼리가 다양한 길이의 WAITFOR 명령을 중요하지 않은 SELECT 쿼리에 추가하여 긴 프로세스를 에뮬레이트합니다.  
  
## <a name="example-wait-any-model"></a>예제: Wait(Any) 모델  
다음 예제에서는 Wait(Any) 모델을 설명합니다. 3개의 비동기 프로세스가 시작되면 <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드가 호출되어 셋 중 하나가 완료될 때까지 대기합니다. 각 프로세스가 완료되면 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 메서드가 호출되고 <xref:Microsoft.Data.SqlClient.SqlDataReader> 개체가 읽힙니다. 이 시점에서 실제 애플리케이션은 <xref:Microsoft.Data.SqlClient.SqlDataReader>를 사용하여 페이지의 일부를 채울 수 있습니다. 이 간단한 예제에서는 프로세스 완료 시간이 프로세스에 해당하는 텍스트 상자에 추가됩니다. 종합하여 볼 때 텍스트 상자의 시간을 보면 알 수 있는 점이 있는데, 바로 프로세스가 완료될 때마다 코드가 실행된다는 사실입니다.  
  
이 예제를 설정하려면 새 ASP.NET 웹 사이트 프로젝트를 만듭니다. 각 컨트롤에 대해 기본 이름을 적용하여 페이지에 <xref:System.Web.UI.WebControls.Button> 컨트롤 1개와 <xref:System.Web.UI.WebControls.TextBox> 컨트롤 4개를 배치합니다.  
  
사용자의 환경에 필요한 대로 연결 문자열을 수정하여 양식의 클래스에 다음 코드를 추가합니다.  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
     //  To avoid storing the connection string in your code,              
     //  you can retrieve it from a configuration file.   
     //  If you have not included "Asynchronous Processing=true"   
     //  in the connection string, the command will not be able  
     //  to execute asynchronously.  
{  
     return "Data Source=(local);Integrated Security=SSPI;" +  
          "Initial Catalog=AdventureWorks;" +  
          "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
     //  In a real-world application, you might be connecting to   
     //   three different servers or databases. For the example,  
     //   we connect to only one.  
  
     SqlConnection connection1 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection2 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection3 =   
          new SqlConnection(GetConnectionString());  
     //  To keep the example simple, all three asynchronous   
     //  processes select a row from the same table. WAITFOR  
     //  commands are used to emulate long-running processes  
     //  that complete after different periods of time.  
  
     string commandText1 = "WAITFOR DELAY '0:0:01';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText2 = "WAITFOR DELAY '0:0:05';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText3 = "WAITFOR DELAY '0:0:10';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     try  
          //  For each process, open a connection and begin   
          //  execution. Use the IAsyncResult object returned by   
          //  BeginExecuteReader to add a WaitHandle for the   
          //  process to the array.  
     {  
          connection1.Open();  
          SqlCommand command1 =  
               new SqlCommand(commandText1, connection1);  
          IAsyncResult result1 = command1.BeginExecuteReader();  
          WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
  
          connection2.Open();  
          SqlCommand command2 =  
               new SqlCommand(commandText2, connection2);  
          IAsyncResult result2 = command2.BeginExecuteReader();  
          WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
  
          connection3.Open();  
          SqlCommand command3 =  
               new SqlCommand(commandText3, connection3);  
          IAsyncResult result3 = command3.BeginExecuteReader();  
          WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
          WaitHandle[] waitHandles = {  
               waitHandle1, waitHandle2, waitHandle3  
          };  
  
          int index;  
          for (int countWaits = 0; countWaits <= 2; countWaits++)  
          {  
               //  WaitAny waits for any of the processes to   
               //  complete. The return value is either the index   
               //  of the array element whose process just   
               //  completed, or the WaitTimeout value.  
  
               index = WaitHandle.WaitAny(waitHandles,   
                    60000, false);  
               //  This example doesn't actually do anything with   
               //  the data returned by the processes, but the   
               //  code opens readers for each just to demonstrate       
               //  the concept.  
               //  Instead of using the returned data to fill the   
               //  controls on the page, the example adds the time  
               //  the process was completed to the corresponding  
               //  text box.  
  
               switch (index)  
               {  
                    case 0:  
                         SqlDataReader reader1;  
                         reader1 =   
                              command1.EndExecuteReader(result1);  
                         if (reader1.Read())  
                         {  
                           TextBox1.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader1.Close();  
                         break;  
                    case 1:  
                         SqlDataReader reader2;  
                         reader2 =   
                              command2.EndExecuteReader(result2);  
                         if (reader2.Read())  
                         {  
                           TextBox2.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader2.Close();  
                         break;  
                    case 2:  
                         SqlDataReader reader3;  
                         reader3 =   
                              command3.EndExecuteReader(result3);  
                         if (reader3.Read())  
                         {  
                           TextBox3.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader3.Close();  
                         break;  
                    case WaitHandle.WaitTimeout:  
                         throw new Exception("Timeout");  
                         break;  
               }  
          }  
     }  
     catch (Exception ex)  
     {  
          TextBox4.Text = ex.ToString();  
     }  
     connection1.Close();  
     connection2.Close();  
     connection3.Close();  
}  
```  
  
## <a name="example-wait-all-model"></a>예제: Wait(All) 모델  
다음 예제에서는 Wait(All) 모델을 설명합니다. 3개의 비동기 프로세스가 시작되면 <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드가 호출되어 프로세스 완료나 시간 초과까지 대기합니다.  
  
Wait(Any) 모델의 예제와 마찬가지로 여기서도 프로세스 완료 시간이 프로세스에 해당하는 텍스트 상자에 추가됩니다. 이때도 텍스트 상자의 시간을 보면 알 수 있는 점이 있는데, <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드 다음의 코드는 모든 프로세스가 완료된 후에만 실행된다는 사실입니다.  
  
이 예제를 설정하려면 새 ASP.NET 웹 사이트 프로젝트를 만듭니다. 각 컨트롤에 대해 기본 이름을 적용하여 페이지에 <xref:System.Web.UI.WebControls.Button> 컨트롤 1개와 <xref:System.Web.UI.WebControls.TextBox> 컨트롤 4개를 배치합니다.  
  
사용자의 환경에 필요한 대로 연결 문자열을 수정하여 양식의 클래스에 다음 코드를 추가합니다.  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
    //  To avoid storing the connection string in your code,              
    //  you can retrieve it from a configuration file.   
    //  If you have not included "Asynchronous Processing=true"   
    //  in the connection string, the command will not be able  
    //  to execute asynchronously.  
{  
    return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks;" +  
        "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
    //  In a real-world application, you might be connecting to   
    //   three different servers or databases. For the example,  
    //   we connect to only one.  
  
    SqlConnection connection1 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection2 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection3 =   
        new SqlConnection(GetConnectionString());  
    //  To keep the example simple, all three asynchronous   
    //  processes execute UPDATE queries that result in  
      //  no change to the data. WAITFOR  
    //  commands are used to emulate long-running processes  
    //  that complete after different periods of time.  
  
    string commandText1 =   
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint + 1 " +  
        "WHERE ReorderPoint Is Not Null;" +  
        "WAITFOR DELAY '0:0:01';" +  
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint - 1 " +  
        "WHERE ReorderPoint Is Not Null";  
  
    string commandText2 =   
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint + 1 " +  
      "WHERE ReorderPoint Is Not Null;" +  
      "WAITFOR DELAY '0:0:05';" +  
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint - 1 " +  
      "WHERE ReorderPoint Is Not Null";  
  
    string commandText3 =  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint + 1 " +  
       "WHERE ReorderPoint Is Not Null;" +  
       "WAITFOR DELAY '0:0:10';" +  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint - 1 " +  
       "WHERE ReorderPoint Is Not Null";  
    try  
        //  For each process, open a connection and begin   
        //  execution. Use the IAsyncResult object returned by   
        //  BeginExecuteReader to add a WaitHandle for the   
        //  process to the array.  
    {  
        connection1.Open();  
        SqlCommand command1 =  
            new SqlCommand(commandText1, connection1);  
        IAsyncResult result1 = command1.BeginExecuteNonQuery();  
        WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
        connection2.Open();  
  
        SqlCommand command2 =  
            new SqlCommand(commandText2, connection2);  
        IAsyncResult result2 = command2.BeginExecuteNonQuery();  
        WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
        connection3.Open();  
  
        SqlCommand command3 =  
            new SqlCommand(commandText3, connection3);  
        IAsyncResult result3 = command3.BeginExecuteNonQuery();  
        WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
        WaitHandle[] waitHandles = {  
            waitHandle1, waitHandle2, waitHandle3  
        };  
  
        bool result;  
        //  WaitAll waits for all of the processes to   
        //  complete. The return value is True if the processes  
        //  all completed successfully, False if any process  
        //  timed out.  
  
        result = WaitHandle.WaitAll(waitHandles, 60000, false);  
        if(result)  
        {  
            long rowCount1 =   
                command1.EndExecuteNonQuery(result1);  
            TextBox1.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
            long rowCount2 =   
                command2.EndExecuteNonQuery(result2);  
            TextBox2.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
  
            long rowCount3 =   
                command3.EndExecuteNonQuery(result3);  
            TextBox3.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
        }  
        else  
        {  
            throw new Exception("Timeout");  
        }  
    }  
  
    catch (Exception ex)  
    {  
        TextBox4.Text = ex.ToString();  
    }  
    connection1.Close();  
    connection2.Close();  
    connection3.Close();  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [비동기 작업](asynchronous-operations.md)
