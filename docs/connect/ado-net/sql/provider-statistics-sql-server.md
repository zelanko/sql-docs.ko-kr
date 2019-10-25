---
title: SQL Server의 공급자 통계
description: SQL Server 런타임 통계 가져오기에 대 한 지원을 설명 합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 092cf63e62bce01e2a771ce4e5f7f46e1073e91a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452068"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server의 공급자 통계

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

.NET Framework 버전 2.0 및 .NET Core 버전 1.0부터 SQL Server 용 Microsoft SqlClient Data Provider는 런타임 통계를 지원 합니다. 유효한 연결 개체를 만든 후에 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 속성을 `True`로 설정 하 여 통계를 사용 하도록 설정 해야 합니다. 통계를 활성화 한 후에는 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 메서드를 통해 <xref:System.Collections.IDictionary> 참조를 검색 하 여 "시간 내 스냅숏"으로 검토할 수 있습니다. 목록 전체를 이름/값 쌍 사전 항목 집합으로 열거 합니다. 이러한 이름/값 쌍은 순서가 지정 되지 않습니다. 언제 든 지 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> 메서드를 호출 하 여 카운터를 다시 설정할 수 있습니다. 통계 수집이 사용 하도록 설정 되지 않은 경우 예외가 생성 되지 않습니다. 또한 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A>를 먼저 호출 하지 않고 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>를 호출 하는 경우 검색 된 값은 각 항목의 초기 값입니다. 통계를 사용 하도록 설정 하 고 잠시 동안 응용 프로그램을 실행 한 다음 통계를 사용 하지 않도록 설정 하면 검색 된 값에 통계가 사용 하지 않도록 설정 된 지점까지 수집 된 값이 반영 됩니다. 수집 된 모든 통계 값은 연결 단위로 설정 됩니다.  
  
