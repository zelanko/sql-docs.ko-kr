---
title: 데이터베이스 미러링 - 네트워크 액세스 허용 - Windows 인증 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f66217471aa71d4c5552a8354221acc191a0dc09
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="database-mirroring---allow-network-access---windows-authentication"></a>데이터베이스 미러링 - 네트워크 액세스 허용 - Windows 인증
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows 인증을 사용하여 두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스 미러링 끝점을 연결하려면 다음과 같은 조건에서 로그인 계정의 수동 구성이 필요합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 동일 도메인 또는 신뢰할 수 있는 도메인에서 다른 도메인 계정을 사용하여 서비스로 실행될 경우 각 계정의 로그인을 각 원격 서버 인스턴스에서 **마스터** 로 만들어야 하며, 해당 로그인에는 해당 끝점에 대한 CONNECT 권한이 부여되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 네트워크 서비스 계정으로 실행될 경우 각 호스트 컴퓨터 계정(*DomainName***\\***ComputerName$*)의 로그인은 각 원격 서버 인스턴스에서 **마스터**로 만들어야 하며, 해당 로그인에는 해당 끝점에 대한 CONNECT 권한이 부여되어 있어야 합니다. 네트워크 서비스 계정을 사용하여 서버 인스턴스를 실행할 경우 호스트 컴퓨터의 도메인 계정을 사용하여 인증이 수행되기 때문입니다.  
  
> [!NOTE]  
>  서버 인스턴스마다 끝점이 있는지 확인합니다. 자세한 내용은 [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)를 참조하세요.  
  
### <a name="to-configure-logins-for-windows-authentication"></a>Windows 인증에 대한 로그인을 구성하려면  
  
1.  각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 사용자 계정에 대해 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 로그인을 만듭니다. FROM WINDOWS 절을 사용하여 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 문을 사용합니다.  
  
     자세한 내용은 [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)를 참조하세요.  
  
2.  또한 로그인 사용자가 끝점에 액세스할 수 있도록 하려면 [GRANT](../../t-sql/statements/grant-transact-sql.md) 문을 사용하여 로그인에 끝점에 대한 연결 권한을 부여합니다. 사용자가 관리자인 경우 끝점에 대한 연결 권한을 부여할 필요가 없습니다.  
  
     자세한 내용은 [Grant a Permission to a Principal](../../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)을(를) 참조하세요.  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도메인에 속하는 `Otheruser` 사용자 계정에 대해 `Adomain`로그인을 만듭니다. 그런 다음 `Mirroring_Endpoint`라는 미리 작성된 데이터베이스 미러링 끝점에 연결할 수 있는 권한을 이 사용자에게 부여합니다.  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
