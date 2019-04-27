---
title: 로컬 패키지의 출력 로드 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 57b318ac8062203bd11a0717a4c8077bca9880d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766953"
---
# <a name="loading-the-output-of-a-local-package"></a>로컬 패키지의 출력 로드
  [!INCLUDE[vstecado](../../includes/vstecado-md.md)]을 사용하여 출력을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상에 저장한 경우 또는 **System.IO** 네임스페이스의 클래스를 사용하여 출력을 플랫 파일 대상에 저장한 경우 클라이언트 애플리케이션에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 출력을 읽을 수 있습니다. 하지만 데이터를 지속하기 위한 중간 단계 없이 클라이언트 응용 프로그램이 메모리에서 직접 패키지의 출력을 읽을 수도 있습니다. 이 솔루션의 핵심은는 `Microsoft.SqlServer.Dts.DtsClient` 의 특수화 된 구현을 포함 하는 네임 스페이스를 `IDbConnection`를 `IDbCommand`, 및 **IDbDataParameter** 에서 인터페이스를 **System.Data** 네임 스페이스입니다. Microsoft.SqlServer.Dts.DtsClient.dll 어셈블리는 기본적으로 **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**에 설치됩니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 절차를 수행하려면 데이터 흐름 태스크와 부모 개체의 DelayValidation 속성이 기본값인 **False**로 설정되어 있어야 합니다.  
  
## <a name="description"></a>Description  
 이 절차에서는 DataReader 대상을 사용하는 패키지의 출력을 메모리에서 직접 로드하는 클라이언트 응용 프로그램을 관리 코드로 개발하는 방법을 보여 줍니다. 여기에 요약된 단계는 뒷부분의 코드 예제에서 자세히 보여 줍니다.  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>데이터 패키지 출력을 클라이언트 응용 프로그램으로 로드하려면  
  
1.  패키지에서 DataReader 대상이 클라이언트 응용 프로그램으로 읽어 올 출력을 받도록 구성합니다. DataReader 대상 이름은 나중에 클라이언트 응용 프로그램에서 사용되므로 이 대상에 알기 쉬운 이름을 지정합니다. 또한 DataReader 대상의 이름을 적어 두어야 합니다.  
  
2.  개발 프로젝트 대 한 참조를 설정 합니다 `Microsoft.SqlServer.Dts.DtsClient` 어셈블리를 찾아 네임 스페이스 **Microsoft.SqlServer.Dts.DtsClient.dll**합니다. 기본적으로 이 어셈블리는 **C:\Program Files\Microsoft SQL Server\100\DTS\Binn**에 설치됩니다. C#을 사용 하 여 네임 스페이스를 코드로 가져옵니다 `Using` 또는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] `Imports` 문입니다.  
  
3.  코드에서 형식의 개체를 만듭니다 `DtsClient.DtsConnection` 에 필요한 명령줄 매개 변수를 포함 하는 연결 문자열을 사용 하 여 **dtexec.exe** 패키지를 실행 합니다. 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md)를 참조하세요. 그런 다음 이 연결 문자열을 사용하여 연결을 엽니다. **dtexecui** 유틸리티를 사용하여 필요한 연결 문자열을 시각적으로 만들 수도 있습니다.  
  
    > [!NOTE]  
    >  예제 코드에서는 `/FILE <path and filename>` 구문을 사용하여 파일 시스템에서 패키지를 로드하는 방법을 보여 줍니다. 그러나 `/SQL <package name>` 구문을 사용하여 MSDB 데이터베이스에서 패키지를 로드하거나 `/DTS \<folder name>\<package name>` 구문을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 저장소에서 패키지를 로드할 수도 있습니다.  
  
4.  이전에 만든 `DtsClient.DtsCommand`을 사용하는 `DtsConnection` 형식의 개체를 만들고 이 개체의 `CommandText` 속성을 패키지의 DataReader 대상 이름으로 설정합니다. 그런 다음 이 명령 개체의 `ExecuteReader` 메서드를 호출하여 패키지 결과를 새 DataReader로 로드합니다.  
  
5.  필요할 경우 `DtsDataParameter` 개체에서 `DtsCommand` 개체의 컬렉션을 사용하여 패키지의 출력을 간접적으로 매개 변수화함으로써 패키지에 정의된 변수에 값을 전달할 수 있습니다. 패키지 내에서는 이러한 변수를 쿼리 매개 변수로 사용하거나 식에 사용하여 DataReader 대상에 반환되는 결과에 영향을 줄 수 있습니다. 패키지에 이러한 변수를 정의 해야 합니다는 **DtsClient** 네임 스페이스를 사용 하 여 사용 하기 전에 `DtsDataParameter` 클라이언트 응용 프로그램에서 개체입니다. **변수** 창에서 **변수 열 선택** 도구 모음 단추를 클릭하여 **네임스페이스** 열을 표시해야 할 수도 있습니다. 클라이언트 코드를 추가 하면를 `DtsDataParameter` 에 `Parameters` 컬렉션은 `DtsCommand`, 변수 이름에서 DtsClient 네임 스페이스 참조를 생략 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  DataReader의 `Read` 메서드를 필요한 만큼 반복적으로 호출하여 출력 데이터 행을 반복합니다. 클라이언트 응용 프로그램에서 이 데이터를 사용하거나 나중에 사용할 수 있도록 저장합니다.  
  
    > [!IMPORTANT]  
    >  이 DataReader 구현의 `Read` 메서드는 마지막 데이터 행을 읽은 후 `true`를 한 번 더 반환합니다. 따라서 `Read`가 `true`를 반환하는 동안 DataReader를 반복하는 일반적인 코드를 사용하기가 어렵습니다. 예상한 개수의 행을 읽은 후 코드에서 `Read` 메서드를 마지막으로 한 번 더 호출하지 않고 DataReader나 연결을 닫으려고 하면 처리되지 않은 예외가 발생합니다. 그러나 `Read`가 여전히 `true`를 반환하지만 마지막 행이 전달된 경우에 코드에서 이 마지막 루프 반복의 데이터를 읽으려고 하면 "SIS IDataReader가 결과 집합의 끝을 지났습니다."라는 메시지와 함께 처리되지 않은 `ApplicationException`이 발생합니다. 이 동작은 다른 DataReader 구현의 동작과는 다릅니다. 따라서 `Read`가 `true`를 반환하는 동안 DataReader에서 루프를 사용하여 행을 읽으려면 `ApplicationException` 메서드를 마지막으로 성공적으로 호출할 때 예상된 이 `Read`을 catch, 테스트 및 삭제하는 코드를 작성해야 합니다. 예상 행 수를 이미 아는 경우에는 행을 처리한 다음 DataReader와 연결을 닫기 전에 `Read` 메서드를 한 번 이상 호출할 수 있습니다.  
  
