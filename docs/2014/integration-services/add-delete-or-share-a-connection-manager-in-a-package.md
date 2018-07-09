---
title: 추가, 삭제 또는 공유 패키지에서 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
caps.latest.revision: 56
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1f726306b53f896176de23726fc17cdc3a6b2d53
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277409"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>패키지에서 연결 관리자 추가, 삭제 또는 공유
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 관계형 데이터베이스와 같은 다른 데이터 원본에 연결 하기 위한 다양 한 연결 관리자를 포함 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스 및 CSV 및 XML 형식의 파일입니다. 패키지 수준 또는 프로젝트 수준에서 연결 관리자를 만들 수 있습니다. 프로젝트 수준에서 만든 연결 관리자는 프로젝트의 모든 패키지에 사용할 수 있습니다. 반면, 패키지 수준에서 만든 연결 관리자는 해당하는 특정 패키지에 사용할 수 있습니다.  
  
 데이터 원본 대신 프로젝트 수준에서 만든 연결 관리자를 사용하여 원본에 대한 연결을 공유합니다. 프로젝트 수준에서 연결 관리자를 추가하려면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 프로젝트 배포 모델을 사용해야 합니다. 프로젝트가 이 모델을 사용하도록 구성된 경우 **연결 관리자** 폴더가 **솔루션 탐색기**에 표시되고 **데이터 원본** 폴더가 **솔루션 탐색기**에서 제거됩니다.  
  
> [!NOTE]  
>  패키지에 데이터 원본을 사용하려면 프로젝트를 패키지 배포 모델로 변환해야 합니다.  
>   
>  두 가지 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하십시오. 프로젝트를 프로젝트 배포 모델로 변환하는 방법은 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)를 참조하십시오.  
  
 다음 절차는 모든 유형의 연결 관리자에 적용되며 다음과 같은 태스크를 수행하는 방법에 대해 설명합니다.  
  
