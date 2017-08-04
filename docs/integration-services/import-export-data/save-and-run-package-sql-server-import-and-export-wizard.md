---
title: "저장 한 패키지 (SQL Server 가져오기 및 내보내기 마법사)를 실행 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 40b8677cddf363e8789a2fc15b1c2aab5f49f58c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>저장 하 고 실행할 패키지 (SQL Server 가져오기 및 내보내기 마법사)
  데이터 원본 및 대상을 지정하고 구성하고 나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **패키지 저장 및 실행**을 표시합니다. 이 페이지에서는 복사 작업을 즉시 실행할지 여부를 지정합니다. 구성에 따라 수도 있습니다으로 설정을 저장할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 패키지 사용자 지정 하 고 나중에 다시 사용 합니다.
  
**패키지란?** 마법사에서는 SSIS(SQL Server Integration Services)를 사용하여 데이터를 복사합니다. SSIS에서 기본 단위는 패키지입니다. 마법사는 사용자가 마법사 페이지를 진행하고 옵션을 지정하면 메모리 내에 SSIS 패키지를 만듭니다.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>패키지 저장 및 실행 페이지의 스크린샷  
다음 스크린샷은 마법사의 **패키지 저장 및 실행** 페이지입니다. 
   
![저장 하 고 패키지 페이지 가져오기 및 내보내기 마법사의 실행](../../integration-services/import-export-data/media/save-and-run.png "저장 하 고 패키지 가져오기 및 내보내기 마법사 페이지를 실행 합니다.") 
  
## <a name="run-and-save-the-package"></a>패키지 실행 및 저장 
 계속하려면 다음 두 옵션 중 하나 이상을 선택해야 합니다.  
  
 **Run immediately**  
 데이터 가져오기 및 내보내기 즉시 하려면이 옵션을 선택 합니다. 기본적으로이 확인란을 선택 하 고 작업을 즉시 실행 됩니다.
  
 **SSIS 패키지 저장**  
 SSIS 패키지로 설정을 저장 합니다. 나중에 필요에 따라 패키지를 사용자 지정하고 다시 실행할 수 있습니다. 패키지 저장을 선택하는 경우 다음 페이지 **SSIS 패키지 저장**에 추가 옵션이 있습니다.
 
패키지를 저장하는 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 이상이 설치된 경우에만 사용할 수 있습니다.   
  
> [!NOTE]
> 마법사를 완료 하 하지만 작업을 실행 한 중지 되기 전에 작업 실행이 완료 될 경우 패키지는 저장 되지를 선택한 경우에는 **i S 패키지 저장** 확인란 합니다.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Visual Studio에서 마법사를 시작 하는 경우
SQL Server 데이터 도구 (SSDT)와 Visual Studio에서 Integration Services 프로젝트에서 마법사를 시작:
-   수 없는 **실행** 마법사를 종료 될 때까지 패키지 합니다. 그런 다음 Visual Studio에서 패키지를 실행할 수 있습니다.
-   마법사 **저장** 마법사를 시작한 Integration Services 프로젝트에 패키지 합니다.

## <a name="specify-options-for-saving-the-package"></a>패키지 저장 옵션 지정
**SQL Server**  
 SQL Server에 패키지를 저장 하려면이 옵션을 선택는 **msdb** 여기에 데이터베이스는 **sysssispackages** 테이블입니다.
 
> [!IMPORTANT]
> 이 옵션은 SSIS 카탈로그 데이터베이스(SSISDB)에 패키지를 저장하지 않습니다.  

 대상 서버를 선택하고 다음 페이지 **SSIS 패키지 저장**에서 서버에 연결할 자격 증명을 제공합니다. 자세한 내용은 [SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
 **파일 시스템**  
 파일으로 패키지를 저장 하려면이 옵션을 선택는 **.dtsx** 확장 합니다.  
  
 다음 페이지 **SSIS 패키지 저장**에서 패키지에 대한 파일 이름과 대상 폴더를 선택합니다. 자세한 내용은 [SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)을 참조하세요.  
 
 ## <a name="specify-the-package-protection-level"></a>패키지 보호 수준 지정
 **패키지 보호 수준**  
 패키지의 데이터를 보호하려면 목록에서 보호 수준을 선택합니다.  
  
 보호 수준은 보호 방법(암호 또는 사용자 키)과 패키지 보호의 범위를 결정합니다. 보호에는 모든 데이터를 포함시키거나 중요한 데이터만 포함시킬 수 있습니다. 사용 가능한 옵션에 대한 자세한 내용은 [패키지의 중요한 데이터에 대한 액세스 제어](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)를 참조하세요.  
  
 **암호**  
 암호를 입력합니다.  
  
 **암호 다시 입력**  
 암호를 다시 입력합니다.  
  
> [!NOTE]
> 암호 옵션을 사용할 수 있는 경우에만 지정는 **패키지 보호 수준** 필요로 하는 암호-즉, 지정 하는 경우 **암호로 중요 한 데이터 암호화** 또는 **암호로 모든 데이터를 암호화**합니다.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>패키지 저장을 위한 두 페이지의 옵션 정보  
 **패키지 저장 및 실행** 페이지는 SSIS 패키지를 저장하기 위한 옵션을 선택하는 두 페이지 중 하나입니다.  
  
-   현재 페이지에서 패키지를 SQL Server에 저장할지 또는 파일로 저장할지 선택합니다. 저장된 패키지의 보안 설정을 선택할 수도 있습니다.  
  
-   다음으로 **SSIS 패키지 저장** 페이지에서 패키지 이름 및 저장 위치에 대한 자세한 정보를 제공합니다. 자세한 내용은 [SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
 이러한 옵션은 이 페이지에서 **SSIS 패키지 저장** 옵션을 선택하는 경우에만 사용할 수 있습니다.  
  
## <a name="whats-next"></a>다음 단계  
 복사 작업을 즉시 실행할지 여부와 패키지 저장 여부를 지정한 후 다음 페이지는 선택한 옵션에 따라 다릅니다.  
  
-   패키지를 저장하지 않고 즉시 실행하는 옵션을 선택한 경우 다음 페이지는 **마법사 완료**입니다. 이 페이지에서는 마법사에서 선택한 내용을 검토하고 복사 작업을 시작합니다. 자세한 내용은 [마법사 완료](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
-   패키지를 저장하는 옵션을 선택한 경우 다음 페이지는 **SSIS 패키지 저장**입니다. 이 페이지에서는 패키지 저장 옵션을 추가로 지정할 수 있습니다. (패키지를 저장한 후 다음 페이지는 **마법사 완료**입니다.) 자세한 내용은 [SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[패키지 저장](../../integration-services/save-packages.md)  
[Integration Services(SSIS) 패키지 실행](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[이 간단한 예제 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  


