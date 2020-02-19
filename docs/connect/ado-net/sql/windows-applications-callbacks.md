---
title: 콜백을 사용하는 Windows 애플리케이션
description: 비동기 명령을 안전하게 실행하는 방법을 보여 주는 예제를 제공합니다. 이 예제에서는 별도의 스레드에서 양식과 해당 내용을 사용하여 상호 작용을 올바르게 처리합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ae2ea457-0764-4b06-8977-713c77e85bd2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 83dca011087150eef5d8fdc948bb65cc6808830e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253377"
---
# <a name="windows-applications-using-callbacks"></a>콜백을 사용하는 Windows 애플리케이션

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

대부분의 비동기 처리 시나리오에서는 데이터베이스 작업을 시작하고 데이터베이스 작업이 완료될 때까지 기다리지 않고 다른 프로세스를 계속 실행하려고 합니다. 그러나 많은 시나리오에서는 데이터베이스 작업이 종료된 후 다른 작업을 수행해야 합니다. 예를 들어 Windows 애플리케이션에서 장기 실행 작업을 백그라운드 스레드에 위임하는 동시에 사용자 인터페이스 스레드가 응답성을 유지하기를 원합니다. 그러나 데이터베이스 작업이 완료되면 결과를 사용하여 양식을 채워야 합니다. 이 시나리오 유형은 콜백을 사용하여 구현하는 것이 가장 좋습니다.  
  
<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 또는 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 메서드에서 <xref:System.AsyncCallback> 대리자를 지정하여 콜백을 정의합니다. 작업이 완료되면 대리자가 호출됩니다. <xref:Microsoft.Data.SqlClient.SqlCommand> 자체에 대한 참조를 대리자에게 전달할 수 있습니다. 그러면 대리자가 쉽게 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체에 액세스하고 전역 변수를 사용하지 않고 적절한 `End` 메서드를 호출할 수 있습니다.  
  
## <a name="example"></a>예제  
다음 Windows 애플리케이션에서는 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A> 메서드를 사용하여 몇 초의 지연이 포함된 Transact-SQL 문을 실행하는 방법을 보여 줍니다(장기 실행 명령을 에뮬레이션).  
  
이 예제에서는 별도의 스레드에서 양식과 상호 작용하는 메서드를 호출하는 등의 여러 가지 중요한 기술을 보여 줍니다. 또한 이 예제에서는 사용자가 여러 명령을 동시에 실행하는 것을 차단하는 방법과 콜백 프로시저를 호출하기 전에 양식이 닫히지 않도록 하는 방법을 보여 줍니다.  
  
이 예제를 설정하려면 새 Windows 애플리케이션을 만듭니다. 각 컨트롤에 대해 기본 이름을 적용하여 양식에 <xref:System.Windows.Forms.Button> 컨트롤과 2개의 <xref:System.Windows.Forms.Label> 컨트롤을 배치합니다. 사용자의 환경에 필요한 대로 연결 문자열을 수정하여 양식의 클래스에 다음 코드를 추가합니다.  
  
