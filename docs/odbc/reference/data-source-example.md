---
title: 데이터 원본 예 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f427074f7cd7153f448aaef43bc4ac5dca84c01
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215723"
---
# <a name="data-source-example"></a>데이터 원본 예제
Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT 워크스테이션/Windows 2000 Professional 또는 Microsoft Windows® 95/98 컴퓨터 데이터를 실행 하는 컴퓨터에서 원본 정보는 레지스트리에 저장 됩니다. 사용할 레지스트리에 따라 키 정보는 아래에 저장, 데이터 원본 이라고는 *사용자 데이터 원본* 또는 *시스템 데이터 원본을*합니다. 사용자 데이터 원본 HKEY_CURRENT_USER 키 아래에 저장 됩니다 및 현재 사용자 에게만 제공 됩니다. 시스템 데이터 원본 HKEY_LOCAL_MACHINE 키 아래 저장 되 고 하나의 컴퓨터에서 둘 이상의 사용자가 사용할 수 있습니다. 또한 없는 사용자가 컴퓨터에 로그온 하는 경우에 데이터 원본에 대 한 액세스를 얻을 수 있습니다는 시스템 전체 서비스에서 사용 수 있습니다. 사용자 및 시스템 데이터 원본에 대 한 자세한 내용은 참조 하세요. [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)합니다.  
  
 사용자가 세 개의 사용자 데이터 소스를 가정 합니다. Oracle DBMS;를 사용 하는 직원 및 인벤토리 및 Microsoft SQL Server DBMS를 사용 하는 급여를 합니다. 데이터 원본에 대 한 레지스트리 값을 수 있습니다.  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 및 급여 데이터 원본에 대 한 레지스트리 값이 될 수 있습니다.  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
