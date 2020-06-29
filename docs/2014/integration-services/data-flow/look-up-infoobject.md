---
title: InfoObject 조회 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ec67a0330bca614e5224b01d8df81a5e07ff8e95
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432140"
---
# <a name="look-up-infoobject"></a>InfoObject 조회
  **InfoObject 조회** 대화 상자에서는 SAP Netweaver BW 시스템에 정의된 InfoObject를 조회할 수 있습니다. 사용할 수 있는 InfoObject 목록이 표시될 때 원하는 InfoObject를 선택하면 관련 옵션이 SAP BW 대상의 값으로 채워집니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 대상은 **InfoObject 조회** 대화 상자를 사용합니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **InfoObject 조회 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **SAP BW 개체 만들기** 그룹 상자에서 다음 옵션 중 하나를 선택합니다.  
  
    1.  **InfoCube**를 선택합니다. 그런 다음 **만들기**를 클릭합니다. **트랜잭션 데이터용 InfoCube 만들기** 대화 상자에서 목록의 행 중 하나에 대해 **IObject** 열에서 **검색** 을 클릭합니다. 각 행은 패키지의 데이터 흐름에 있는 열을 나타냅니다.  
  
    2.  **InfoSource**를 선택합니다. 그런 다음, **만들기**를 클릭합니다. **InfoSource 만들기** 대화 상자에서 **트랜잭션 데이터**를 선택합니다. **트랜잭션 데이터용 InfoSource 만들기** 대화 상자에서 목록의 행 중 하나에 대해 **IObject** 열에서 **검색** 을 클릭합니다. 각 행은 패키지의 데이터 흐름에 있는 열을 나타냅니다.  
  
    3.  **InfoSource**를 선택합니다. 그런 다음, **만들기**를 클릭합니다. **InfoSource 만들기** 대화 상자에서 **마스터 데이터**를 선택합니다. **마스터 데이터용 InfoSource 만들기** 대화 상자에서 **조회**를 클릭합니다.  
  
 **새 InfoObject 만들기** 대화 상자의 **특성** 섹션에서 **추가** 를 클릭하여 **InfoObject 조회** 대화 상자를 열 수도 있습니다.  
  
## <a name="lookup-options"></a>조회 옵션  
 조회 필드 입력란에서 별표 와일드카드 문자(*)를 사용하거나 문자열 일부를 별표 와일드카드 문자와 함께 사용하여 결과를 필터링할 수 있습니다. 조회 필드를 비워 두면 해당 필드에서 빈 문자열만 일치하는 항목으로 필터링됩니다.  
  
 **특성**  
 특징을 나타내는 InfoObject를 조회합니다.  
  
 **단위**  
 단위를 나타내는 InfoObject를 조회합니다.  
  
 **주요 수치**  
 주요 수치를 나타내는 InfoObject를 조회합니다.  
  
 **시간 특징**  
 시간 특징을 나타내는 InfoObject를 조회합니다.  
  
 **이름**  
 조회할 InfoObject의 이름을 입력하거나 이름의 일부와 별표 와일드카드 문자(*)를 입력합니다. 모든 InfoObject를 포함하려면 별표 와일드카드 문자만 사용합니다.  
  
 **설명**  
 설명을 입력하거나 설명의 일부와 별표 와일드카드 문자(*)를 함께 입력합니다. 설명에 관계없이 모든 InfoObject를 포함하려면 별표 와일드카드 문자만 입력합니다.  
  
 **조회**  
 SAP Netweaver BW 시스템에 정의된 InfoObject 중 일치하는 InfoObject를 조회합니다.  
  
## <a name="lookup-results"></a>조회 결과  
 조회 단추를 클릭하면 SAP Netweaver BW 시스템의 InfoObject 목록이 다음 열 머리글과 함께 표에 표시됩니다.  
  
 **InfoObject**  
 SAP Netweaver BW 시스템에 정의된 InfoObject의 이름을 표시합니다.  
  
 **짧은 텍스트**  
 InfoObject와 연관된 짧은 텍스트를 표시합니다.  
  
 사용할 수 있는 InfoObject 목록이 표시될 때 원하는 InfoObject를 선택하면 관련 옵션이 대상의 값으로 채워집니다.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 데이터용 InfoCube 만들기](create-infocube-for-transaction-data.md)   
 [InfoSource 만들기](create-infosource.md)   
 [트랜잭션 데이터용 InfoSource 만들기](create-infosource-for-transaction-data.md)   
 [마스터 데이터용 InfoSource 만들기](create-infosource-for-master-data.md)   
 [새 InfoObject 만들기](create-new-infoobject.md)   
 [SAP BW 대상 편집기&#40;연결 관리자 페이지&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 도움말](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
