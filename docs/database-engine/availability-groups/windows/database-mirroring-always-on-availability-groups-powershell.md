---
title: 'Powershell: 가용성 그룹 데이터베이스 미러링 엔드포인트'
description: PowerShell을 사용하여 Always On 가용성 그룹에 대한 데이터베이스 미러링 엔드포인트를 만드는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d8cc91d628c365d4f9092ca24a8b4df06f17adf2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252905"
---
# <a name="create-a-database-mirroring-endpoint-for-an-availability-group-using-powershell"></a>PowerShell을 사용하여 가용성 그룹에 대한 데이터베이스 미러링 엔드포인트 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 PowerShell을 사용하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에 사용할 데이터베이스 미러링 엔드포인트를 만드는 방법에 대해 설명합니다.  
  

  
##  <a name="Permissions"></a> 권한  
 CREATE ENDPOINT 권한 또는 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다. 자세한 내용은 [GRANT 엔드포인트 사용 권한&#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.  

> [!IMPORTANT]  
>  RC4 알고리즘은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] AES를 사용하는 것이 좋습니다.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **데이터베이스 미러링 엔드포인트를 만들려면**  
  
1.  데이터베이스 미러링 엔드포인트를 만들 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
2.  **New-SqlHadrEndpoint** cmdlet을 사용하여 엔드포인트를 만든 다음 **Set-SqlHadrEndpoint** 를 사용하여 엔드포인트를 시작합니다.  
  
###  <a name="PShellExample"></a> 예제(PowerShell)  
 다음 PowerShell 명령은 SQL Server 인스턴스(*Machine*\\*Instance*)에 데이터베이스 미러링 엔드포인트를 만듭니다. 이 엔드포인트는 포트 5022를 사용합니다.  
  
> [!IMPORTANT]  
>  이 예는 데이터베이스 미러링 엔드포인트가 현재 없는 서버 인스턴스에서만 작동합니다.  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **데이터베이스 미러링 엔드포인트를 구성하려면**  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **데이터베이스 미러링 엔드포인트에 대한 정보를 보려면**  
  
-   [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