## <a name="statistical-values-available"></a>통계 값 사용 가능  
현재 Microsoft SQL Server 공급자에서 사용할 수 있는 18 개의 다른 항목이 있습니다. 사용 가능한 항목의 수는 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>에서 반환한 <xref:System.Collections.IDictionary> 인터페이스 참조의 **Count** 속성을 통해 액세스할 수 있습니다. 공급자 통계의 모든 카운터는 64비트 수준의 공용 언어 런타임 <xref:System.Int64> 형식(C#과 Visual Basic의 **long**)을 사용합니다. **int64.MaxValue** 필드에서 정의한 **int64** 데이터 형식의 최댓값은 ((2^63)-1))입니다. 카운터의 값이 최대값에 도달 하면 더 이상 정확 하 게 고려 되지 않아야 합니다. 즉, **int64.MaxValue**-1((2^63)-2)는 사실상 모든 통계의 최대 유효 값입니다.  
  
> [!NOTE]
>  반환 된 통계의 번호, 이름 및 순서가 나중에 변경 될 수 있으므로 사전을 사용 하 여 공급자 통계를 반환 합니다. 응용 프로그램은 사전에 있는 특정 값을 사용 하면 안 됩니다. 대신 값이 있는지 여부를 확인 하 고 적절 하 게 분기 해야 합니다.  
  
다음 표에서는 현재 사용 가능한 통계 값에 대해 설명 합니다. 개별 값의 키 이름은 Microsoft .NET Framework 및 .NET Core의 국가별 버전에서 지역화 되지 않습니다.  
  
|키 이름|설명|  
|--------------|-----------------|  
|`BuffersReceived`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 공급자가 SQL Server에서 받은 TDS (tabular data stream) 패킷의 수를 반환 합니다.|  
|`BuffersSent`|통계를 사용 하도록 설정한 후 공급자가 SQL Server에 보낸 TDS 패킷 수를 반환 합니다. 긴 명령에는 여러 버퍼가 필요할 수 있습니다. 예를 들어 서버에 대량 명령이 전송 되 고 6 개의 패킷이 필요한 경우 `ServerRoundtrips` 1 씩 증가 하 고 `BuffersSent` 6 씩 증가 합니다.|  
|`BytesReceived`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 공급자가 SQL Server에서 받은 TDS 패킷의 데이터 바이트 수를 반환 합니다.|  
|`BytesSent`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 TDS 패킷에서 SQL Server 전송 된 데이터의 바이트 수를 반환 합니다.|  
|`ConnectionTime`|통계가 활성화된 후 연결이 열려 있던 시간(밀리초 단위)입니다(연결을 열기 전에 통계를 활성화한 경우에는 총 연결 시간).|  
|`CursorOpens`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 커서를 연 횟수를 반환 합니다.<br /><br /> SELECT 문에 의해 반환 되는 읽기 전용/전달 전용 결과는 커서로 간주 되지 않으므로이 카운터에 영향을 주지 않습니다.|  
|`ExecutionTime`|통계가 활성화된 후 서버의 응답을 기다린 시간과 공급자 자체에서 코드를 실행하는 데 걸린 시간을 포함하여 공급자에서 처리에 소요된 누적 시간(밀리초 단위)을 반환합니다.<br /><br /> 타이밍 코드를 포함 하는 클래스는 다음과 같습니다.<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> 성능이 중요 한 멤버를 가능한 한 작게 유지 하려면 다음 멤버를 시간 제한 하지 않습니다.<br /><br /> SqlDataReader<br /><br /> 이 [] 연산자 (모든 오버 로드)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 실행 된 INSERT, DELETE 및 UPDATE 문의 총 수를 반환 합니다.|  
|`IduRows`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 실행 되는 INSERT, DELETE 및 UPDATE 문의 영향을 받는 총 행 수를 반환 합니다.|  
|`NetworkServerTime`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 공급자에서 서버의 응답을 기다리는 데 소요된 누적 시간(밀리초 단위)의 양을 반환합니다.|  
|`PreparedExecs`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 실행 된 준비 된 명령의 수를 반환 합니다.|  
|`Prepares`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 준비 된 문의 수를 반환 합니다.|  
|`SelectCount`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 실행 된 SELECT 문의 수를 반환 합니다. 여기에는 커서에서 행을 검색 하는 FETCH 문이 포함 되며 <xref:Microsoft.Data.SqlClient.SqlDataReader> 끝에 도달 하면 SELECT 문의 수가 업데이트 됩니다.|  
|`SelectRows`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후에 선택 된 행 수를 반환 합니다. 이 카운터는 호출자가 실제로 사용 하지 않은 행을 포함 하 여 SQL 문에서 생성 된 모든 행을 반영 합니다. 예를 들어 전체 결과 집합을 읽기 전에 데이터 판독기를 닫으면 개수에 영향을 주지 않습니다. 여기에는 FETCH 문을 통해 커서에서 검색 된 행이 포함 됩니다.|  
|`ServerRoundtrips`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결이 서버에 명령을 보내고 응답을 받은 횟수를 반환 합니다.|  
|`SumResultSets`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 사용 된 결과 집합의 수를 반환 합니다. 예를 들어 여기에는 클라이언트에 반환 되는 모든 결과 집합이 포함 됩니다. 커서의 경우 각 인출 또는 블록 페치 작업은 독립적인 결과 집합으로 간주 됩니다.|  
|`Transactions`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 시작 된 사용자 트랜잭션 수를 반환 합니다. 에서 자동 커밋을 사용 하 여 연결을 실행 하는 경우 각 명령은 트랜잭션으로 간주 됩니다.<br /><br /> 이 카운터는 나중에 트랜잭션이 커밋되거나 롤백되는 지 여부에 관계 없이 BEGIN TRAN 문이 실행 되는 즉시 트랜잭션 수를 증가 시킵니다.|  
|`UnpreparedExecs`|응용 프로그램에서 공급자 사용을 시작 하 고 통계를 활성화 한 후 연결을 통해 실행 준비 되지 않은 문 수를 반환 합니다.|  
  
### <a name="retrieving-a-value"></a>값 검색  
다음 콘솔 응용 프로그램에서는 연결에서 통계를 사용 하도록 설정 하 고, 4 개의 개별 통계 값을 검색 하 고, 콘솔 창에 기록 하는 방법을 보여 줍니다.  
  
> [!NOTE]
>  다음 예제에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 샘플 코드에 제공 된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치 되어 있고 사용 가능한 것으로 가정 합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정 합니다.  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>모든 값 검색  
다음 콘솔 응용 프로그램에서는 연결에서 통계를 사용 하도록 설정 하 고, 열거자를 사용 하 여 사용 가능한 모든 통계 값을 검색 하 고, 콘솔 창에 쓰는 방법을 보여 줍니다.  
  
> [!NOTE]
>  다음 예제에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 샘플 코드에 제공 된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치 되어 있고 사용 가능한 것으로 가정 합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정 합니다.  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
