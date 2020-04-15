---
title: 데이터 원본 예제 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306524"
---
# <a name="data-source-example"></a>데이터 원본 예제
마이크로소프트를 실행 하는 컴퓨터에® 윈도우 NT® 서버/윈도우 2000 서버, 마이크로소프트 윈도 NT 워크 스테이션/윈도우 2000 전문가, 또는 마이크로소프트 윈도 ® 95/98, 기계 데이터 소스 정보는 레지스트리에 저장 됩니다. 정보가 저장되는 레지스트리 키에 따라 데이터 원본을 사용자 *데이터 원본* 또는 *시스템 데이터 원본이라고*합니다. 사용자 데이터 원본은 HKEY_CURRENT_USER 키 아래에 저장되며 현재 사용자만 사용할 수 있습니다. 시스템 데이터 원본은 HKEY_LOCAL_MACHINE 키 아래에 저장되며 한 컴퓨터에서 둘 이상의 사용자가 사용할 수 있습니다. 또한 시스템 전체 서비스에서 사용할 수 있으며, 컴퓨터에 로그온한 사용자가 없는 경우에도 데이터 원본에 액세스할 수 있습니다. 사용자 및 시스템 데이터 원본에 대한 자세한 내용은 [SQLManageDataSource](../../odbc/reference/syntax/sqlmanagedatasources.md)를 참조하십시오.  
  
 사용자가 Oracle DBMS를 사용하는 인력 및 인벤토리의 세 가지 사용자 데이터 원본이 있다고 가정합니다. Microsoft SQL Server DBMS를 사용하는 급여입니다. 데이터 원본의 레지스트리 값은 다음과 같은 것일 수 있습니다.  
  
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
  
 급여 데이터 원본의 레지스트리 값은 다음과 같은 것일 수 있습니다.  
  
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
