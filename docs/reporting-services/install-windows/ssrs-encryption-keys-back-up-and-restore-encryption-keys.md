---
title: Reporting Services 암호화 키 백업 및 복원 | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backing up encryption keys [Reporting Services]
- restoring encryption keys [Reporting Services]
- encryption keys [Reporting Services]
- symmetric keys [Reporting Services]
ms.assetid: 6773d5df-03ef-4781-beb7-9f6825bac979
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: fa9eb1ee19e689fd34285c0ee3fb4dd2ba5095f7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005067"
---
# <a name="ssrs-encryption-keys---back-up-and-restore-encryption-keys"></a>SSRS 암호화 키 - 암호화 키 백업 및 복원
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  보고서 서버 구성의 중요한 부분은 중요한 정보의 암호화에 사용되는 대칭 키의 백업 복사본을 만드는 것입니다. 대칭 키의 백업 복사본은 여러 일상 작업에 필요하며 새 설치에서 기존 보고서 서버 데이터베이스를 다시 사용할 수 있도록 합니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드  
  
 다음 이벤트가 발생할 경우 암호화 키의 백업 복사본을 복원해야 합니다.  
  
-   보고서 서버 Windows 서비스 계정 이름 변경 또는 암호 다시 설정. Reporting Services 구성 관리자를 사용할 경우 서비스 계정 이름 변경 작업의 일부로 키가 백업됩니다.  
  
    > [!NOTE]
    > 암호를 다시 설정하는 것은 암호를 변경하는 것과 다릅니다. 암호를 다시 설정하려면 도메인 컨트롤러의 계정 정보를 덮어쓸 수 있는 권한이 있어야 합니다. 특정 암호를 잊어버리거나 알지 못할 경우 시스템 관리자가 암호를 다시 설정합니다. 대칭 키의 복원 작업은 암호를 다시 설정할 때만 필요합니다. 계정 정보를 주기적으로 변경할 경우에는 대칭 키를 다시 설정할 필요가 없습니다.  
  
-   보고서 서버를 호스팅하는 컴퓨터나 인스턴스 이름 바꾸기(보고서 서버 인스턴스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 기반으로 함)  
  
-   보고서 서버 설치 마이그레이션 또는 다른 보고서 서버 데이터베이스를 사용하도록 보고서 서버 구성  
  
-   하드웨어 오류로 인한 보고서 서버 설치 복구  
  
 대칭 키 복사본을 하나만 백업하면 됩니다. 보고서 서버 데이터베이스와 대칭 키 간에는 일 대 일 상관 관계가 있습니다. 따라서 대칭 키 복사본을 1개만 백업하면 되지만 스케일 아웃 배포 모델에서 여러 보고서 서버를 실행할 경우에는 키를 여러 번 복원해야 할 수 있습니다. 각 보고서 서버 인스턴스는 보고서 서버 데이터베이스의 데이터를 잠그거나 잠금을 해제하기 위해 대칭 키 복사본이 필요합니다.

 대칭 키를 백업하면 사용자가 지정한 파일에 키가 기록된 후 사용자가 제공한 암호를 사용하여 키가 스크램블됩니다. 대칭 키는 암호화되지 않은 상태로는 저장될 수 없으므로 디스크에 저장할 때 암호를 제공하여 키를 암호화해야 합니다. 파일이 생성되면 해당 파일을 안전한 위치에 저장하고 파일 잠금을 해제하는 데 사용되는 **암호를 기억해야** 합니다. 대칭 키를 백업하려면 다음과 같은 도구를 사용할 수 있습니다.  
  
 **기본 모드:** Reporting Services 구성 관리자 또는 **rskeymgmt** 유틸리티  
  
 **SharePoint 모드:** SharePoint 중앙 관리 페이지 또는 PowerShell  
  
##  <a name="bkmk_backup_sharepoint"></a> SharePoint 모드 보고서 서버 백업  
 SharePoint 모드 보고서 서버의 경우 PowerShell 명령을 사용하거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램용 관리 페이지를 사용할 수 있습니다. 자세한 내용은 [Reporting Services SharePoint 서비스 응용 프로그램 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)의 "키 관리" 섹션을 참조하세요.  
  
