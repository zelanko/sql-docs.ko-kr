---
title: 미러링 모니터 추가 또는 바꾸기(SSMS)
description: SSMS(SQL Server Management Studio)를 사용하여 데이터베이스 미러링 모니터를 추가하거나 바꾸는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], establishing
- database mirroring [SQL Server], witness
ms.assetid: 4b5ecffd-f025-4ab7-b69d-8958c6477127
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 61e7be7b4e1f61f243d896d5073ae469bebe6940
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75247501"
---
# <a name="add-or-replace-a-database-mirroring-witness-sql-server-management-studio"></a>데이터베이스 미러링 모니터 서버 추가 또는 바꾸기(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 미러링 엔드포인트에서 Windows 인증을 사용하는 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 미러링 모니터 서버를 추가하거나 바꿀 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 미러링 모니터 서버를 추가하면 운영 모드도 자동 장애 조치(Failover)가 있는 보호 우선 모드로 변경됩니다.  
  
> [!NOTE]  
>  미러링 모니터 서버는 파트너 중 별도의 컴퓨터에 있는 것이 좋습니다. 미러링 모니터 서버에서 사용하는 서비스 계정은 주 서버 인스턴스 및 미러 서버 인스턴스에서 사용하는 서비스 계정과 같은 도메인에 있거나 트러스트된 도메인에 있어야 합니다.  
  
### <a name="to-add-or-replace-a-witness"></a>미러링 모니터 서버를 추가하거나 바꾸려면  
  
1.  주 서버 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 미러링 모니터 서버를 추가하거나 바꿀 세션의 주 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  **보안 구성**을 클릭합니다.  
  
5.  **데이터베이스 미러링 보안 구성 마법사** 시작 화면이 나타나면 **다음**을 클릭합니다.  
  
6.  **미러링 모니터 서버 포함** 대화 상자에서 **예**를 클릭한 후 **다음**을 클릭합니다.  
  
7.  **구성할 서버 선택** 대화 상자에서 **미러링 모니터 서버 인스턴스** 확인란이 자동으로 선택됩니다. **다음**을 클릭합니다.  
  
8.  **주 서버 인스턴스** 대화 상자에서 기존 포트와 엔드포인트를 유지합니다. **다음**을 클릭합니다.  
  
9. **미러링 모니터 서버 인스턴스** 대화 상자에서 **연결**을 클릭합니다.  
  
10. **서버에 연결** 대화 상자에서 **서버 이름** 필드에 미러링 모니터 서버 인스턴스를 지정하고 Windows 인증(기본값)을 사용합니다. **연결**을 클릭합니다.  
  
11. 연결이 설정되면 미러링 모니터 서버 인스턴스의 수신기 포트와 데이터베이스 미러링 엔드포인트가 **미러링 모니터 서버 인스턴스** 대화 상자에 표시됩니다. **다음**을 클릭합니다.  
  
12. **서비스 계정** 대화 상자에는 주 서버 인스턴스, 미러 서버 인스턴스 및 미러링 모니터 서버 인스턴스의 도메인 서비스 계정에 대한 필드가 있습니다.  
  
    -   모든 서버 인스턴스에서 같은 서비스 계정을 사용하는 경우 필드를 비워 둡니다.  
  
    -   미러링 모니터 서버 인스턴스에서 파트너 중 하나와 다른 서비스 계정을 사용하는 경우에는 **주 서버**, **미러 서버**및 **미러링 모니터 서버** 필드에 계정 이름을 입력합니다.  
  
         *DOMAINNAME* **\\** *username*  
  
         도메인 이름은 대문자로 입력해야 합니다.  
  
     **다음**을 클릭합니다.  
  
13. 필요에 따라 **마법사 완료** 요약 화면에서 미러링 모니터 서버 구성을 확인한 다음 **마침**을 클릭합니다.  
  
14. 마침을 클릭하면 마법사가 **데이터베이스 속성** 대화 상자로 돌아가고 이제 이 대화 상자의 **미러링 모니터 서버** 필드에 미러링 모니터 서버의 서버 네트워크 주소가 표시됩니다. 또한 미러링 모니터 서버에 필요한 **자동 장애 조치(Failover)가 있는 보호 우선(동기) 모드**가 자동으로 선택됩니다.  
  
     미러링 모니터 서버를 설정하고 세션을 자동 장애 조치(Failover)가 있는 보호 우선 모드로 변경하려면 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)   
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
