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
ms.openlocfilehash: ec9eacef6f0bd63eb0aaeac36dc97938297d1f16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135642"
---
# <a name="data-source-example"></a>데이터 원본 예제
Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional 또는 Microsoft Windows® 95/98를 실행 하는 컴퓨터에서는 컴퓨터 데이터 원본 정보가 레지스트리에 저장 됩니다. 정보가 저장 되는 레지스트리 키에 따라 데이터 원본을 *사용자 데이터* 원본 또는 *시스템 데이터 원본*이라고 합니다. 사용자 데이터 원본은 HKEY_CURRENT_USER 키 아래에 저장 되며 현재 사용자만 사용할 수 있습니다. 시스템 데이터 원본은 HKEY_LOCAL_MACHINE 키 아래에 저장 되며 한 컴퓨터에서 둘 이상의 사용자가 사용할 수 있습니다. 또한 사용자가 컴퓨터에 로그온 하지 않은 경우에도 데이터 원본에 대 한 액세스 권한을 얻을 수 있는 시스템 전반의 서비스에서 사용할 수 있습니다. 사용자 및 시스템 데이터 원본에 대 한 자세한 내용은 [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)를 참조 하세요.  
  
 사용자에 게 Oracle DBMS를 사용 하는 직원 및 재고 라는 세 가지 사용자 데이터 원본이 있다고 가정 합니다. Microsoft SQL Server DBMS를 사용 하는 및 급여 데이터 원본에 대 한 레지스트리 값은 다음과 같을 수 있습니다.  
  
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
  
 급여 데이터 원본에 대 한 레지스트리 값은 다음과 같을 수 있습니다.  
  
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
