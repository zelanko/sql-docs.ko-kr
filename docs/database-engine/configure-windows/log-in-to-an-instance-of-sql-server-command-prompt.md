---
title: "SQL Server 인스턴스에 로그인(명령 프롬프트) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 00b2a66c23d60597c3a2c4c0f66a660788b3c0af
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>SQL Server 인스턴스에 로그인(명령 프롬프트)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 테스트하고 **sqlcmd** 유틸리티를 사용하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>SQL Server의 기본 인스턴스에 로그인하려면  
  
1.  명령 프롬프트에서 다음 명령을 입력하여 Windows 인증을 통해 연결합니다.  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>SQL Server의 명명된 인스턴스에 로그인하려면  
  
1.  명령 프롬프트에서 다음 명령을 입력하여 Windows 인증을 통해 연결합니다.  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [osql 유틸리티](../../tools/osql-utility.md)  
  
  
