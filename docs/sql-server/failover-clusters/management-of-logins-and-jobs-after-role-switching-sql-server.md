---
title: 미러 장애 조치(failover) 후 로그인 및 작업 관리
description: 미러된 데이터베이스를 주 데이터베이스에서 보조 데이터베이스로 장애 조치(failover)한 후 로그인 및 작업을 관리하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- role switching [SQL Server]
ms.assetid: fc2fc949-746f-40c7-b5d4-3fd51ccfbd7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 234657a06ca2162bffc9448a1424820ead00f0c3
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988340"
---
# <a name="management-of-logins-and-jobs-after-role-switching-sql-server"></a>역할 전환 후 로그인 및 작업 관리(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 고가용성 또는 재해 복구 솔루션을 배포하는 경우 **master** 또는 **msdb** 데이터베이스에 해당 데이터베이스에 대해 저장되는 관련 정보를 다시 생성해야 합니다. 대개 관련 정보에는 주 데이터베이스의 작업과 데이터베이스에 연결해야 하는 프로세스 또는 사용자의 로그인이 포함됩니다. 보조/미러 데이터베이스를 호스팅하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 이 정보를 복제해야 합니다. 가능하다면 역할이 전환된 후 새 주 데이터베이스에서 프로그래밍 방식으로 해당 정보를 다시 생성하는 것이 가장 좋습니다.  
  
## <a name="logins"></a>로그인  
 데이터베이스 복사본을 호스팅하는 모든 서버 인스턴스에서 주 데이터베이스에 대한 액세스 권한이 있는 로그인을 다시 생성해야 합니다. 주 역할이 전환되는 경우 새 주 서버 인스턴스에 로그인이 있는 사용자만 새 주 데이터베이스에 액세스할 수 있습니다. 새 주 서버 인스턴스에 로그인이 정의되어 있지 않은 사용자는 분리된 상태가 되어 데이터베이스에 액세스할 수 없습니다.  
  
 사용자가 분리된 경우 새 주 서버 인스턴스에서 로그인을 만들고 [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)을 실행합니다. 자세한 내용은 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)을 실행합니다.  
  
###  <a name="logins-of-applications-that-use-sql-server-authentication-or-a-local-windows-login"></a><a name="SSauthentication"></a> SQL Server 인증 또는 로컬 Windows 로그인을 사용하는 애플리케이션의 로그인  
 애플리케이션에서 SQL Server 인증 또는 로컬 Windows 로그인을 사용하는 경우 일치하지 않는 SID로 인해 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 애플리케이션의 로그인이 확인되지 않을 수 있습니다. 일치하지 않는 SID로 인해 해당 로그인이 원격 서버 인스턴스에서 분리된 사용자가 됩니다. 이 문제는 애플리케이션이 장애 조치(Failover) 후 미러링된 데이터베이스 또는 로그 전달 데이터베이스에 연결하거나 백업에서 초기화된 복제 구독자 데이터베이스에 연결하는 경우에 발생할 수 있습니다.  
  
 이 문제를 방지하려면 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 호스팅하는 데이터베이스를 사용하도록 애플리케이션을 설정할 때 예방 조치를 취하는 것이 좋습니다. 예방 조치에는 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 로그인 및 암호를 전송하는 것이 포함됩니다. 이 문제를 방지하는 방법에 대한 자세한 내용은 KB 문서 918992 [SQL Server 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992/)을 참조하세요.  
  
> [!NOTE]  
>  이 문제는 다른 컴퓨터의 Windows 로컬 계정에 영향을 줍니다. 하지만 도메인 계정에서는 SID가 각 컴퓨터에서 동일하기 때문에 이러한 문제가 발생하지 않습니다.  
  
 자세한 내용은 [데이터베이스 미러링 및 로그 전달에서의 분리된 사용자](/archive/blogs/sqlserverfaq/orphaned-users-with-database-mirroring-and-log-shipping) (데이터베이스 엔진 블로그)를 참조하세요.  
  
## <a name="jobs"></a>교육  
 백업과 같은 작업에는 특별한 주의가 필요합니다. 일반적으로 역할 전환 후 데이터베이스 소유자 또는 시스템 관리자는 새 주 데이터베이스의 작업을 다시 만들어야 합니다.  
  
 이전 주 서버 인스턴스를 사용할 수 있는 경우 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 원래 작업을 삭제해야 합니다. 현재 미러 데이터베이스가 RESTORING 상태에 있어서 사용할 수 없으므로 현재 미러 데이터베이스의 작업은 실패합니다.  
  
> [!NOTE]  
>  각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 드라이브 문자를 다르게 지정하는 등의 방법으로 서로 다르게 구성할 수 있습니다. 각 파트너에 대한 작업 시 이러한 모든 차이점을 감안해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
