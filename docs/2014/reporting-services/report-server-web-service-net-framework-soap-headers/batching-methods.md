---
title: 일괄 처리 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- methods [Reporting Services], batches
- BatchHeader SOAP header
- Web service [Reporting Services], methods
- Report Server Web service, batching
- batches [Reporting Services]
- XML Web service [Reporting Services], methods
- locking [Reporting Services]
- multiple Web service methods
ms.assetid: 86435534-c9fe-4b49-b88c-7fb6d21976b0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 56e58bfdb36e464aa6048343350ea929971989f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112643"
---
# <a name="batching-methods"></a>일괄 처리 메서드
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 SOAP 헤더를 사용하면 단일 작업에 여러 웹 서비스 메서드를 포함시킬 수 있습니다. 메서드는 호출된 순서대로 단일 데이터베이스 트랜잭션의 범위 내에서 실행됩니다.  
  
 다중 메서드 일괄 처리 작업을 사용할 때 얻을 수 있는 이점으로 롤백이 있습니다. 일괄 처리 실행 도중 메서드 호출에서 오류가 발생하면 보고서 서버에서 일괄 처리 실행을 중지하고 모든 이전 작업을 롤백할 수 있습니다. 이 기능은 메서드 호출이 일괄 처리 내 다른 메서드 호출이 성공적으로 완료되는지 여부에 따라 달라지는 경우에 유용합니다.  
  
 웹 서비스에서는 다중 메서드 일괄 처리 작업에 대한 잠금 기능을 제공하지 않습니다. 메시지가 서버에 전송되고 Execute 명령이 호출되기 전까지는 보고서 서버 데이터베이스의 행이 업데이트를 위해 잠기지 않습니다.  
  
 또한 데이터를 마지막으로 읽은 이후 데이터베이스가 변경되지 않았음을 보장하는 동시성 제어도 없습니다. 두 클라이언트가 동일한 항목을 수정할 경우 매개 변수가 유효하면(예: 항목 이름이 바뀌지 않음) 마지막 업데이트가 성공합니다.  
  
 다음 예에서는 <xref:ReportService2005.ReportingService2005.CreateFolder%2A> 메서드를 세 번 호출하고 이러한 호출을 단일 일괄 처리로 실행합니다. <xref:ReportService2005.ReportingService2005.CreateFolder%2A>에 대한 호출 중 하나라도 실패할 경우 전체 일괄 처리가 취소됩니다.  
  
```vb  
Imports System  
Imports System.Web.Services.Protocols  
Imports myNamespace.MyReferenceName  
  
Class Sample  
    Sub Main(args() As String)  
        Dim rs As New ReportingService2005()  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      ' Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        Dim bh As New BatchHeader()  
  
        bh.BatchId = service.CreateBatch()  
        rs.BatchHeaderValue = bh  
        rs.CreateFolder("New Folder1", "/", Nothing)  
        rs.CreateFolder("New Folder2", "/", Nothing)  
        rs.CreateFolder("New Folder3", "/", Nothing)  
  
        Console.WriteLine("Creating folders...")  
        rs.BatchHeaderValue = bh  
        rs.ExecuteBatch()  
        Console.WriteLine("Folders created successfully.")  
  
        rs.BatchHeaderValue = Nothing  
    End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Web.Services.Protocols;   
using myNamespace.MyReferenceName;  
  
class Sample  
{  
    static void Main(string[] args)  
    {  
        ReportingService2005 rs = new ReportingService2005();  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      // Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        BatchHeader bh = new BatchHeader();  
  
        bh1.BatchID = service.CreateBatch();  
        rs.BatchHeaderValue = bh;  
        rs.CreateFolder("New Folder1", "/", null);  
        rs.CreateFolder("New Folder2", "/", null);  
        rs.CreateFolder("New Folder3", "/", null);  
  
        Console.WriteLine("Creating folders...");  
        rs.BatchHeaderValue = bh1;  
        rs.ExecuteBatch();  
        Console.WriteLine("Folders created successfully.");  
  
        rs.BatchHeaderValue = null;  
    }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:ReportService2005.ReportingService2005.CancelBatch%2A>   
 <xref:ReportService2005.ReportingService2005.CreateBatch%2A>   
 [기술 참조&#40;SSRS&#41;](../technical-reference-ssrs.md)   
 [Reporting Services SOAP 헤더 사용](using-reporting-services-soap-headers.md)  
  
  
