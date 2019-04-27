---
title: AlwaysOn 가용성 그룹 (SQL Server) 또는 데이터베이스 미러링에 대 한 로그인 계정 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- logins [SQL Server], database mirroring
ms.assetid: e9f5287b-1325-4cda-88a6-19eaaa52a652
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fd397349bc3fa3ed7f69e9e1293415ea96fc75d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754317"
---
# <a name="set-up-login-accounts-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대한 로그인 계정 설정(SQL Server)
  두 서버 인스턴스가 서로의 [데이터베이스 미러링 엔드포인트](the-database-mirroring-endpoint-sql-server.md) 포인트에 연결할 수 있으려면 각 인스턴스의 로그인 계정에 다른 인스턴스에 대한 액세스가 필요합니다. 또한 각 로그인 계정에는 다른 인스턴스의 데이터베이스 미러링 엔드포인트에 대한 CONNECT 권한도 있어야 합니다.  
  
 이 요구 사항의 영향은 서버 인스턴스가 동일한 도메인 사용자 계정으로 실행되는지 여부에 따라 달라집니다.  
  
-   서버 인스턴스가 동일한 도메인 사용자 계정으로 실행되는 경우에는 두 **master** 데이터베이스 모두에 올바른 사용자 로그인이 자동으로 생성됩니다. 이 경우 데이터베이스 미러링 및 AlwaysOn 가용성 그룹에 대한 보안 구성이 단순해집니다.  
  
-   서버 인스턴스가 다른 사용자 계정으로 실행되는 경우 주 서버 인스턴스 또는 주 복제본을 호스팅하는 서버 인스턴스의 사용자 로그인을 미러 서버를 호스팅하는 서버 인스턴스 또는 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 수동으로 재현해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [다른 계정에 대해 로그인 만들기](#CreateLogin) 및 [현재 권한 부여](#GrantConnect)를 참조하십시오.  
  
    > [!IMPORTANT]  
    >  보다 안전한 환경을 만들려면 각 서버 인스턴스에 대해 별도의 도메인 계정을 사용해 보십시오.  
  
##  <a name="CreateLogin"></a> 다른 계정에 대해 로그인 만들기  
 두 서버 인스턴스가 다른 계정으로 실행되는 경우 시스템 관리자는 CREATE LOGIN [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 서버 인스턴스마다 원격 인스턴스의 시작 서비스 계정에 대한 로그인을 만들 수 있습니다. 자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)을 참조하세요.  
  
> [!IMPORTANT]  
>  도메인이 아닌 계정에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 경우 인증서를 사용해야 합니다. 자세한 내용은 [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&amp;#40;Transact-SQL&amp;#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)을 참조하세요.  
  
 예를 들어 loginA에서 실행되는 sqlA 서버 인스턴스의 경우 loginB에서 실행되는 sqlB 서버 인스턴스에 연결하려면 loginA는 sqlB에 있어야 하고 loginB는 sqlA에 있어야 합니다. 또한 미러링 모니터 서버 인스턴스(sqlC)가 있고 서버 인스턴스 3개가 서로 다른 도메인 계정으로 실행되는 데이터베이스 미러링 세션의 경우 다음 로그인을 만들어야 합니다.  
  
|인스턴스|로그인을 만들고 CONNECT 권한 부여할 대상|  
|--------------------|--------------------------------------------------------------|  
|sqlA|sqlB 및 sqlC|  
|sqlB|sqlA 및 sqlC|  
|sqlC|sqlA 및 sqlB|  
  
> [!NOTE]  
>  도메인 사용자 대신 컴퓨터 계정을 사용하여 네트워크 서비스 계정과 연결할 수 있습니다. 컴퓨터 계정을 사용하는 경우 다른 서버 인스턴스의 사용자로 추가해야 합니다.  
  
##  <a name="GrantConnect"></a> 현재 권한 부여  
 서버 인스턴스에 로그인을 만든 후에는 해당 로그인에 서버 인스턴스의 데이터베이스 미러링 엔드포인트에 연결할 권한을 부여해야 합니다. 시스템 관리자는 GRANT [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 CONNECT 권한을 부여합니다. 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용&amp;#40;SQL Server&amp;#41;](../database-mirroring-allow-network-access-windows-authentication.md)  
  
-   [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&amp;#40;Transact-SQL&amp;#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링 엔드포인트&amp;#40;SQL Server&amp;#41;](the-database-mirroring-endpoint-sql-server.md)   
 [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [AlwaysOn 가용성 그룹 구성 문제 해결 &#40;SQL Server&#41;](../availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
