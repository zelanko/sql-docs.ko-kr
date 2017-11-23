---
title: "(분석 플랫폼 시스템) Master 데이터베이스 복원"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: "11"
ms.openlocfilehash: ff00e17d05b13317e009357e8c2089a46cbce4a4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="restore-the-master-database"></a>Master 데이터베이스 복원
**마스터 복원** SQL Server PDW 구성 관리자의 페이지를 사용 하면 백업에서 master 데이터베이스를 복원할 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
> [!IMPORTANT]  
> 복원을 수행 하려면 SQL Server PDW 데이터베이스 카탈로그 및 사용자 보안 정보를 포함 하는 현재 마스터 데이터베이스를 삭제 해야 합니다. 복원을 수행 하기 전에 현재 master 데이터베이스의 백업을 수행 하는 것이 좋습니다.  
  
## <a name="to-restore-the-master-database"></a>master 데이터베이스를 복원하려면  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 참조 [구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41; ](launch-the-configuration-manager.md).  
  
2.  구성 관리자의 왼쪽된 창에서 클릭 **마스터 복원**합니다.  
  
3.  마스터 복원할 백업 파일을 선택 합니다.  
  
4.  **적용**을 클릭합니다.  
  
5.  복원을 수행 하려면 SQL Server PDW 어플라이언스 서비스를 모두 종료 되며 모든 사용자 연결을 해제 합니다. 복원을 완료 한 후에 SQL Server PDW 어플라이언스 서비스 다시 시작 됩니다.  
  
![DWConfig 어플라이언스 PDW 마스터 복원](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
