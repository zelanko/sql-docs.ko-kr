---
title: 가져오기 및 내보내기 (SSIS 서비스) 패키지 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8ee81709bb8f0c9b30ab528d78a21b4ff72c1eed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183488"
---
# <a name="import-and-export-packages-ssis-service"></a>패키지 가져오기 및 내보내기(SSIS 서비스)
    
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 데이터베이스의 sysssispackages 테이블 또는 파일 시스템에 패키지를 저장할 수 있습니다.  
  
 패키지 저장소는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서 모니터링 및 관리하는 논리 저장소이며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스의 구성 파일에 지정된 msdb 데이터베이스 및 파일 시스템 폴더를 포함할 수 있습니다.  
  
 다음 유형의 저장소 간에 패키지를 가져오고 내보낼 수 있습니다.  
  
-   파일 시스템 내의 파일 시스템 폴더  
  
-   SSIS 패키지 저장소 내 폴더. 두 기본 폴더의 이름은 각각 File System 및 MSDB입니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 데이터베이스  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 통해 패키지를 가져오고 내보낼 수 있으며 이렇게 하면 패키지의 위치 및 저장소 형식을 변경 합니다. 가져오기 및 내보내기 기능을 사용하여 파일 시스템, 패키지 저장소 또는 msdb 데이터베이스에 패키지를 추가할 수 있으며 하나의 저장소 형식에서 다른 저장소 형식으로 패키지를 복사할 수 있습니다. 예를 들어 msdb에 저장된 패키지를 파일 시스템으로 복사할 수 있으며 반대의 경우도 가능합니다.  
  
 **dtutil** 명령 프롬프트 유틸리티(dtutil.exe)를 사용하여 패키지를 다른 형식으로 복사할 수 있습니다. 자세한 내용은 [dtutil Utility](dtutil-utility.md)를 참조하세요.  
  
## <a name="to-import-or-export-a-package"></a>패키지를 가져오거나 내보내려면  
  
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 일부인 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]와의 이전 버전 호환성을 위해 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 패키지를 관리하는 방법은 [Integration Services&#40;SSIS&#41; 서버](catalog/integration-services-ssis-server-and-catalog.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지는 다음과 같은 위치에서 가져오거나 내보낼 수 있습니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스, 파일 시스템 또는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지를 가져올 수 있습니다. 가져온 패키지는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 나 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소의 폴더에 저장됩니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스, 파일 시스템 또는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지를 다른 저장소 형식 또는 위치로 내보낼 수 있습니다.  
  
 그러나 버전이 다른 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]간에 패키지를 가져오거나 내보내는 경우 다음과 같은 몇 가지 제한 사항이 있습니다.  
  
-   [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]인스턴스에서는 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]인스턴스에서 패키지를 가져올 수만 있고 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]로 패키지를 내보낼 수는 없습니다.  
  
-   [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]인스턴스에서는 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]인스턴스에서 패키지를 가져오거나 인스턴스로 패키지를 내보낼 수 없습니다.  
  
 다음 절차에서는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 사용하여 패키지를 가져오거나 내보내는 방법에 대해 설명합니다.  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 패키지 가져오려면  
  
1.  **시작**을 클릭하고 **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 다음 옵션을 설정합니다.  
  
    -   **서버 유형** 상자에서 **Integration Services**를 선택합니다.  
  
    -   **서버 이름** 상자에 서버 이름을 입력하거나 **\<더 찾아보기…>** 를 클릭하여 사용할 서버를 찾습니다.  
  
3.  개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기**를 클릭합니다.  
  
4.  개체 탐색기에서 **저장된 패키지** 폴더를 확장합니다.  
  
5.  하위 폴더를 확장하여 패키지를 가져오려는 폴더를 찾습니다.  
  
6.  폴더를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 클릭한 다음 다음 중 하나를 수행합니다.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에서 가져오려면 **SQL Server** 옵션을 선택한 후 서버를 지정하고 인증 모드를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 선택한 경우 사용자 이름과 암호를 제공합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하고 가져올 패키지를 선택한 후 **확인**을 클릭합니다.  
  
    -   파일 시스템에서 가져오려면 **파일 시스템** 옵션을 선택합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하고 가져올 패키지를 선택한 후 **열기**를 클릭합니다.  
  
    -   [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소에서 가져오려면 **SSIS 패키지 저장소** 옵션을 선택하고 서버를 지정합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하고 가져올 패키지를 선택한 후 **확인**을 클릭합니다.  
  
7.  선택적으로 패키지 이름을 업데이트합니다.  
  
8.  패키지의 보호 수준을 업데이트하려면 찾아보기 단추 **(…)** 를 클릭하고 **패키지 보호 수준** 대화 상자를 사용하여 다른 보호 수준을 선택합니다. **암호로 중요한 데이터 암호화** 또는 **암호로 모든 데이터 암호화** 옵션을 선택한 경우 암호를 입력하고 확인합니다.  
  
9. **확인** 을 클릭하여 가져오기를 완료합니다.  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 패키지 내보내려면  
  
1.  **시작**을 클릭하고 **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 다음 옵션을 설정합니다.  
  
    -   **서버 유형** 상자에서 **Integration Services**를 선택합니다.  
  
    -   **서버 이름** 상자에 서버 이름을 입력하거나 **\<더 찾아보기…>** 를 클릭하여 사용할 서버를 찾습니다.  
  
3.  개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기**를 클릭합니다.  
  
4.  개체 탐색기에서 **저장된 패키지** 폴더를 확장합니다.  
  
5.  하위 폴더를 확장하고 내보내려는 패키지를 찾습니다.  
  
6.  패키지를 마우스 오른쪽 단추로 클릭하고 **내보내기**를 클릭한 후 다음 중 하나를 수행합니다.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스를 내보내려면 **SQL Server** 옵션을 선택한 후 서버를 지정하고 인증 모드를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 선택한 경우 사용자 이름과 암호를 제공합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하고 **SSIS 패키지** 폴더를 확장하여 패키지를 저장하려는 폴더를 찾습니다. 선택적으로 패키지의 기본 이름을 업데이트한 후 **확인**을 클릭합니다.  
  
    -   파일 시스템으로 내보내려면 **파일 시스템** 옵션을 선택합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하여 패키지를 내보내려는 폴더를 찾고, 패키지 파일의 이름을 입력한 후 **저장**을 클릭합니다.  
  
    -   [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소로 내보내려면 **SSIS 패키지 저장소** 옵션을 선택하고 서버를 지정합니다.  
  
         찾아보기 단추 **(…)** 를 클릭하고 **SSIS 패키지** 폴더를 확장하여 패키지를 저장하려는 폴더를 선택합니다. 선택적으로 **패키지 이름** 입력란에 패키지의 새 이름을 입력합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  패키지의 보호 수준을 업데이트하려면 찾아보기 단추 **(…)** 를 클릭하고 **패키지 보호 수준** 대화 상자를 사용하여 다른 보호 수준을 선택합니다. **암호로 중요한 데이터 암호화** 또는 **암호로 모든 데이터 암호화** 옵션을 선택한 경우 암호를 입력하고 확인합니다.  
  
8.  **확인** 을 클릭하여 내보내기를 완료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [관리 패키지 &#40;SSIS 서비스&#41;](service/package-management-ssis-service.md)  
  
  