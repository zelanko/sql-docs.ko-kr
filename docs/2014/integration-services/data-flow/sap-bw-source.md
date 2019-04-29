---
title: SAP BW 원본 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 169c35d89075646aa3f4964d0e9d6eda92bc13a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901073"
---
# <a name="sap-bw-source"></a>SAP BW 원본
  SAP BW 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 원본 구성 요소입니다. 따라서 SAP BW 원본은 SAP Netweaver BW 버전 7 시스템에서 데이터를 추출하고 이 데이터를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 사용할 수 있도록 합니다.  
  
 이 원본에는 출력 한 개와 오류 출력 한 개가 있습니다.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 SAP BW 원본을 사용하려면 다음 태스크를 수행해야 합니다.  
  
-   [SAP Netweaver BW 개체 준비](#bkmk_Prepare_Objects)  
  
-   [SAP Netweaver BW 시스템에 연결](#bkmk_Connect_Database)  
  
-   [SAP BW 원본 구성](#bkmk_Configure_Source)  
  
##  <a name="bkmk_Prepare_Objects"></a> 원본에 필요한 SAP Netweaver BW 개체 준비  
 SAP BW 원본이 작동하려면 특정 개체가 SAP Netweaver BW 시스템에 있어야 합니다. 이러한 개체가 없는 경우 다음 단계를 수행하여 SAP Netweaver BW 시스템에서 이러한 개체를 만들고 구성해야 합니다.  
  
> [!NOTE]  
>  이러한 개체와 구성 단계에 대한 자세한 내용은 SAP Netweaver BW 설명서를 참조하십시오.  
  
1.  SAP GUI를 통해 SAP Netweaver BW에 로그온하고 트랜잭션 코드 SM59를 입력한 다음 RFC 대상을 만듭니다.  
  
    1.  **Connection Type**에서 **TCP/IP**를 선택합니다.  
  
    2.  **Activation Type**에서 **Registered Server Program**을 선택합니다.  
  
    3.  **Communication Type with Target System**(대상 시스템과 통신 유형)에서 **Non-Unicode (Inactive MDMP Settings)**(비유니코드(비활성 MDMP 설정))를 선택합니다.  
  
    4.  적절한 프로그램 ID를 할당합니다.  
  
2.  오픈 허브 대상을 만듭니다.  
  
    1.  Administrator Workbench(트랜잭션 코드 RSA1)로 이동하고 왼쪽 창에서 **Open Hub Destination**을 선택합니다.  
  
    2.  가운데 창에서 InfoArea를 마우스 오른쪽 단추로 클릭한 다음 **"Create Open Hub Destination"** 을 선택합니다.  
  
    3.  **Destination Type**에서 **"Third Party Tool"** 을 선택한 다음 이전에 만든 RFC 대상을 입력합니다.  
  
    4.  새 오픈 허브 대상을 저장하고 활성화합니다.  
  
3.  DTP(데이터 전송 프로세스)를 만듭니다.  
  
    1.  InfoArea의 가운데 창에서 이전에 만든 대상을 마우스 오른쪽 단추로 클릭한 다음 **"Create data transfer process"** 를 선택합니다.  
  
    2.  DTP를 구성하고 저장하고 활성화합니다.  
  
    3.  메뉴에서 **Goto**를 클릭한 다음 **Settings for Batch Manager**를 클릭합니다.  
  
    4.  순차 처리의 경우 **Number of processes** 를 1로 업데이트합니다.  
  
4.  프로세스 체인을 만듭니다.  
  
    1.  프로세스 체인을 구성할 때 **Start Using Metadata Chain or API** 를 **Start Process** 의 **Scheduling Options**로 선택한 다음 이전에 만든 DTP를 후속 노드로 추가합니다.  
  
    2.  프로세스 체인을 저장하고 활성화합니다.  
  
     SAP BW 원본은 프로세스 체인을 호출하여 데이터 전송 프로세스를 활성화할 수 있습니다.  
  
##  <a name="bkmk_Connect_Database"></a> SAP Netweaver BW 시스템에 연결  
 SAP Netweaver BW 버전 7 시스템에 연결하기 위해 SAP BW 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 패키지의 일부인 SAP BW 연결 관리자를 사용합니다. SAP BW 연결 관리자는 SAP BW 원본이 사용할 수 있는 유일한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결 관리자입니다.  
  
 SAP BW 연결 관리자에 대한 자세한 내용은 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)를 참조하십시오.  
  
##  <a name="bkmk_Configure_Source"></a> SAP BW 원본 구성  
 다음과 같은 방법으로 SAP BW 원본을 구성할 수 있습니다.  
  
-   데이터를 추출하는 데 사용할 OHS(Open Hub Service) 대상을 조회하고 선택합니다.  
  
-   데이터를 추출하는 방법으로 다음 중 하나를 선택합니다.  
  
    -   프로세스 체인을 트리거합니다. 이 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 추출 프로세스를 시작합니다.  
  
    -   SAP Netweaver BW 시스템에서 추출 시작 알림을 기다립니다. 이 경우 SAP Netweaver BW 시스템은 추출 프로세스를 시작합니다.  
  
    -   특정 요청 ID와 연결된 데이터를 검색합니다. 이 경우 SAP Netweaver BW 시스템에서 데이터를 내부 테이블에 이미 추출했으므로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 데이터를 읽기만 합니다.  
  
-   선택한 데이터 추출 방법에 따라 다음 추가 정보를 제공합니다.  
  
    -   **P - 프로세스 체인 트리거** 옵션의 경우 게이트웨이 호스트 이름, 게이트웨이 서비스 이름, RFC 대상의 프로그램 ID 및 프로세스 체인의 이름을 제공합니다.  
  
    -   **W - 알릴 때까지 대기** 옵션의 경우 게이트웨이 호스트 이름, 게이트웨이 서버 이름 및 RFC 대상의 프로그램 ID를 제공합니다. 제한 시간(초)도 지정할 수 있습니다. 제한 시간은 원본이 알림을 받을 때까지 대기할 최대 시간입니다.  
  
    -   **E - 추출만** 옵션의 경우 요청 ID를 제공합니다.  
  
-   문자열 변환의 규칙을 지정합니다. 예를 들어 SAP Netweaver BW 시스템이 유니코드인지 여부에 따라 모든 문자열을 변환하거나 모든 문자열을 `varchar` 또는 `nvarchar`로 변환합니다.  
  
-   선택한 옵션을 사용하여 추출할 데이터를 미리 봅니다.  
  
 원본에 의한 RFC 함수 호출의 로깅을 사용하도록 설정할 수도 있습니다. 이 로깅은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용하도록 설정할 수 있는 선택적 로깅과 별개입니다. 원본이 사용할 SAP BW 연결 관리자를 구성할 때 RFC 함수 호출의 로깅을 사용하도록 설정합니다. SAP BW 연결 관리자를 구성하는 방법은 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)를 참조하십시오.  
  
 원본을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 SAP BW 연결 관리자, 원본 및 대상을 구성하고 사용하는 방법을 제시하는 연습은 [SAP BI 7.0에서 SQL Server 2008 Integration Services 사용](https://go.microsoft.com/fwlink/?LinkID=137090)백서를 참조하십시오. 또한 이 백서는 SAP BW에 필요한 개체를 구성하는 방법을 보여 줍니다.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>SSIS 디자이너를 사용하여 원본 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 SAP BW 원본의 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](sap-bw-source-editor-connection-manager-page.md)  
  
-   [SAP BW 원본 편집기&#40;열 페이지&#41;](sap-bw-source-editor-columns-page.md)  
  
-   [SAP BW 원본 편집기&#40;오류 출력 페이지&#41;](sap-bw-source-editor-error-output-page.md)  
  
-   [SAP BW 원본 편집기&#40;고급 페이지&#41;](sap-bw-source-editor-advanced-page.md)  
  
 SAP BW 원본을 구성하는 동안 다양한 대화 상자를 사용하여 SAP Netweaver BW 개체를 조회하거나 원본 데이터를 미리 볼 수도 있습니다. 이러한 대화 상자에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [RFC 대상 조회](look-up-rfc-destination.md)  
  
-   [프로세스 체인 조회](look-up-process-chain.md)  
  
-   [요청 로그](request-log.md)  
  
-   [미리 보기](preview.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft Connector 1.1 for SAP BW 구성 요소](../microsoft-connector-for-sap-bw-components.md)  
  
  
