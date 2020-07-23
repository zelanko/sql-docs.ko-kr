---
title: SSIS 패키지 저장(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f354643c156024eeee1db53ad366dfb63f55859
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914384"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>SSIS 패키지 저장(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **패키지 저장 및 실행** 페이지에서 SSIS(SQL Server Integration Services) 패키지로 설정을 저장하도록 지정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **SSIS 패키지 저장**을 표시합니다. 이 페이지에서 마법사에서 만든 패키지를 저장하기 위한 추가 옵션을 지정합니다.  

**SSIS 패키지 저장** 페이지에 표시되는 옵션은 이전에 **패키지 저장 및 실행** 페이지에서 패키지를 SQL Server 또는 파일 시스템에 저장하도록 선택했는지에 따라 달라집니다. **패키지 저장 및 실행** 페이지를 다시 살펴보려면 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.
 
**패키지란?** 마법사에서는 SSIS(SQL Server Integration Services)를 사용하여 데이터를 복사합니다. SSIS에서 기본 단위는 패키지입니다. 마법사는 사용자가 마법사 페이지를 진행하고 옵션을 지정하면 메모리 내에 SSIS 패키지를 만듭니다.

## <a name="screen-shot---common-options"></a>스크린샷 - 일반 옵션
다음 스크린샷에서는 마법사의 **SSIS 패키지 저장** 페이지에 있는 첫 번째 부분을 보여 줍니다. 페이지의 나머지 부분에는 선택한 패키지 대상에 따라 달라지는 다양한 옵션이 있습니다.

![패키지 저장 - 일반 옵션](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>패키지에 대한 이름 및 설명 입력  
 **이름**  
 패키지에 사용할 고유 이름을 제공합니다.  
  
 **설명**  
 패키지에 대한 설명을 입력합니다. 해당 패키지의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **대상**  
 이전에 패키지에 대해 지정한 대상([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 파일 시스템). 다른 대상에 패키지를 저장하려는 경우 **패키지 저장 및 실행** 페이지로 돌아갑니다.

## <a name="screen-shot---save-the-package-in-sql-server"></a>스크린샷 - SQL Server에 패키지 저장

 다음 스크린샷에서는 **패키지 저장 및 실행** 페이지에서 **SQL Server** 옵션을 선택한 경우 마법사의 **SSIS 패키지 저장** 페이지를 보여 줍니다. 
  
![가져오기 및 내보내기 마법사의 SSIS 패키지 저장 페이지](../../integration-services/import-export-data/media/save-package2.png "가져오기 및 내보내기 마법사의 SSIS 패키지 저장 페이지")  

## <a name="options-to-specify-target--sql-server"></a>지정할 옵션(대상 = SQL Server) 

 > [!NOTE]
 > 마법사는 **msdb** 데이터베이스의 **sysssispackages** 테이블에 패키지를 저장합니다. 이 옵션은 SSISDB(SSIS 카탈로그 데이터베이스)에 패키지를 **저장하지 않습니다**.  
 
 **서버 이름**  
 대상 서버 이름을 선택하거나 입력합니다.  
   
 **Windows 인증 사용**  
Windows 통합 인증을 사용하여 서버에 연결합니다. 이 방법은 기본적으로 사용되는 인증 방법입니다.  
  
 **SQL Server 인증 사용**  
SQL Server 인증을 사용하여 서버에 연결합니다.  
  
 **사용자 이름**  
SQL Server 인증을 지정한 경우 사용자 이름을 입력합니다.  
  
 **암호**  
SQL Server 인증을 지정한 경우 암호를 입력합니다.  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>스크린샷 - 파일 시스템에 패키지 저장
 
다음 스크린샷에서는 **패키지 저장 및 실행** 페이지에서 **파일 시스템** 옵션을 선택한 경우 마법사의 **SSIS 패키지 저장** 페이지를 보여 줍니다. 
  
![가져오기 및 내보내기 마법사의 SSIS 패키지 저장 페이지](../../integration-services/import-export-data/media/save-package1.png "가져오기 및 내보내기 마법사의 SSIS 패키지 저장 페이지")  

## <a name="options-to-specify-target--file-system"></a>지정할 옵션(대상 = 파일 시스템)

 **파일 이름**  
 대상 파일의 경로와 파일 이름을 입력하거나 **찾아보기** 단추를 사용하여 대상을 선택합니다.  
  
> [!TIP]
> 대상 폴더를 입력하거나 검색하여 지정해야 합니다. 경로 없이 파일 이름만 입력하면 마법사에서 패키지를 저장하는 위치를 인식할 수 없습니다. 또한 마법사에서 파일을 저장할 수 있는 권한이 없는 위치에 패키지를 저장하려고 시도하고 오류가 발생할 수도 있습니다.  
>   
>  패키지 파일의 저장 위치를 기억해 두세요.  
  
 **찾아보기**  
 필요에 따라 **패키지 저장** 대화 상자에서 대상 파일의 경로를 찾아 선택합니다.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>패키지 저장을 위한 두 페이지의 옵션 정보  
 **SSIS 패키지 저장** 페이지는 SSIS 패키지를 저장하기 위한 옵션을 선택하는 두 페이지 중 하나입니다.  
  
-   이전 페이지인 **패키지 저장 및 실행**에서 패키지를 SQL Server에 저장할지 또는 파일로 저장할지 선택합니다. 저장된 패키지의 보안 설정을 선택할 수도 있습니다. **패키지 저장 및 실행** 페이지를 다시 살펴보려면 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
-   현재 페이지에서 패키지 이름 및 저장 위치에 대한 자세한 정보를 제공합니다.  
 
## <a name="run-the-saved-package-again-later"></a>나중에 저장된 패키지 다시 실행  
 나중에 저장된 패키지를 다시 실행하는 방법을 알아보려면 다음 항목 중 하나를 참조하세요.  
  
-   친숙한 사용자 인터페이스로 유틸리티 프로그램을 사용하여 패키지를 실행하려면 [패키지 유틸리티 실행&#40;DtExecUI&#41; UI 참조](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)를 참조하세요.  
  
-   명령줄 또는 배치 파일에서 패키지를 실행하려면 [dtexec 유틸리티](../../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
-   SQL Server의 **msdb** 데이터베이스에 패키지를 저장한 경우 Integration Services 서비스에 연결합니다. 그런 다음, SQL Server Management Studio의 개체 탐색기에서 **저장된 패키지 | MSDB**로 이동하고 패키지를 마우스 오른쪽 단추로 클릭한 다음 **패키지 실행**을 선택합니다.

-   파일 시스템에 패키지를 저장한 경우 개발 환경에서 패키지를 실행하려면 [Integration Services(SSIS) 패키지 실행](../../integration-services/packages/run-integration-services-ssis-packages.md) 을 참조하세요. 먼저 Integration Services 프로젝트에 패키지를 추가해야 열어서 실행할 수 있습니다.  

## <a name="customize-the-saved-package"></a>저장된 패키지 사용자 지정  
 저장된 패키지를 사용자 지정하는 방법을 알아보려면 [Integration Services&#40;SSIS&#41; 패키지](../../integration-services/integration-services-ssis-packages.md)를 참조하세요.  
  
## <a name="whats-next"></a>다음 단계  
 패키지 저장 옵션을 추가로 지정한 후 다음 페이지는 **마법사 완료**입니다. 이 페이지에서는 마법사에서 선택한 내용을 검토하고 작업을 시작합니다. 자세한 내용은 [마법사 완료](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)를 참조하세요.  
 
## <a name="see-also"></a>참고 항목  
[패키지 저장](../../integration-services/save-packages.md)  
[Integration Services(SSIS) 패키지 실행](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 
