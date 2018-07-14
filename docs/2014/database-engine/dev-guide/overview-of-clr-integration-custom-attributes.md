---
title: CLR 통합 사용자 지정 특성 개요 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom attributes [CLR integration]
- attributes [CLR integration]
- common language runtime [SQL Server], attributes
- database objects [CLR integration], custom attributes
- building database objects [CLR integration], custom attributes
ms.assetid: ecf5c097-0972-48e2-a9c0-b695b7dd2820
caps.latest.revision: 39
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2153277cbb0592b808fde3e0a8bec3a8ca582455
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324943"
---
# <a name="overview-of-clr-integration-custom-attributes"></a>CLR 통합 사용자 지정 특성 개요
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 CLR(공용 언어 런타임)에서는 특성이라고 하는 설명적 키워드를 사용할 수 있습니다. 이러한 특성은 메서드와 클래스 같은 많은 요소에 대한 추가적인 정보를 제공합니다. 특성은 개체의 메타데이터와 함께 어셈블리에 저장되며 다른 개발 도구를 위한 코드 설명이나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 런타임 동작 제어에 사용될 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 CLR 루틴을 등록할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 루틴에 대한 속성 집합이 파생됩니다. 이러한 루틴 속성은 루틴에 대한 인덱싱 여부를 비롯한 루틴의 여러 가지 기능을 결정합니다. 예를 들어 `DataAccess` 속성을 `DataAccessKind.Read`로 설정하면 CLR 함수 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 테이블의 데이터에 액세스할 수 있습니다. 다음 예제는 단순한 경우에서는 합니다 `DataAccess` 속성은 사용자 테이블에서 데이터 액세스를 용이 하 게 **table1**합니다.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public partial class UserDefinedFunctions  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static string func1()  
    {  
        // Open a connection and create a command  
        SqlConnection conn = new SqlConnection("context connection = true");  
        conn.Open();  
        SqlCommand cmd = conn.CreateCommand();  
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10";  
        // where table1 is a user table  
        // Execute this command   
        SqlDataReader rd = cmd.ExecuteReader();  
        // Set string ret_val to str_val returned from the query  
        string ret_val = rd.GetValue(0).ToString();  
        rd.Close();  
        return ret_val;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public partial Class UserDefinedFunctions  
    <SqlFunction(DataAccess = DataAccessKind.Read)> _   
    Public Shared Function func1() As String  
        ' Open a connection and create a command  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")   
        conn.Open()  
        Dim cmd As SqlCommand =  conn.CreateCommand()   
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10"  
        ' where table1 is a user table  
        ' Execute this command   
        Dim rd As SqlDataReader =  cmd.ExecuteReader()   
        ' Set string ret_val to str_val returned from the query  
        Dim ret_val As String =  rd.GetValue(0).ToString()   
        rd.Close()  
        Return ret_val  
    End Function  
End Class  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 루틴 정의에서 직접 루틴 속성을 파생합니다. CLR 루틴의 경우에는 이러한 속성을 파생하기 위해 서버가 루틴 본문을 분석하지 않습니다. 대신 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 언어로 구현된 클래스와 클래스 멤버의 사용자 지정 속성을 사용할 수 있습니다.  
  
 CLR 루틴, 사용자 정의 형식 및 집계에 필요한 사용자 지정 특성은 `Microsoft.SqlServer.Server` 네임스페이스에 정의됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 루틴용 사용자 지정 특성](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)  
  
  
