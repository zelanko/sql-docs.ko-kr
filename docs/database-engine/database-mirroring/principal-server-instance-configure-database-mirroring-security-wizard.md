---
title: 주 서버 인스턴스(데이터베이스 미러링 보안 구성 마법사)
description: SQL Server Management Studio ‘데이터베이스 미러링 보안 구성’ 마법사의 ‘주 서버 인스턴스’ 페이지에 대한 설명입니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8d48c59b06202f898fdf61746aee9f62ca155da6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75255958"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>주 서버 인스턴스(데이터베이스 미러링 보안 구성 마법사)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 주 데이터베이스의 서버 인스턴스에 대한 정보를 지정할 수 있습니다. 주 데이터베이스는 미러링 세션을 시작하는 데이터베이스의 복사본입니다. 세션이 시작된 후 주 데이터베이스는 사용자 변경 내용을 받아들이는 데이터베이스의 복사본입니다. 장애 조치(Failover)가 일어나면 주 역할과 미러링 역할이 서로 바뀌므로 처음의 주 데이터베이스가 주 데이터베이스로 유지되지 않을 수도 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 구성하려면**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>옵션  
 **주 서버 인스턴스**  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 데이터베이스 미러링은 항상 주 서버에서 구성하기 때문에 현재 서버 인스턴스는 항상 주 서버 인스턴스입니다.  
  
 **수신기 포트**  
 이 서버 인스턴스의 미러링 엔드포인트가 있는지 여부에 따라 이 옵션의 동작은 다음과 같이 달라집니다.  
  
-   이 서버 인스턴스에 대한 수신기 포트가 없으면 **포트** 입력란에 포트 번호 5022가 표시됩니다. 7022와 같은 사용 가능한 임의의 포트 번호를 사용할 수 있습니다.  
  
-   미러링 엔드포인트가 있으면 해당 엔드포인트의 포트 번호가 표시됩니다. 포트를 변경해야 하는 경우 ALTER ENDPOINT 명령을 사용합니다. 자세한 내용은 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  포트 번호는 반드시 지정해야 합니다.  
  
 **엔드포인트 이름**  
 이 서버 인스턴스의 미러링 엔드포인트가 있으면 여기에 엔드포인트 이름이 표시됩니다. 엔드포인트가 없으면 엔드포인트 이름을 지정할 수 있습니다.  
  
 **이 엔드포인트로 보낸 데이터 암호화**  
 암호화는 기본적으로 사용됩니다. 확인란을 선택하면 암호화가 단순히 지원되는 차원을 넘어 필수 항목이 되며 모든 암호화 옵션에 기본값을 사용합니다. 자세한 내용은 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
 암호화를 사용하지 않으려면 이 확인란의 선택을 취소합니다. 암호화를 다시 사용하려면 확인란을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
