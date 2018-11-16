---
title: 최소 구성으로 SQL Server 시작 | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed12d2db1f0f23d7a848b3905e0084413ed897ac
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602003"
---
# <a name="start-sql-server-with-minimal-configuration"></a>최소 구성으로 SQL Server 시작
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  서버를 시작할 수 없게 하는 구성 문제가 있는 경우 최소 구성 시작 옵션을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스를 시작할 수 있습니다. 이 옵션은 시작 옵션 **-f**입니다. 최소 구성으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작하면 자동으로 서버가 단일 사용자 모드로 배치됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스를 최소 구성 모드로 시작할 경우 다음에 유의하십시오.  
  
-   한 명의 사용자만 연결할 수 있고 `CHECKPOINT` 프로세스는 실행되지 않습니다.  
  
-   원격 액세스와 미리 읽기는 사용할 수 없습니다.  
  
-   시작 저장 프로시저는 실행되지 않습니다.  

-   `tempdb`는 가능한 최소 크기로 구성됩니다.
  
 서버를 최소 구성으로 시작한 후에는 해당 서버 옵션 값을 변경하고 서버를 중지한 다음 다시 시작해야 합니다.  
  
> [!IMPORTANT]  
>  **sqlcmd** 유틸리티 및 관리자 전용 연결(DAC)을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 있습니다. 일반 연결을 사용하는 경우 최소 구성 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하기 전에 SQL Server 에이전트 서비스를 중단하십시오. 그렇지 않으면 SQL Server 에이전트 서비스가 연결을 사용함으로써 차단합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [데이터베이스 관리자를 위한 진단 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
