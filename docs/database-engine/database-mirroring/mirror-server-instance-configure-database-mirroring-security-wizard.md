---
title: 미러 서버 인스턴스(데이터베이스 미러링 보안 구성 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.mirrorsrvr.f1
ms.assetid: 53223432-615e-440f-904d-925d33ec2144
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d6c83b17b36754f5e424afd830feaa51fd2767d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mirror-server-instance-configure-database-mirroring-security-wizard"></a>미러 서버 인스턴스(데이터베이스 미러링 보안 구성 마법사)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 미러 데이터베이스가 있는 서버 인스턴스에 대한 정보를 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  미러 서버 인스턴스는 주 서버 인스턴스와 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전(Standard 또는 Enterprise)을 실행해야 합니다. 또한 서버 인스턴스는 동일한 작업을 처리할 수 있는 동등한 시스템에서 실행하는 것이 좋습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 구성하려면**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>변수  
 **미러 서버 인스턴스**  
 **데이터베이스 속성** 대화 상자의 **미러링** 페이지에서 미러 서버 인스턴스가 이미 지정되어 있으면 해당 인스턴스가 표시됩니다. 자세한 내용은 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)을 참조하세요.  
  
 그렇지 않은 경우에는 미러 서버 인스턴스의 이름을 입력합니다. 주 서버 인스턴스는 미러 서버 인스턴스로 지정할 수 없습니다.  
  
 **연결**  
 미러 서버 인스턴스가 지정되어 있지 않으면 **연결**을 클릭합니다. 그러면 서버 인스턴스를 지정하고 연결할 수 있는 **서버에 연결** 대화 상자가 표시됩니다.  
  
 인스턴스를 지정했지만 끝점이 있는지 확인할 수 있는 권한을 가진 연결이 없을 경우 **연결**을 클릭합니다. 그러면 서버 인스턴스가 미리 선택되어 있고 변경할 수 없는 **서버에 연결** 대화 상자가 표시됩니다. 충분한 사용 권한을 가진 도메인 계정을 지정하고 서버 인스턴스에 연결합니다.  
  
> [!NOTE]  
>  데이터베이스 미러링 보안 구성 마법사는 서버 인스턴스에 연결할 때 **서버에 연결** 대화 상자에서 지정한 자격 증명을 사용합니다. 이 자격 증명은 서버 인스턴스가 서비스로 실행 중인 시작 계정의 자격 증명을 사용하는 미러링 세션의 자격 증명과는 다릅니다.  
  
 **수신기 포트**  
 이 서버 인스턴스의 미러링 끝점이 있는지 여부에 따라 이 옵션의 동작은 다음과 같이 달라집니다.  
  
-   서버 인스턴스에 대한 수신기 포트가 없으면 **포트** 입력란에 포트 번호 5022가 표시됩니다. 7022와 같은 사용 가능한 임의의 포트 번호를 사용할 수 있습니다.  
  
-   미러링 끝점이 있으면 해당 끝점의 포트 번호가 표시됩니다. 포트를 변경해야 하는 경우 ALTER ENDPOINT 명령을 사용합니다. 자세한 내용은 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)을 참조하세요.  
  
    > [!NOTE]  
    >  포트 번호는 반드시 지정해야 합니다.  
  
 **끝점 이름**  
 이 서버 인스턴스의 미러링 끝점이 있으면 여기에 끝점 이름이 표시됩니다. 끝점이 없으면 끝점 이름을 지정할 수 있습니다.  
  
 **이 끝점으로 보낸 데이터 암호화**  
 암호화는 기본적으로 사용됩니다. 확인란을 선택하면 암호화가 단순히 지원되는 차원을 넘어 필수 항목이 되며 모든 암호화 옵션에 기본값을 사용합니다. 자세한 내용은 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)를 참조하세요.  
  
 암호화를 사용하지 않으려면 이 확인란의 선택을 취소합니다. 암호화를 다시 사용하려면 확인란을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Windows 인증에 대한 데이터베이스 미러링 끝점 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
