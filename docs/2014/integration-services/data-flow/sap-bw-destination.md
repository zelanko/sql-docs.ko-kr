---
title: SAP BW 대상 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a612ed91-b89b-4173-a0b1-0bce381e1e28
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1cac8403327ecf3888439290554f059bb00bce2c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375218"
---
# <a name="sap-bw-destination"></a>SAP BW 대상
  SAP BW 대상은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 대상 구성 요소입니다. 따라서 SAP BW 대상은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 SAP Netweaver BW 버전 7 시스템으로 데이터를 로드합니다.  
  
 이 대상에는 하나의 입력과 하나의 오류 출력이 포함됩니다.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 SAP BW 대상을 사용하려면 다음 태스크를 수행해야 합니다.  
  
-   [SAP Netweaver BW 개체 준비](#bkmk_Prepare_Objects)  
  
-   [SAP Netweaver BW 시스템에 연결](#bkmk_Connect_Database)  
  
-   [SAP BW 대상 구성](#bkmk_Configure_Destination)  
  
##  <a name="bkmk_Prepare_Objects"></a> 대상에 필요한 SAP Netweaver BW 개체 준비  
 SAP BW 대상이 작동하려면 특정 개체가 SAP Netweaver BW 시스템에 있어야 합니다. 이러한 개체가 없는 경우 다음 단계를 수행하여 SAP Netweaver BW 시스템에서 이러한 개체를 만들고 구성해야 합니다.  
  
> [!NOTE]  
>  이러한 개체와 구성 단계에 대한 자세한 내용은 SAP Netweaver BW 설명서를 참조하십시오.  
  
1.  새 원본 시스템을 만듭니다.  
  
    1.  **"Third Party/Staging BAPIs"** 유형을 선택합니다.  
  
    2.  **Communication Type with Target System**(대상 시스템과 통신 유형)에서 **Non-Unicode (Inactive MDMP Settings)**(비유니코드(비활성 MDMP 설정))를 선택합니다.  
  
    3.  적절한 프로그램 ID를 할당합니다.  
  
2.  InfoSource에 원본 시스템을 할당합니다.  
  
3.  InfoPackage를 만듭니다.  
  
     InfoPackage는 SAP BW 대상에 필요한 가장 중요한 개체입니다.  
  
 SAP Netweaver BW 시스템으로의 데이터 로드를 지원하는 데 필요한 InfoObject, InfoCube, InfoSource 및 InfoPackage를 추가로 만들 수도 있습니다.  
  
##  <a name="bkmk_Connect_Database"></a> SAP Netweaver BW 시스템에 연결  
 SAP Netweaver BW 버전 7 시스템에 연결하기 위해 SAP BW 대상은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 패키지의 일부인 SAP BW 연결 관리자를 사용합니다. SAP BW 연결 관리자는 SAP BW 대상이 사용할 수 있는 유일한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결 관리자입니다.  
  
 SAP BW 연결 관리자에 대한 자세한 내용은 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)를 참조하십시오.  
  
##  <a name="bkmk_Configure_Destination"></a> SAP BW 대상 구성  
 다음과 같은 방법으로 SAP BW 대상을 구성할 수 있습니다.  
  
-   데이터를 로드하는 데 사용할 InfoPackage를 조회하고 선택합니다.  
  
-   데이터 흐름의 각 열을 InfoPackage의 적절한 InfoObject에 매핑합니다.  
  
-   `PackageSize` 속성을 구성하여 한 번에 전송될 데이터 행 수를 지정합니다.  
  
-   SAP Netweaver BW 시스템에서 데이터 로드가 완료될 때까지 대기하도록 선택합니다.  
  
-   InfoPackage를 트리거하지 않고 SAP Netweaver BW 시스템에서 데이터 로드를 시작했다는 알림을 받을 때까지 대기하도록 선택합니다.  
  
-   데이터 로드가 완료된 후 필요에 따라 다른 프로세스 체인을 트리거합니다.  
  
-   필요에 따라 대상에 필요한 SAP Netweaver BW 개체를 만듭니다. 여기에는 InfoObject, InfoCube, InfoSource 및 InfoPackage를 만드는 작업이 포함됩니다.  
  
-   선택한 옵션을 사용하여 데이터 로드를 테스트합니다.  
  
 대상에 의한 RFC 함수 호출의 로깅을 사용하도록 설정할 수도 있습니다. 이 로깅은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용하도록 설정할 수 있는 선택적 로깅과 별개입니다. 대상이 사용할 SAP BW 연결 관리자를 구성할 때 RFC 함수 호출의 로깅을 사용하도록 설정합니다. SAP BW 연결 관리자를 구성하는 방법은 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)를 참조하십시오.  
  
 대상을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 SAP BW 연결 관리자, 원본 및 대상을 구성하고 사용하는 방법을 제시하는 연습은 [SAP BI 7.0에서 SQL Server 2008 Integration Services 사용](https://go.microsoft.com/fwlink/?LinkID=137090)백서를 참조하십시오. 또한 이 백서는 SAP BW에 필요한 개체를 구성하는 방법을 보여 줍니다.  
  
### <a name="using-the-ssis-designer-to-configure-the-destination"></a>SSIS 디자이너를 사용하여 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 SAP BW 대상의 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [SAP BW 대상 편집기&#40;연결 관리자 페이지&#41;](sap-bw-destination-editor-connection-manager-page.md)  
  
-   [SAP BW 대상 편집기&#40;매핑 페이지&#41;](sap-bw-destination-editor-mappings-page.md)  
  
-   [SAP BW 대상 편집기&#40;오류 출력 페이지&#41;](sap-bw-destination-editor-error-output-page.md)  
  
-   [SAP BW 대상 편집기&#40;고급 페이지&#41;](sap-bw-destination-editor-advanced-page.md)  
  
 SAP BW 대상을 구성하는 동안 다양한 대화 상자를 사용하여 SAP Netweaver BW 개체를 조회하거나 만들 수도 있습니다. 이러한 대화 상자에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [InfoPackage 조회](look-up-infopackage.md)  
  
-   [새 InfoObject 만들기](create-new-infoobject.md)  
  
-   [트랜잭션 데이터용 InfoCube 만들기](create-infocube-for-transaction-data.md)  
  
-   [InfoObject 조회](look-up-infoobject.md)  
  
-   [InfoSource 만들기](create-infosource.md)  
  
-   [트랜잭션 데이터용 InfoSource 만들기](create-infosource-for-transaction-data.md)  
  
-   [마스터 데이터용 InfoSource 만들기](create-infosource-for-master-data.md)  
  
-   [InfoPackage 만들기](create-infopackage.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft Connector 1.1 for SAP BW 구성 요소](../microsoft-connector-for-sap-bw-components.md)  
  
  
