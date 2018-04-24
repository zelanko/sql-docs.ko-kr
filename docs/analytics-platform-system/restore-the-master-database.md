---
title: Master 데이터베이스 복원-분석 플랫폼 시스템 | Microsoft Docs
description: 분석 플랫폼 시스템에 있는 master 데이터베이스를 복원 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>분석 플랫폼 시스템에 있는 master 데이터베이스 복원
**마스터 복원** SQL Server PDW 구성 관리자의 페이지를 사용 하면 백업에서 master 데이터베이스를 복원할 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
> [!IMPORTANT]  
> 복원을 수행 하려면 SQL Server PDW 데이터베이스 카탈로그 및 사용자 보안 정보를 포함 하는 현재 마스터 데이터베이스를 삭제 해야 합니다. 복원을 수행 하기 전에 현재 master 데이터베이스의 백업을 수행 하는 것이 좋습니다.  
  
## <a name="to-restore-the-master-database"></a>master 데이터베이스를 복원하려면  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 참조 [구성 관리자를 시작 &#40;분석 플랫폼 시스템&#41;](launch-the-configuration-manager.md)합니다.  
  
2.  구성 관리자의 왼쪽된 창에서 클릭 **마스터 복원**합니다.  
  
3.  마스터 복원할 백업 파일을 선택 합니다.  
  
4.  **적용**을 클릭합니다.  
  
5.  복원을 수행 하려면 SQL Server PDW 어플라이언스 서비스를 모두 종료 되며 모든 사용자 연결을 해제 합니다. 복원을 완료 한 후에 SQL Server PDW 어플라이언스 서비스 다시 시작 됩니다.  
  
![DWConfig 어플라이언스 PDW 마스터 복원](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