7.  `Dispose` 개체의 `DtsCommand` 메서드를 호출합니다. 이 메서드는 `DtsDataParameter` 개체를 사용한 경우에 특히 중요합니다.  
  
8.  DataReader와 연결 개체를 닫습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 단일 집계 값을 계산하고 해당 값을 DataReader 대상에 저장하는 패키지를 실행한 다음 DataReader에서 이 값을 읽어 Windows Form의 입력란에 표시합니다.  
  
 패키지의 출력을 클라이언트 응용 프로그램으로 로드할 때는 매개 변수를 사용할 필요가 없습니다. 매개 변수를 사용 하지 않을 경우에 변수를 사용 하 여를 생략할 수 있습니다 합니다 **DtsClient** 네임 스페이스를 사용 하는 코드를 생략 하 고는 `DtsDataParameter` 개체입니다.  
  
#### <a name="to-create-the-test-package"></a>테스트 패키지를 만들려면  
  
1.  새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만듭니다. 예제 코드에서는 패키지 이름으로 "DtsClientWParamPkg.dtsx"를 사용합니다.  
  
2.  DtsClient 네임스페이스에 String 형식의 변수를 추가합니다. 예제 코드에서는 변수 이름으로 Country를 사용합니다. **변수** 창에서 **변수 열 선택** 도구 모음 단추를 클릭하여 **네임스페이스** 열을 표시해야 할 수도 있습니다.  
  
3.  [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 연결하는 OLE DB 연결 관리자를 추가합니다.  
  
4.  패키지에 데이터 흐름 태스크를 추가하고 데이터 흐름 디자인 화면으로 전환합니다.  
  
5.  데이터 흐름에 OLE DB 원본을 추가하고, 이 데이터 원본에서 이전에 만든 OLE DB 연결 관리자와 다음 SQL 명령을 사용하도록 구성합니다.  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  클릭 `Parameters` 고 합니다 **쿼리 매개 변수 설정** 대화 상자 단일 입력된 매개 변수인 parameter0을, DtsClient::Country 변수에 합니다.  
  
7.  데이터 흐름에 집계 변환을 추가하고 OLE DB 원본의 출력을 변환에 연결합니다. 집계 변환 편집기를 열고 이 변환에서 모든 입력 열(*)에 대해 "Count all" 연산을 수행하고 집계된 값을 CustomerCount라는 별칭으로 출력하도록 구성합니다.  
  
8.  데이터 흐름에 DataReader 대상을 추가하고 집계 변환의 출력을 DataReader 대상에 연결합니다. 예제 코드에서는 DataReader 이름으로 "DataReaderDest"를 사용합니다. 대상에 대해 사용 가능한 단일 입력 열인 CustomerCount를 선택합니다.  
  
9. 패키지를 저장합니다. 다음에 만들 테스트 응용 프로그램에서는 이 패키지를 실행하고 메모리에서 직접 출력을 검색합니다.  
  
#### <a name="to-create-the-test-application"></a>테스트 응용 프로그램을 만들려면  
  
1.  새 Windows Forms 응용 프로그램을 만듭니다.  
  
2.  에 대 한 참조를 추가 합니다 `Microsoft.SqlServer.Dts.DtsClient` 네임 스페이스에 있는 동일한 이름의 어셈블리를 찾아 **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**합니다.  
  
3.  다음 예제 코드를 복사하여 폼의 코드 모듈에 붙여 넣습니다.  
  
4.  값을 수정 합니다 `dtexecArgs` 필요에 따라 변수를 포함 하 여 필요한 명령줄 매개 변수 **dtexec.exe** 패키지를 실행 하려면. 예제 코드는 파일 시스템에서 패키지를 로드합니다.  
  
5.  값을 수정 합니다 `dataReaderName` 필요에 따라 변수를 포함 된 패키지의 DataReader 대상의 이름입니다.  
  
6.  폼에 단추와 입력란을 추가합니다. 샘플 코드를 사용 하 여 `btnRun` 단추의 이름으로 및 `txtResults` 입력란의 이름으로 합니다.  
  
7.  응용 프로그램을 실행하고 단추를 클릭합니다. 그러면 패키지가 실행되는 동안 잠깐 일시 중지된 후 패키지에서 계산한 집계 값, 즉 캐나다의 고객 수가 폼의 입력란에 표시됩니다.  
  
### <a name="sample-code"></a>예제 코드  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [로컬 실행과 원격 실행의 차이점 이해](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [프로그래밍 방식으로 원격 패키지 로드 및 실행](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  
