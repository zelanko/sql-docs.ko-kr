---
description: 서버 등록
title: 서버 등록
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlserverregisteredserver.dhelp
helpviewer_keywords:
- connections [SQL Server], registered servers
- registering servers
- servers [SQL Server], registering
- server management [SQL Server], registering servers
- server registration [SQL Server]
ms.assetid: c2a2513e-fa09-419c-99e7-a12d57c5a0db
author: markingmyname
ms.author: maghan
ms.manageR: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 3bd61a8a290f8863d13c2052d0a50835461c5aae
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038398"
---
# <a name="register-servers"></a>서버 등록

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 서버를 등록하면 나중에 연결하기 위한 서버 연결 정보를 저장할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 서버를 등록하는 방법은 3가지가 있습니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 로컬 인스턴스는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 설치한 후 처음 시작할 때 자동으로 등록됩니다.  
  
2.  언제든지 자동 등록 과정을 시작하여 로컬 서버 인스턴스의 등록을 복원할 수도 있습니다.  
  
3.  마지막으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 등록된 서버 도구를 사용하여 서버를 등록할 수 있습니다.  
  
## <a name="benefits-of-registered-servers"></a>등록된 서버의 이점  
 등록된 서버를 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   서버를 등록하여 연결 정보를 유지합니다.  
  
-   등록된 서버가 실행 중인지 확인합니다.  
  
-   개체 탐색기와 쿼리 편집기를 등록된 서버에 쉽게 연결합니다.  
  
-   등록된 서버에 대한 등록 정보를 편집하거나 삭제합니다.  
  
-   서버 그룹을 만듭니다.  
  
-   **서버 이름** 목록과 다른 **등록된 서버 이름** 상자에 값을 제공하여 등록된 서버에 대한 친숙한 이름을 제공합니다.  
  
-   등록된 서버에 대한 세부적인 설명을 제공합니다.  
  
-   등록된 서버 그룹에 대한 세부적인 설명을 제공합니다.  
  
-   등록된 서버 그룹을 내보냅니다.  
  
-   등록된 서버 그룹을 가져옵니다.  
  
-   온라인 또는 오프라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그 파일을 봅니다.  
  
## <a name="related-tasks"></a>관련 작업  
 등록된 서버를 시작하려면 다음 항목을 사용하십시오.  
  
|**설명**|**항목**|  
|---------------------|---------------|  
|로컬 서버 인스턴스 등록|[연결된 서버 등록&#40;SQL Server Management Studio&#41;](./register-a-connected-server-sql-server-management-studio.md)|  
|서버 등록|[새 등록된 서버 만들기&#40;SQL Server Management Studio&#41;](./create-a-new-registered-server-sql-server-management-studio.md)|  
|등록된 서버 보기|[SQL Server Management Studio에서 등록된 서버 보기](./view-registered-servers-in-sql-server-management-studio.md)|  
|등록된 서버 제거|[등록된 서버 제거&#40;SQL Server Management Studio&#41;](./remove-a-registered-server-sql-server-management-studio.md)|  
|서버 등록 변경|[서버 등록 변경&#40;SQL Server Management Studio&#41;](./change-a-server-s-registration-sql-server-management-studio.md)|  
|등록된 서버에 연결|[등록된 서버에 연결&#40;SQL Server Management Studio&#41;](./connect-to-a-registered-server-sql-server-management-studio.md)|  
|등록된 서버에서 연결 끊기|[등록된 서버에서 연결 끊기&#40;SQL Server Management Studio&#41;](./disconnect-from-a-registered-server-sql-server-management-studio.md)|  
|등록된 서버 또는 서버 그룹 이동|[등록된 서버 및 등록된 서버 그룹 이동&#40;SQL Server Management Studio&#41;](./move-a-registered-server-or-registered-server-group.md)|  
|등록된 서버 또는 등록된 서버 그룹 이름 변경|[등록된 서버 또는 등록된 서버 그룹 이름 변경&#40;SQL Server Management Studio&#41;](./change-the-name-of-registered-server-or-registered-server-group.md)|  
|서버 그룹 만들기 또는 편집|[서버 그룹 만들기 또는 편집&#40;SQL Server Management Studio&#41;](./create-or-edit-a-server-group-sql-server-management-studio.md)|  
|서버 그룹 제거|[서버 그룹 제거&#40;SQL Server Management Studio&#41;](./remove-a-server-group-sql-server-management-studio.md)|  
|등록된 서버 정보 내보내기|[등록된 서버 정보 내보내기&#40;SQL Server Management Studio&#41;](./export-registered-server-information-sql-server-management-studio.md)|  
|등록된 서버 정보 가져오기|[등록된 서버 정보 가져오기&#40;SQL Server Management Studio&#41;](./import-registered-server-information-sql-server-management-studio.md)|  
|중앙 관리 서버 및 서버 그룹 만들기|[중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](./create-a-central-management-server-and-server-group.md)|  
|여러 서버에 대해 동시에 문 실행|[여러 서버에 대해 동시에 문 실행&#40;SQL Server Management Studio&#41;](./execute-statements-against-multiple-servers-simultaneously.md)|  
  
## <a name="see-also"></a>참고 항목  
 [원격 서버](../../database-engine/configure-windows/remote-servers.md)  
  
