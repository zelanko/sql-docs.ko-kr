---
title: Master 데이터베이스-분석 플랫폼 시스템 (APS) 복원 Microsoft Docs
description: Master 데이터베이스를 APS (Analytics Platform System)에 복원 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 624e1199fb953945ae6476a1f935dded48508bab
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176141"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Analytics Platform System (APS)에서 master 데이터베이스 복원
SQL Server PDW Configuration Manager의 **복원 마스터** 페이지를 사용 하 여 백업에서 master 데이터베이스를 복원할 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
> [!IMPORTANT]  
> 복원을 수행 하려면 SQL Server PDW 사용자 보안 정보 및 데이터베이스 카탈로그가 포함 된 현재 master 데이터베이스를 삭제 해야 합니다. 복원 작업을 수행 하기 전에 현재 master 데이터베이스의 백업을 만드는 것이 좋습니다.  
  
## <a name="to-restore-the-master-database"></a>master 데이터베이스를 복원하려면  
  
1.  Configuration Manager를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  Configuration Manager의 왼쪽 창에서 **Master 복원**을 클릭 합니다.  
  
3.  복원할 마스터 백업을 선택 합니다.  
  
4.  **적용**을 클릭합니다.  
  
5.  복원을 수행 하려면 SQL Server PDW 모든 어플라이언스 서비스를 종료 하 고 모든 사용자의 연결을 끊습니다. 복원이 완료 된 후 SQL Server PDW는 어플라이언스 서비스를 다시 시작 합니다.  
  
![Dwconfig 어플라이언스 PDW 복원 마스터](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
