---
title: 샘플:.NET Framework를 사용 하 여 WMI 이벤트 공급자 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Server Events, samples
- sample applications [WMI]
- managed code [WMI]
ms.assetid: 3d7aa7e9-0bb3-4a5b-9a3c-047f3240a6f8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6660a5a2e53c5ff4959826a72b779876c27a67a9
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216971"
---
# <a name="sample-using-the-wmi-event-provider-with-the-net-framework"></a>샘플: .NET Framework에서 WMI 이벤트 공급자 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  다음 예에서는 WMI 이벤트 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 설치 인스턴스에서 발생하는 모든 DDL 이벤트에 대한 이벤트 데이터를 반환하는 응용 프로그램을 C#으로 만듭니다.  
  
## <a name="example"></a>예제  
 이 예는 다음 명령 파일을 사용하여 컴파일됩니다.  
  
```  
set compiler_path=C:\WINNT\Microsoft.NET\Framework\v2.0.50110  
  
%compiler_path%\csc %1  
```  
  
```  
using System;  
using System.Management;  
  
class SQLWEPExample   
{  
    public static void Main(string[] args)  
    {  
        string query =  @"SELECT * FROM DDL_EVENTS " ;  
        // Default namespace for default instance of SQL Server   
        string managementPath =  
            @"\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER";  
        ManagementEventWatcher  watcher =   
            new ManagementEventWatcher(new WqlEventQuery (query));  
        ManagementScope scope = new ManagementScope (managementPath);  
        scope.Connect();  
        watcher.Scope = scope;  
        Console.WriteLine("Watching...");  
        while (true)  
        {  
            ManagementBaseObject obj = watcher.WaitForNextEvent();  
            Console.WriteLine("Event!");  
            foreach (PropertyData data in obj.Properties)  
            {  
                Console.Write("{0}:", data.Name);  
                if (data.Value == null)  
                {  
                    Console.WriteLine("<null>");  
                }  
                else  
                {  
                    Console.WriteLine(data.Value.ToString());  
                }  
            }  
            Console.WriteLine("-----");  
            Console.WriteLine();  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [서버 이벤트용 WMI 공급자 개념](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
