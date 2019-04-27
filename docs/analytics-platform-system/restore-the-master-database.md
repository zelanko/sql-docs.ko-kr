---
title: Master 데이터베이스 복원-Analytics Platform System | Microsoft Docs
description: Analytics Platform System에 master 데이터베이스를 복원 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678438"
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>Analytics Platform System에 master 데이터베이스 복원
합니다 **마스터 복원** 페이지 SQL Server PDW 구성 관리자의 master 데이터베이스 백업에서 복원할 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
> [!IMPORTANT]  
> 복원을 수행 하려면 SQL Server PDW는 데이터베이스 카탈로그 및 사용자 보안 정보를 포함 하는 현재 마스터 데이터베이스를 삭제 해야 합니다. 현재 마스터 데이터베이스의 백업을 복원 하기 전에 수행 하는 것이 좋습니다.  
  
## <a name="to-restore-the-master-database"></a>master 데이터베이스를 복원하려면  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.  
  
2.  구성 관리자의 왼쪽된 창에서 클릭 **마스터 복원**합니다.  
  
3.  마스터 복원할 백업 파일을 선택 합니다.  
  
4.  **적용**을 클릭합니다.  
  
5.  복원을 수행 하려면 SQL Server PDW 어플라이언스에 모든 서비스를 종료 하 고 모든 사용자 연결 끊기 됩니다. 복원이 완료 된 후에 SQL Server PDW 어플라이언스에 서비스 다시 시작 됩니다.  
  
![DWConfig 어플라이언스 PDW 마스터 복원](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
