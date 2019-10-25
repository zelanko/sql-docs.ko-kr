---
title: 대기 핸들을 사용하는 ASP.NET 애플리케이션
description: 모든 명령이 완료 될 때 대기 핸들을 사용 하 여 작업을 관리 하는 ASP.NET 페이지에서 여러 동시 명령을 실행 하는 방법을 보여 주는 예제를 제공 합니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: f7d242410b5f7aadd74494bb33a7572afe23be54
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452334"
---
# <a name="aspnet-applications-using-wait-handles"></a>대기 핸들을 사용하는 ASP.NET 애플리케이션

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

비동기 작업을 처리 하는 콜백 및 폴링 모델은 응용 프로그램에서 한 번에 하나의 비동기 작업을 처리 하는 경우에 유용 합니다. 대기 모델은 여러 비동기 작업을 보다 유연 하 게 처리할 수 있는 방법을 제공 합니다. 대기 모델은 두 가지 대기 모델을 구현 하는 데 사용 되는 <xref:System.Threading.WaitHandle> 방법 (대기 (Any) 모델 및 Wait (All) 모델)이 있습니다.  
  
대기 모델을 사용 하려면 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 또는 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 메서드에서 반환 되는 <xref:System.IAsyncResult> 개체의 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 속성을 사용 해야 합니다. @No__t_0 및 <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드는 모두 배열에 함께 그룹화 된 인수로 <xref:System.Threading.WaitHandle> 개체를 전송 하도록 요구 합니다.  
  
두 대기 메서드는 모두 비동기 작업을 모니터링 하 여 완료를 대기 합니다. <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드는 작업이 완료되거나 시간이 초과되기를 기다립니다. 특정 작업이 완료되면 해당 결과를 처리한 다음 계속해서 다음 작업이 완료되거나 시간이 초과되기를 기다릴 수 있습니다. <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드는 <xref:System.Threading.WaitHandle> 인스턴스 배열의 모든 프로세스가 완료되거나 시간이 초과되기를 기다린 후 계속해서 프로세스를 진행합니다.  
  
대기 모델의 혜택은 다른 서버에서 특정 길이의 여러 작업을 실행 해야 하는 경우 또는 서버가 모든 쿼리를 동시에 처리할 수 있을 정도로 강력한 경우에 가장 적합 합니다. 여기에 나와 있는 예제에서 3 개의 쿼리는 다양 한 길이의 WAITFOR 명령을 중요 하지 않은 SELECT 쿼리에 추가 하 여 긴 프로세스를 에뮬레이트합니다.  
  
## <a name="example-wait-any-model"></a>예: Wait (Any) 모델  
다음 예에서는 Wait (Any) 모델을 보여 줍니다. 세 개의 비동기 프로세스를 시작 하면이 중 하나가 완료 될 때까지 대기 하기 위해 <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드가 호출 됩니다. 각 프로세스가 완료 되 면 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 메서드가 호출 되 고 결과 <xref:Microsoft.Data.SqlClient.SqlDataReader> 개체가 읽혀집니다. 이 시점에서 실제 응용 프로그램은 <xref:Microsoft.Data.SqlClient.SqlDataReader>를 사용 하 여 페이지의 일부를 채울 수 있습니다. 이 간단한 예제에서는 프로세스가 완료 된 시간이 프로세스에 해당 하는 텍스트 상자에 추가 됩니다. 이 경우 텍스트 상자의 시간은 프로세스가 완료 될 때마다 코드가 실행 되는 지점을 나타냅니다.  
  
이 예제를 설정 하려면 새 ASP.NET 웹 사이트 프로젝트를 만듭니다. 각 컨트롤에 대 한 기본 이름을 적용 하 여 페이지에 <xref:System.Web.UI.WebControls.Button> 컨트롤과 네 개의 <xref:System.Web.UI.WebControls.TextBox> 컨트롤을 추가 합니다.  
  
사용자 환경에 필요한 대로 연결 문자열을 수정 하 여 폼의 클래스에 다음 코드를 추가 합니다.  
  
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
  
## <a name="example-wait-all-model"></a>예: Wait (All) 모델  
다음 예제에서는 Wait (All) 모델을 보여 줍니다. 세 개의 비동기 프로세스를 시작 하면 <xref:System.Threading.WaitHandle.WaitAll%2A> 메서드가 호출 되어 프로세스가 완료 되거나 시간이 초과 될 때까지 대기 합니다.  
  
Wait (Any) 모델의 예제와 같이 프로세스가 완료 된 시간이 프로세스에 해당 하는 텍스트 상자에 추가 됩니다. 다시 텍스트 상자의 시간은 모든 프로세스가 완료 된 후에도 <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드 다음에 오는 코드가 실행 되는 시점을 보여 줍니다.  
  
이 예제를 설정 하려면 새 ASP.NET 웹 사이트 프로젝트를 만듭니다. 각 컨트롤에 대 한 기본 이름을 적용 하 여 페이지에 <xref:System.Web.UI.WebControls.Button> 컨트롤과 네 개의 <xref:System.Web.UI.WebControls.TextBox> 컨트롤을 추가 합니다.  
  
사용자 환경에 필요한 대로 연결 문자열을 수정 하 여 폼의 클래스에 다음 코드를 추가 합니다.  
  
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
