---
title: 데이터베이스 엔진 액세스에 대한 파일 시스템 권한 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- file system permissions
- service account [SQL Server], file system permissions
- permissions [SQL Server], file system
ms.assetid: 78bba43c-4edb-4216-84ac-d6246ae5546d
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7438b2ba6a1a908d47dec55c6773645a4f3ead85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32865298"
---
# <a name="configure-file-system-permissions-for-database-engine-access"></a>데이터베이스 엔진 액세스에 대한 파일 시스템 사용 권한 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 데이터베이스 파일이 저장된 위치에 파일 시스템 즉, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대한 액세스 권한을 부여하는 방법에 대해 설명합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스를 사용하려면 Windows 파일 시스템에서 데이터베이스 파일이 저장된 파일 폴더에 액세스할 수 있는 권한이 있어야 합니다. 기본 위치에 대한 사용 권한은 설치 중에 구성됩니다. 데이터베이스 파일을 다른 위치에 저장한 경우 다음 단계를 수행하여 해당 위치에 대한 모든 권한을 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 부여해야 할 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 사용 권한부터 각 서비스에 대해 서비스별 SID에 할당됩니다. 이 시스템에서는 서비스 격리 및 철저한 방어 기능을 제공하도록 돕습니다. 서비스별 SID는 서비스 이름에서 파생되며 각 서비스마다 고유합니다. [Windows 서비스 계정 및 사용 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 항목에서는 서비스별 SID에 대해 설명하며 **Windows 권한 및 권리**섹션에 이름을 제공합니다. 파일 위치에 대한 액세스 권한을 할당해야 하는 서비스별 SID입니다.  
  
## <a name="to-grant-file-system-permission-to-the-per-service-sid"></a>서비스별 SID에 파일 시스템 권한을 부여하려면  
  
1.  Windows 탐색기를 사용하여 데이터베이스 파일이 저장된 파일 시스템 위치로 이동합니다. 파일 시스템 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **보안** 탭에서 **편집**을 클릭한 다음 **추가**를 클릭합니다.  
  
3.  **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 위치 목록 맨 위에 있는 **위치**를 클릭하고 컴퓨터 이름을 선택한 다음 **확인**을 클릭합니다.  
  
4.  **선택할 개체 이름을 입력하세요.** 상자에 온라인 설명서 항목 [**Windows 서비스 계정 및 권한 구성**](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)에 나열된 서비스별 SID 이름을 입력합니다. ( [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스별 SID 이름의 경우 기본 인스턴스에 대해 **NT SERVICE\MSSQLSERVER** 를 사용하거나 명명된 인스턴스에 대해 **NT SERVICE\MSSQL$InstanceName** 을 사용합니다.)  
  
5.  **이름 확인** 을 클릭하여 항목의 유효성을 검사합니다. 유효성 검사가 실패하는 경우 이름을 찾을 수 없음이 표시될 수 있습니다. **확인**을 클릭하면 **여러 이름 찾음** 대화 상자가 표시됩니다. 이제 **MSSQLSERVER** 또는 **NT SERVICE\MSSQL$InstanceName**의 서비스별 SID 이름을 선택한 다음 **확인**을 클릭합니다.  **확인** 을 다시 클릭하여 **사용 권한** 대화 상자로 돌아갑니다.   
6.  **그룹 또는 사용자** 이름 상자에서 서비스별 SID 이름을 선택한 다음 \<이름>에 대한 **권한** 상자에서 **모든 권한**에 대한 **허용** 확인란을 선택합니다.  
  
7. **적용**을 클릭한 다음 **확인** 을 두 번 클릭하여 종료합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 서비스 관리](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [시스템 데이터베이스 이동](../../relational-databases/databases/move-system-databases.md)   
 [사용자 데이터베이스 이동](../../relational-databases/databases/move-user-databases.md)  
  
  
