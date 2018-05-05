---
title: 데이터 원본 예 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19e5596107f5bae9ceeab8ae105203e89584e854
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-example"></a>데이터 원본 예
원본 정보는 Microsoft® Windows NT® 서버/Windows 2000 Server, Microsoft Windows NT 워크스테이션/Windows 2000 Professional 또는 Microsoft Windows® 95/98, 컴퓨터 데이터를 실행 하는 컴퓨터에서 레지스트리에 저장 됩니다. 레지스트리에 따라 키 정보 아래에 저장 된, 데이터 원본 이라고는 *사용자 데이터 원본이* 또는 *시스템 데이터 원본*합니다. 사용자 데이터 원본 HKEY_CURRENT_USER 키 아래에 저장 됩니다 및 현재 사용자에만 사용할 수 있습니다. 시스템 데이터 원본은 HKEY_LOCAL_MACHINE 키 아래에서 저장 되 고 하나의 컴퓨터에 둘 이상의 사용자가 사용할 수 있습니다. 도 액세스할 수 있게 데이터 원본에 없는 사용자가 컴퓨터에 로그온 하는 경우에는 시스템 전체 서비스에서 사용할 수 있습니다. 사용자 및 시스템 데이터 원본에 대 한 자세한 내용은 참조 [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)합니다.  
  
 사용자가 사용자 데이터 원본은 다음 세 가지 경우를 가정해 볼: Oracle DBMS;를 사용 하 여 담당자 및 인벤토리를 및 Microsoft SQL Server DBMS를 사용 하 여 급여 합니다. 데이터 원본에 대 한 레지스트리 값 수 있습니다.  
  
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
  
 고 급여 데이터 원본에 대 한 레지스트리 값 수 있습니다.  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
