---
title: 데이터베이스 미러링 엔드포인트에 대한 인증서 사용
descriptoin: Steps to configure the use of a certificate on both inbound and outbound connections for a SQL Server database mirroring endpoint.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d263276c392ef4fb40682b832cf94237694d94ac
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822328"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>데이터베이스 미러링 엔드포인트에 대한 인증서 사용(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  지정된 서버 인스턴스에서 데이터베이스 미러링에 인증서 인증을 사용하려면 시스템 관리자가 아웃바운드 및 인바운드 연결 모두에 인증서를 사용하도록 각 서버 인스턴스를 구성해야 합니다. 이 경우 아웃바운드 연결을 먼저 구성해야 합니다.  
  
> [!NOTE]  
>  서버 인스턴스의 모든 미러링 연결은 단일 데이터베이스 미러링 엔드포인트를 사용하며 이러한 엔드포인트를 만들 때는 서버 인스턴스의 인증 방법을 지정해야 합니다. 따라서 데이터베이스 미러링에 사용할 서버 인스턴스마다 한 형식의 인증만 사용할 수 있습니다.  
  
## <a name="configuring-outbound-connections"></a>아웃바운드 연결 구성  
 데이터베이스 미러링을 구성할 각 서버 인스턴스에 대해 다음 단계를 수행합니다.  
  
1.  **master** 데이터베이스에서 데이터베이스 마스터 키를 만듭니다.  
  
2.  **master** 데이터베이스에서 서버 인스턴스의 암호화된 인증서를 만듭니다.  
  
3.  서버 인스턴스의 인증서를 사용하여 해당 인스턴스의 엔드포인트를 만듭니다.  
  
4.  인증서를 파일에 백업한 다음 안전한 다른 시스템으로 복사합니다.  
  
 파트너와 미러링 모니터 각각에 대해 이러한 단계를 완료해야 합니다.  
  
 자세햔 내용은 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)을 참조하세요.  
  
## <a name="configuring-inbound-connections"></a>인바운드 연결 구성  
 데이터베이스 미러링을 구성할 각 파트너에 대해 다음 단계를 수행합니다. **master** 데이터베이스에서 다음을 수행합니다.  
  
1.  다른 시스템에 대한 로그인을 만듭니다.  
  
2.  해당 로그인의 사용자를 만듭니다.  
  
3.  다른 서버 인스턴스의 미러링 엔드포인트에 대한 인증서를 얻습니다.  
  
4.  2단계에서 만든 사용자에 인증서를 연결합니다.  
  
5.  해당 미러링 엔드포인트에 대한 로그인에 CONNECT 권한을 부여합니다.  
  
 미러링 모니터가 있는 경우 그에 대한 인바운드 연결도 설정해야 합니다. 이렇게 하려면 양쪽 파트너 모두에서 미러링 모니터에 대한 로그인, 사용자 및 인증서를 설정해야 합니다.  
  
 자세햔 내용은 [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)을 참조하세요.  
  
## <a name="security"></a>보안  
 네트워크 보안을 보장할 수 없는 경우 데이터베이스 미러링 연결에 암호화를 사용하는 것이 좋습니다. 자세한 내용은 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)을 참조하세요.  
  
 인증서를 다른 시스템으로 복사할 때는 안전한 복사 방법을 사용하세요. 모든 인증서를 안전하게 보관하는 데 많은 주의를 기울여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 마스터 키 만들기](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
