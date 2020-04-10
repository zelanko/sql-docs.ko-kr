---
title: SQL Server의 공급자 통계
description: SQL Server 런타임 통계를 가져오기 위한 지원을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 9a736eedf98d5e654f34423af8893cecda5a106f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925485"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server의 공급자 통계

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

.NET Framework 버전 2.0 및 .NET Core 버전 1.0부터 Microsoft SqlClient Data Provider for SQL Server가 런타임 통계를 지원합니다. 유효한 연결 개체를 만든 후 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection> 속성을 `True`로 설정하여 통계를 사용하도록 설정해야 합니다. 통계를 사용하도록 설정한 후에는 <xref:System.Collections.IDictionary> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 메서드를 통해 <xref:Microsoft.Data.SqlClient.SqlConnection> 참조를 검색하여 "특정 시점 스냅샷"으로 검토할 수 있습니다. 목록 전체를 이름/값 쌍 사전 항목 집합으로 열거합니다. 이러한 이름/값 쌍은 순서가 지정되지 않습니다. 언제든지 <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection> 메서드를 호출하여 카운터를 초기화할 수 있습니다. 통계 수집을 사용하도록 설정하지 않은 경우 예외가 생성되지 않습니다. 또한 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>를 먼저 호출하지 않고 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A>를 호출하는 경우 검색된 값은 각 항목의 초기 값입니다. 통계를 사용하도록 설정하고 잠시 동안 애플리케이션을 실행한 다음 통계를 사용하지 않도록 설정하면 검색된 값에 통계를 사용하지 않도록 설정한 지점까지 수집된 값이 반영됩니다. 모든 통계 값은 연결 단위로 수집됩니다.  
  
