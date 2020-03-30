---
title: SQL Server의 인스턴스 열거(ADO.NET)
description: SQL Server의 활성 인스턴스를 열거하는 방법을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bd0dbbedcb2fa33af80e0a1a1d593bf7df27edb6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896953"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>SQL Server의 인스턴스 열거(ADO.NET)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server에서 애플리케이션이 현재 네트워크 내에서 SQL Server 인스턴스를 찾을 수 있습니다. <xref:System.Data.Sql.SqlDataSourceEnumerator> 클래스는 표시되는 모든 서버에 대한 정보가 포함된 <xref:System.Data.DataTable>을 제공하여 애플리케이션 개발자에게 이 정보를 노출합니다. 이 반환된 테이블은 사용자가 새 연결을 만들려고 할 때 제공되는 목록과 일치하는 네트워크상에서 사용 가능한 서버 인스턴스의 목록을 포함하며, **Connection Properties** 대화 상자에서 사용 가능한 모든 서버가 포함된 드롭다운 목록을 확장합니다. 표시되는 결과가 항상 완전하지는 않습니다.  
  
> [!NOTE]
>  대부분의 Windows 서비스와 마찬가지로 최소 권한으로 SQL Browser 서비스를 실행하는 것이 가장 좋습니다. SQL Browser 서비스와 이 서비스의 동작을 관리하는 방법에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하세요.  
  
## <a name="retrieving-an-enumerator-instance"></a>열거자 인스턴스 검색  
사용 가능한 SQL Server 인스턴스에 대한 정보가 포함된 테이블을 검색하려면 먼저 공유/정적 <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> 속성을 사용하여 열거자를 검색해야 합니다.  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
정적 인스턴스를 검색한 후에는 사용 가능한 서버에 대한 정보가 포함된 <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A>을 반환하는 <xref:System.Data.DataTable> 메서드를 호출할 수 있습니다.  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
메서드 호출에서 반환된 테이블에는 다음 열이 포함되어 있으며, 모든 열은 `string` 값을 포함합니다.  
  
|열|Description|  
|------------|-----------------|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|서버의 이름입니다.|  
|**InstanceName**|서버 인스턴스의 이름입니다. 서버를 기본 인스턴스로 실행하는 경우에는 비어있습니다.|  
|**IsClustered**|서버가 클러스터의 일부인지 여부를 나타냅니다.|  
|**버전**|서버 버전입니다. 다음은 그 예입니다.<br /><br /> -   9.00.x (SQL Server 2005)<br />-   10.0.xx (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-   11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>열거형 제한 사항  
사용 가능한 서버가 모두 나열될 수도 있고 그렇지 않을 수도 있습니다. 이 목록은 제한 시간, 네트워크 트래픽과 같은 요인에 따라 달라질 수 있습니다. 이로 인해 두 번의 연속 호출에서 목록이 다를 수 있습니다. 동일한 네트워크에 있는 서버만 나열됩니다. 브로드캐스트 패킷은 일반적으로 라우터를 트래버스하지 않습니다. 즉, 나열된 서버가 표시되지 않을 수 있지만 호출에서 안정적으로 작동합니다.  
  
나열된 서버에는 `IsClustered` 및 버전과 같은 추가 정보가 있을 수도 있고 없을 수도 있습니다. 이는 목록을 가져온 방법에 따라 달라집니다. SQL Server 브라우저 서비스를 통해 나열된 서버에서는 Windows 인프라를 통해 찾은 정보(이름만 나열됨)보다 더 자세한 정보를 제공합니다.  
  
> [!NOTE]
>  서버 열거는 완전 신뢰로 실행되는 경우에만 사용할 수 있습니다. 부분적으로 신뢰할 수 있는 환경에서 실행되는 어셈블리는 <xref:Microsoft.Data.SqlClient.SqlClientPermission> CAS(코드 액세스 보안) 권한이 있는 경우에도 이를 사용할 수 없습니다.  
  
SQL Server에서는 SQL Browser라고 하는 외부 Windows 서비스를 사용하여 <xref:System.Data.Sql.SqlDataSourceEnumerator>에 대한 정보를 제공합니다. 이 서비스는 기본적으로 사용하도록 설정되어 있지만 관리자가 해제하거나 사용하지 않도록 설정하여 서버 인스턴스를 이 클래스에 표시하지 않을 수 있습니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 표시되는 모든 SQL Server 인스턴스에 대한 정보를 검색하여 콘솔 창에 표시합니다.  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
