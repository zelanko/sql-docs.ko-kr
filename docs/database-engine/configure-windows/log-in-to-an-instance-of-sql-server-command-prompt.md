---
title: SQL Server 인스턴스에 로그인(명령 프롬프트) | Microsoft Docs
description: "\"sqlcmd\" 유틸리티에 대해 알아봅니다. 명령 프롬프트에서 이 유틸리티를 사용하여 SQL Server 인스턴스에 대한 연결을 테스트하는 방법을 알아봅니다."
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0723a5d463757eca93dd7bacb1fc2b8fe232cdd8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772410"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>SQL Server 인스턴스에 로그인(명령 프롬프트)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 연결을 테스트하고 **sqlcmd** 유틸리티를 사용하는 방법에 대해 설명합니다.  
  
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
  
  