## <a name="statistical-values-available"></a>사용 가능한 통계 값  
현재 Microsoft SQL Server 공급자에서 사용할 수 있는 항목은 18개입니다. 사용 가능한 항목의 수는 **에서 반환한**  인터페이스 참조의 <xref:System.Collections.IDictionary>Count<xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 속성을 통해 액세스할 수 있습니다. 공급자 통계의 모든 카운터는 64비트 수준의 공용 언어 런타임 <xref:System.Int64> 형식(C#과 Visual Basic의 **long**)을 사용합니다. **int64.MaxValue** 필드에서 정의한 **int64** 데이터 형식의 최댓값은 ((2^63)-1))입니다. 카운터 값이 최댓값에 도달하면 더 이상 정확한 것으로 간주하지 않아야 합니다. 즉, **int64.MaxValue**-1((2^63)-2)는 사실상 모든 통계의 최대 유효 값입니다.  
  
> [!NOTE]
>  반환된 통계의 번호, 이름 및 순서가 나중에 변경될 수 있으므로 사전을 사용하여 공급자 통계를 반환합니다. 애플리케이션이 사전에 있는 특정 값을 사용하면 안 되며, 값이 있는지 여부를 확인하고 적절하게 분기해야 합니다.  
  
다음 표에서는 현재 사용 가능한 통계 값에 대해 설명합니다. 개별 값의 키 이름은 Microsoft .NET Framework 및 .NET Core의 국가별 버전에서 지역화되지 않습니다.  
  
|키 이름|Description|  
|--------------|-----------------|  
|`BuffersReceived`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 공급자가 SQL Server에서 받은 TDS(Tabular Data Stream) 패킷의 수를 반환합니다.|  
|`BuffersSent`|통계를 사용하도록 설정한 후 공급자가 SQL Server에 보낸 TDS 패킷 수를 반환합니다. 긴 명령에는 여러 버퍼가 필요할 수 있습니다. 예를 들어 서버에 긴 명령이 전송되고 6개의 패킷이 필요한 경우 `ServerRoundtrips`가 1씩 증가하고 `BuffersSent`가 6씩 증가합니다.|  
|`BytesReceived`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 공급자가 SQL Server에서 받은 TDS 패킷의 데이터 바이트 수를 반환합니다.|  
|`BytesSent`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 SQL Server로 보낸 TDS 패킷의 데이터 바이트 수를 반환합니다.|  
|`ConnectionTime`|통계가 활성화된 후 연결이 열려 있던 시간(밀리초 단위)입니다(연결을 열기 전에 통계를 활성화한 경우에는 총 연결 시간).|  
|`CursorOpens`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 커서를 연 횟수를 반환합니다.<br /><br /> SELECT 문이 반환하는 읽기 전용/전달 전용 결과는 커서로 간주되지 않으므로 이 카운터에 영향을 주지 않습니다.|  
|`ExecutionTime`|통계가 활성화된 후 서버의 응답을 기다린 시간과 공급자 자체에서 코드를 실행하는 데 걸린 시간을 포함하여 공급자에서 처리에 소요된 누적 시간(밀리초 단위)을 반환합니다.<br /><br /> 타이밍 코드를 포함하는 클래스는 다음과 같습니다.<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> 성능이 중요한 멤버를 가능한 한 작게 유지하기 위해 다음 멤버는 시간이 제한되지 않습니다.<br /><br /> SqlDataReader<br /><br /> this[] 연산자(모두 오버로드)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 실행된 INSERT, DELETE 및 UPDATE 문의 총 수를 반환합니다.|  
|`IduRows`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 실행된 INSERT, DELETE 및 UPDATE 문의 영향을 받은 행의 총 수를 반환합니다.|  
|`NetworkServerTime`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 공급자에서 서버의 응답을 기다리는 데 소요된 누적 시간(밀리초 단위)의 양을 반환합니다.|  
|`PreparedExecs`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 실행된 준비된 명령의 수를 반환합니다.|  
|`Prepares`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 준비된 문의 수를 반환합니다.|  
|`SelectCount`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 실행된 SELECT 문의 수를 반환합니다. 여기에는 커서에서 행을 검색하는 FETCH 문이 포함되며 <xref:Microsoft.Data.SqlClient.SqlDataReader>의 끝에 도달하면 SELECT 문 수가 업데이트됩니다.|  
|`SelectRows`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후에 선택된 행 수를 반환합니다. 이 카운터는 호출자가 실제로 사용하지 않은 행을 포함하여 SQL 문에서 생성된 모든 행을 반영합니다. 예를 들어 전체 결과 집합을 읽기 전에 데이터 판독기를 닫으면 개수에 영향을 주지 않습니다. 여기에는 FETCH 문을 통해 커서에서 검색된 행이 포함됩니다.|  
|`ServerRoundtrips`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결이 서버에 명령을 보내고 응답을 받은 횟수를 반환합니다.|  
|`SumResultSets`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 사용된 결과 집합의 수를 반환합니다. 예를 들어 클라이언트에 반환되는 모든 결과 집합이 여기에 포함됩니다. 커서의 경우 각 페치 또는 블록 페치 작업은 독립적인 결과 집합으로 간주됩니다.|  
|`Transactions`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 시작된 사용자 트랜잭션의 수를 반환합니다. 자동 커밋을 사용하여 연결을 실행하는 경우 각 명령은 트랜잭션으로 간주됩니다.<br /><br /> 이 카운터는 나중에 트랜잭션이 커밋되거나 롤백되는지 여부에 관계없이 BEGIN TRAN 문이 실행되는 즉시 트랜잭션 수를 증가시킵니다.|  
|`UnpreparedExecs`|애플리케이션에서 공급자 사용을 시작하고 통계를 사용하도록 설정한 후 연결을 통해 실행된 준비되지 않은 문의 수를 반환합니다.|  
  
### <a name="retrieving-a-value"></a>값 검색  
다음 콘솔 애플리케이션에서는 연결에서 통계를 사용하도록 설정하고, 4개의 개별 통계 값을 검색하고, 콘솔 창에 기록하는 방법을 보여 줍니다.  
  
> [!NOTE]
>  다음 예제에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 샘플 코드에 제공된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치되어 있고 사용 가능한 것으로 가정합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정합니다.  
  
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
다음 콘솔 애플리케이션에서는 연결에서 통계를 사용하도록 설정하고, 열거자를 사용하여 사용 가능한 모든 통계 값을 검색하고, 콘솔 창에 쓰는 방법을 보여 줍니다.  
  
> [!NOTE]
>  다음 예제에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 샘플 코드에 제공된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치되어 있고 사용 가능한 것으로 가정합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정합니다.  
  
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
