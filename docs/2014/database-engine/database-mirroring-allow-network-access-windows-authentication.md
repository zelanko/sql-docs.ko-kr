---
title: 데이터베이스 미러링 끝점에 대 한 네트워크 액세스
description: SQL Server에 대 한 데이터베이스 미러링 끝점에 대 한 windows authenticatino 네트워크 액세스를 허용 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0d1d8786d128ef2cc99fe571e33f89c4c4e7699c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934468"
---
# <a name="allow-network-access-to-a-database-mirroring-endpoint-using-windows-authentication-sql-server"></a>Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용(SQL Server)
  Windows 인증을 사용하여 두 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스 미러링 엔드포인트를 연결하려면 다음과 같은 조건에서 로그인 계정의 수동 구성이 필요합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 동일 도메인 또는 신뢰할 수 있는 도메인에서 다른 도메인 계정을 사용하여 서비스로 실행될 경우 각 계정의 로그인을 각 원격 서버 인스턴스에서 **마스터** 로 만들어야 하며, 해당 로그인에는 해당 엔드포인트에 대한 CONNECT 권한이 부여되어 있어야 합니다.  
  
-   ph x="1" /&gt; 인스턴스가 네트워크 서비스 계정으로 실행될 경우 각 호스트 컴퓨터 계정(*DomainName***\\***ComputerName$*)의 로그인은 각 원격 서버 인스턴스에서 **마스터** 로 만들어야 하며, 해당 로그인에는 해당 엔드포인트에 대한 CONNECT 권한이 부여되어 있어야 합니다. 네트워크 서비스 계정을 사용하여 서버 인스턴스를 실행할 경우 호스트 컴퓨터의 도메인 계정을 사용하여 인증이 수행되기 때문입니다.  
  
> [!NOTE]  
>  서버 인스턴스마다 엔드포인트가 있는지 확인합니다. 자세한 내용은 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)를 참조하세요.  
  
### <a name="to-configure-logins-for-windows-authentication"></a>Windows 인증에 대한 로그인을 구성하려면  
  
1.  각 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스의 사용자 계정에 대해 다른 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 로그인을 만듭니다. FROM WINDOWS 절을 사용하여 [CREATE LOGIN](/sql/t-sql/statements/create-login-transact-sql) 문을 사용합니다.  
  
     자세한 내용은 [로그인 만들기](../relational-databases/security/authentication-access/create-a-login.md)를 참조하세요.  
  
2.  또한 로그인 사용자가 엔드포인트에 액세스할 수 있도록 하려면 [GRANT](/sql/t-sql/statements/grant-transact-sql) 문을 사용하여 로그인에 엔드포인트에 대한 연결 권한을 부여합니다. 사용자가 관리자인 경우 엔드포인트에 대한 연결 권한을 부여할 필요가 없습니다.  
  
     자세한 내용은 [Grant a Permission to a Principal](../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)을(를) 참조하세요.  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 예에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도메인에 속하는 `Otheruser` 사용자 계정에 대해 `Adomain`로그인을 만듭니다. 그런 다음 `Mirroring_Endpoint`라는 미리 작성된 데이터베이스 미러링 엔드포인트에 연결할 수 있는 권한을 이 사용자에게 부여합니다.  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [데이터베이스 미러링 &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 및 AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 전송 보안&#41;](database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