##  <a name="bkmk_backup_configuration_manager"></a> 암호화 키 백업 - Reporting Services 구성 관리자(기본 모드)  
  
1.  Reporting Services 구성 관리자를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다.  
  
2.  **암호화 키**를 클릭한 다음 **백업**을 선택합니다.  
  
3.  강력한 암호를 입력합니다.  
  
4.  저장된 키를 보관할 파일을 지정합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 해당 파일에 .snk 파일 확장명을 붙입니다. 보고서 서버와는 분리되도록 해당 파일을 디스크에 저장하세요.  
  
5.  **확인**을 선택합니다.  
  
###  <a name="bkmk_backup_rskeymgmt"></a> 암호화 키 백업 - rskeymgmt(기본 모드)  
  
1.  보고서 서버를 호스팅하는 컴퓨터에서 **rskeymgmt.exe** 를 로컬로 실행합니다. **-e** 추출 인수를 사용하여 키를 복사하고 파일 이름을 제공하고 암호를 지정해야 합니다. 다음은 인수 지정 예입니다.  
  
    ```  
    rskeymgmt -e -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="restore-encryption-keys"></a>암호화 키 복원  
 대칭 키를 복원하면 보고서 서버 데이터베이스에 저장되어 있는 기존 대칭 키를 덮어쓰게 됩니다. 암호화 키를 복원하면 사용할 수 없는 키가 이전에 디스크에 저장한 복사본으로 바뀝니다. 암호화 키를 복원하면 다음 동작이 수행됩니다.  
  
-   암호로 보호된 백업 파일에서 대칭 키가 열립니다.  
  
-   보고서 서버 Windows 서비스의 공개 키를 사용하여 대칭 키가 암호화됩니다.  
  
-   암호화된 대칭 키가 보고서 서버 데이터베이스에 저장됩니다.  
  
-   이전에 저장한 대칭 키 데이터(예: 이전 배포의 보고서 서버 데이터베이스에 이미 있던 키 정보)가 삭제됩니다.  
  
 암호화 키를 복원하려면 파일에 암호화 키 복사본이 있어야 합니다. 또한 저장된 파일의 잠금을 해제할 암호를 알아야 합니다. 키와 암호가 있으면 Reporting Services 구성 도구나 **rskeymgmt** 유틸리티를 실행하여 키를 복원할 수 있습니다. 대칭 키는 보고서 서버 데이터베이스에 현재 저장되어 있는 암호화된 데이터를 잠그거나 잠금을 해제하는 키와 같아야 합니다. 유효하지 않은 복사본을 복원하면 보고서 서버에서 보고서 서버 데이터베이스에 현재 저장되어 있는 암호화된 데이터에 액세스할 수 없습니다. 이 경우 유효한 키를 복원할 수 없으면 암호화된 값을 모두 삭제해야 합니다. 백업 복사본이 없는 경우와 같이 여타의 이유로 암호화 키를 복원할 수 없으면 기존 키 및 암호화된 내용을 삭제해야 합니다. 자세한 내용은 [암호화 키 삭제 및 다시 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)를 참조하세요. 대칭 키를 만드는 방법은 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)를 참조하세요.  
  
###  <a name="bkmk_restore_configuration_manager"></a> 암호화 키 복원 - Reporting Services 구성 관리자(기본 모드)  
  
1.  Reporting Services 구성 관리자를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다.  
  
2.  암호화 키 페이지에서 **복원**을 선택합니다.  
  
3.  백업 복사본이 들어 있는 .snk 파일을 선택합니다.  
  
4.  파일의 잠금을 해제하는 암호를 입력합니다.  
  
5.  **확인**을 선택합니다. 
  
###  <a name="bkmk_restore_rskeymgmt"></a> 암호화 키 복원 - rskeymgmt(기본 모드)  
  
1.  보고서 서버를 호스팅하는 컴퓨터에서 **rskeymgmt.exe** 를 로컬로 실행합니다. **-a** 인수를 사용하여 키를 복원합니다. 정규화된 파일 이름을 제공하고 암호를 지정해야 합니다. 다음은 인수 지정 예입니다.  
  
    ```  
    rskeymgmt -a -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