```csharp  
// Add these to the top of the class, if they're not already there:  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
// Hook up the form's Load event handler (you can double-click on   
// the form's design surface in Visual Studio), and then add   
// this code to the form's class:  
  
// You'll need this delegate in order to display text from a thread  
// other than the form's thread. See the HandleCallback  
// procedure for more information.  
// This same delegate matches both the DisplayStatus   
// and DisplayResults methods.  
private delegate void DisplayInfoDelegate(string Text);  
  
// This flag ensures that the user doesn't attempt  
// to restart the command or close the form while the   
// asynchronous command is executing.  
private bool isExecuting;  
  
// This example maintains the connection object   
// externally, so that it's available for closing.  
private SqlConnection connection;  
  
private static string GetConnectionString()  
{  
    // To avoid storing the connection string in your code,              
    // you can retrieve it from a configuration file.   
  
    // If you have not included "Asynchronous Processing=true" in the  
    // connection string, the command will not be able  
    // to execute asynchronously.  
    return "Data Source=(local);Integrated Security=SSPI;" +  
    "Initial Catalog=AdventureWorks; Asynchronous Processing=true";  
}  
  
private void DisplayStatus(string Text)  
{  
    this.label1.Text = Text;  
}  
  
private void DisplayResults(string Text)  
{  
    this.label1.Text = Text;  
    DisplayStatus("Ready");  
}  
  
private void Form1_FormClosing(object sender, System.Windows.Forms.FormClosingEventArgs e)  
{  
    if (isExecuting)  
    {  
        MessageBox.Show(this, "Can't close the form until " +  
        "the pending asynchronous command has completed. Please " +  
        "wait...");
        e.Cancel = true;  
    }  
}  
  
private void button1_Click(object sender, System.EventArgs e)  
{  
    if (isExecuting)  
    {  
        MessageBox.Show(this, "Already executing. Please wait until " +  
        "the current query has completed.");  
    }  
    else  
    {  
        SqlCommand command = null;  
        try  
        {  
            DisplayResults("");  
            DisplayStatus("Connecting...");  
            connection = new SqlConnection(GetConnectionString());  
            // To emulate a long-running query, wait for   
            // a few seconds before working with the data.  
            // This command doesn't do much, but that's the point--  
            // it doesn't change your data, in the long run.  
            string commandText =  
                "WAITFOR DELAY '0:0:05';" +  
                "UPDATE Production.Product " +  
                "SET ReorderPoint = ReorderPoint + 1 " +  
                "WHERE ReorderPoint Is Not Null;" +  
                "UPDATE Production.Product " +  
                "SET ReorderPoint = ReorderPoint - 1 " +  
                "WHERE ReorderPoint Is Not Null";  
  
            command = new SqlCommand(commandText, connection);  
            connection.Open();  
  
            DisplayStatus("Executing...");  
            isExecuting = true;  
            // Although it's not required that you pass the   
            // SqlCommand object as the second parameter in the   
            // BeginExecuteNonQuery call, doing so makes it easier  
            // to call EndExecuteNonQuery in the callback procedure.  
            AsyncCallback callback = new AsyncCallback(HandleCallback);  
  
            // Once the BeginExecuteNonQuery method is called,  
            // the code continues--and the user can interact with  
            // the form--while the server executes the query.  
            command.BeginExecuteNonQuery(callback, command);  
  
        }  
        catch (Exception ex)  
        {  
            isExecuting = false;  
            DisplayStatus($"Ready (last error: {ex.Message})");
            if (connection != null)  
            {  
                connection.Close();  
            }  
        }  
    }  
}  
  
private void HandleCallback(IAsyncResult result)  
{  
    try  
    {  
        // Retrieve the original command object, passed  
        // to this procedure in the AsyncState property  
        // of the IAsyncResult parameter.  
        SqlCommand command = (SqlCommand)result.AsyncState;  
        int rowCount = command.EndExecuteNonQuery(result);  
        string rowText = " rows affected.";  
        if (rowCount == 1)  
        {  
            rowText = " row affected.";  
        }  
        rowText = rowCount + rowText;  
  
        // You may not interact with the form and its contents  
        // from a different thread, and this callback procedure  
        // is all but guaranteed to be running from a different thread  
        // than the form. Therefore you cannot simply call code that   
        // displays the results, like this:  
        // DisplayResults(rowText)  
  
        // Instead, you must call the procedure from the form's thread.  
        // One simple way to accomplish this is to call the Invoke  
        // method of the form, which calls the delegate you supply  
        // from the form's thread.   
        DisplayInfoDelegate del =   
         new DisplayInfoDelegate(DisplayResults);  
        this.Invoke(del, rowText);  
    }  
    catch (Exception ex)  
    {  
        // Because you're now running code in a separate thread,   
        // if you don't handle the exception here, none of your other  
        // code will catch the exception. Because none of your  
        // code is on the call stack in this thread, there's nothing  
        // higher up the stack to catch the exception if you don't   
        // handle it here. You can either log the exception or   
        // invoke a delegate (as in the non-error case in this   
        // example) to display the error on the form. In no case  
        // can you simply display the error without executing a   
        // delegate as in the try block here.   
  
        // You can create the delegate instance as you   
        // invoke it, like this:  
        this.Invoke(new DisplayInfoDelegate(DisplayStatus),  
            $"Ready (last error: {ex.Message}");
    }  
    finally  
    {  
        isExecuting = false;  
        if (connection != null)  
        {  
            connection.Close();  
        }  
    }  
}  
  
private void Form1_Load(object sender, System.EventArgs e)  
{  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    this.FormClosing += new System.Windows.Forms.  
        FormClosingEventHandler(this.Form1_FormClosing);  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [비동기 작업](asynchronous-operations.md)