-   [패키지를 만들 때 연결 관리자를 추가 하려면](#wizard)  
  
-   [기존 패키지에는 연결 관리자를 추가 하려면](#package)  
  
-   [프로젝트 수준 연결 관리자를 추가 하려면](#project)  
  
-   [연결 관리자 속성에 대 한 매개 변수를 만들려면](#parameter)  
  
-   [패키지에서 연결 관리자를 삭제 하려면](#DeletePackageLevel)  
  
-   [공유 연결 관리자 (프로젝트 수준 연결 관리자)를 삭제 하려면](#DeleteProjectLevel)  
  
##  <a name="wizard"></a> 패키지를 만들 때 연결 관리자를 추가 하려면  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 사용합니다.  
  
     이 마법사는 연결 관리자를 만들고 구성하는 것 외에도 연결 관리자를 사용하는 원본과 대상을 만들고 구성하는 것을 도와줍니다. 자세한 내용은 [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)을 참조하세요.  
  
##  <a name="package"></a> 기존 패키지에는 연결 관리자를 추가 하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭, **데이터 흐름** 탭 또는 **이벤트 처리기** 탭을 클릭하여 **연결 관리자** 영역을 표시합니다.  
  
4.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 다음 중 하나를 수행합니다.  
  
    -   패키지에 추가할 연결 관리자 유형을 클릭합니다.  
  
         —또는—  
  
    -   추가할 유형이 목록에 없는 경우 **새 연결** 을 클릭하여 **SSIS 연결 관리자 추가** 대화 상자를 열고 연결 관리자 유형을 선택한 다음 **확인**을 클릭합니다.  
  
     선택한 연결 관리자 유형의 사용자 지정 대화 상자가 열립니다. 사용 가능한 옵션 및 연결 관리자 유형에 대한 자세한 내용은 다음 옵션 표를 참조하십시오.  
  
    |ODBC 대상 편집기|변수|  
    |------------------------|-------------|  
    |[ADO 연결 관리자](connection-manager/ado-connection-manager.md)|[OLE DB 연결 관리자 구성](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 연결 관리자](connection-manager/ado-net-connection-manager.md)|[ADO.NET 연결 관리자 구성](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 연결 관리자](connection-manager/analysis-services-connection-manager.md)|[Analysis Services 연결 관리자 추가 대화 상자 UI 참조](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 연결 관리자](connection-manager/excel-connection-manager.md)|[Excel 연결 관리자 편집기](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[파일 연결 관리자](connection-manager/file-connection-manager.md)|[파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[다중 파일 연결 관리자](connection-manager/multiple-files-connection-manager.md)|[파일 연결 관리자 추가 대화 상자 UI 참조](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[플랫 파일 연결 관리자](connection-manager/flat-file-connection-manager.md)|[플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[다중 플랫 파일 연결 관리자](connection-manager/multiple-flat-files-connection-manager.md)|[다중 플랫 파일 연결 관리자 편집기 &#40;일반 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기 &#40;열 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기 &#40;고급 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기 &#40;페이지를 미리 보기&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 연결 관리자](connection-manager/ftp-connection-manager.md)|[FTP 연결 관리자 편집기](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 연결 관리자](connection-manager/http-connection-manager.md)|[HTTP 연결 관리자 편집기 &#40;Server 페이지&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 연결 관리자 편집기 &#40;프록시 페이지&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 연결 관리자](connection-manager/msmq-connection-manager.md)|[MSMQ 연결 관리자 편집기](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 연결 관리자](connection-manager/odbc-connection-manager.md)|[ODBC 연결 관리자 UI 참조](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md)|[OLE DB 연결 관리자 구성](configure-ole-db-connection-manager.md)|  
    |[SMO 연결 관리자](connection-manager/smo-connection-manager.md)|[SMO 연결 관리자 편집기](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 연결 관리자](connection-manager/smtp-connection-manager.md)|[SMTP 연결 관리자 편집기](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 연결 관리자](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 연결 관리자 편집기 &#40;연결 페이지&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 연결 관리자 편집기 &#40;모든 페이지&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 연결 관리자](connection-manager/wmi-connection-manager.md)|[WMI 연결 관리자 편집기](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     **연결 관리자** 영역에 추가된 연결 관리자가 나열됩니다.  
  
5.  필요에 따라 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭하여 연결 관리자의 기본 이름을 수정합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
##  <a name="project"></a> 프로젝트 수준 연결 관리자를 추가 하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 **연결 관리자**를 마우스 오른쪽 단추로 클릭하고 **새 연결 관리자**를 클릭합니다.  
  
3.  **SSIS 연결 관리자 추가** 대화 상자에서 연결 관리자 유형을 선택한 다음 **추가**를 클릭합니다.  
  
     선택한 연결 관리자 유형의 사용자 지정 대화 상자가 열립니다. 사용 가능한 옵션 및 연결 관리자 유형에 대한 자세한 내용은 다음 옵션 표를 참조하십시오.  
  
    |ODBC 대상 편집기|변수|  
    |------------------------|-------------|  
    |[ADO 연결 관리자](connection-manager/ado-connection-manager.md)|[OLE DB 연결 관리자 구성](configure-ole-db-connection-manager.md)|  
    |[ADO.NET 연결 관리자](connection-manager/ado-net-connection-manager.md)|[ADO.NET 연결 관리자 구성](configure-ado-net-connection-manager.md)|  
    |[Analysis Services 연결 관리자](connection-manager/analysis-services-connection-manager.md)|[Analysis Services 연결 관리자 추가 대화 상자 UI 참조](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 연결 관리자](connection-manager/excel-connection-manager.md)|[Excel 연결 관리자 편집기](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[파일 연결 관리자](connection-manager/file-connection-manager.md)|[파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[다중 파일 연결 관리자](connection-manager/multiple-files-connection-manager.md)|[파일 연결 관리자 추가 대화 상자 UI 참조](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[플랫 파일 연결 관리자](connection-manager/flat-file-connection-manager.md)|[플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[다중 플랫 파일 연결 관리자](connection-manager/multiple-flat-files-connection-manager.md)|[다중 플랫 파일 연결 관리자 편집기 &#40;일반 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기 &#40;열 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기 &#40;고급 페이지&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [다중 플랫 파일 연결 관리자 편집기 &#40;페이지를 미리 보기&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 연결 관리자](connection-manager/ftp-connection-manager.md)|[FTP 연결 관리자 편집기](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[HTTP 연결 관리자](connection-manager/http-connection-manager.md)|[HTTP 연결 관리자 편집기 &#40;Server 페이지&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 연결 관리자 편집기 &#40;프록시 페이지&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 연결 관리자](connection-manager/msmq-connection-manager.md)|[MSMQ 연결 관리자 편집기](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[ODBC 연결 관리자](connection-manager/odbc-connection-manager.md)|[ODBC 연결 관리자 UI 참조](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md)|[OLE DB 연결 관리자 구성](configure-ole-db-connection-manager.md)|  
    |[SMO 연결 관리자](connection-manager/smo-connection-manager.md)|[SMO 연결 관리자 편집기](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[SMTP 연결 관리자](connection-manager/smtp-connection-manager.md)|[SMTP 연결 관리자 편집기](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 연결 관리자](connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 연결 관리자 편집기 &#40;연결 페이지&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 연결 관리자 편집기 &#40;모든 페이지&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 연결 관리자](connection-manager/wmi-connection-manager.md)|[WMI 연결 관리자 편집기](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     추가한 연결 관리자가 **솔루션 탐색기** 의 **연결 관리자**노드에 표시됩니다. 이 연결 관리자는 프로젝트의 모든 패키지에 대한 **SSIS 디자이너** 창의 **연결 관리자** 탭에도 나타납니다. 이 프로젝트 수준 연결 관리자를 패키지 수준 연결 관리자와 구별하기 위해 이 탭의 연결 관리자 이름에는 **(프로젝트)** 라는 접두사가 붙습니다.  
  
4.  선택적으로 **SSIS 디자이너** 창의 **연결 관리자** 탭 또는 **연결 관리자** 노드 아래에 있는 **솔루션 탐색기** 창에서 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 다음 연결 관리자의 기본 이름을 수정합니다.  
  
    > [!NOTE]  
    >  **SSIS 디자이너** 창의 **연결 관리자** 탭에서는 연결 관리자 이름의 **(프로젝트)** 접두사를 덮어쓸 수 없습니다. 이것은 의도적인 것입니다.  
  
##  <a name="parameter"></a> 연결 관리자 속성에 대 한 매개 변수를 만들려면  
  
1.  **연결 관리자** 영역에서 매개 변수를 만들려는 연결 관리자를 마우스 오른쪽 단추로 클릭한 후 **매개 변수화**를 클릭합니다.  
  
2.  **매개 변수화** 대화 상자에서 매개 변수 설정을 구성합니다. 자세한 내용은 [Parameterize Dialog Box](../../2014/integration-services/parameterize-dialog-box.md)을 참조하세요.  
  
##  <a name="DeletePackageLevel"></a> 패키지에서 연결 관리자를 삭제 하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭, **데이터 흐름** 탭 또는 **이벤트 처리기** 탭을 클릭하여 **연결 관리자** 영역을 표시합니다.  
  
4.  삭제할 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
     SQL 실행 태스크 또는 OLE DB 원본과 같은 패키지 요소가 사용하는 연결 관리자를 삭제하면 다음과 같은 결과가 나타납니다.  
  
    -   삭제된 연결 관리자를 사용하던 패키지 요소에 오류 아이콘이 나타납니다.  
  
    -   패키지의 유효성 검사가 실패합니다.  
  
    -   패키지를 실행할 수 없습니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
##  <a name="DeleteProjectLevel"></a> 공유 연결 관리자 (프로젝트 수준 연결 관리자)를 삭제 하려면  
  
1.  프로젝트 수준 연결 관리자를 삭제하려면 **솔루션 탐색기** 창의 **연결 관리자** 노드 아래에 있는 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에 다음과 같은 경고 메시지가 표시됩니다.  
  
    > [!WARNING]  
    >  프로젝트 연결 관리자를 삭제하면 연결 관리자를 사용하는 패키지가 실행되지 않을 수 있습니다. 이 동작은 실행 취소할 수 없습니다. 연결 관리자를 삭제하시겠습니까?  
  
2.  확인을 클릭하여 연결 관리자를 삭제하거나 취소를 클릭하여 연결 관리자를 그대로 둡니다.  
  
    > [!NOTE]  
    >  프로젝트의 특정 패키지에 대해 열려 있는 **SSIS 디자이너** 창의 **연결 관리자** 탭에서 프로젝트 수준 연결 관리자를 삭제할 수도 있습니다. 탭에서 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭하면 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 연결](connection-manager/integration-services-ssis-connections.md)   
 [연결 관리자의 속성 설정](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
