---
title: InfoPackage 조회 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7c0cb7a4-cd07-44cc-85cb-eb1ad91f85fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43ad94c5f4cc7d97b99dd0cfadda9811e4ce5f05
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916509"
---
# <a name="look-up-infopackage"></a>InfoPackage 조회

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **InfoPackage 조회** 대화 상자에서는 SAP Netweaver BW 시스템에 정의된 InfoPackage를 조회할 수 있습니다. InfoPackage 목록이 표시될 때 원하는 InfoPackage를 선택하면 관련 옵션이 대상의 값으로 채워집니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 대상은 **프로세스 체인 조회** 대화 상자를 사용합니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **InfoPackage 조회 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **InfoPackage/InfoSource** 그룹 상자에서 **조회** 를 클릭하여 **InfoPackage 조회** 대화 상자를 표시합니다.  
  
## <a name="lookup-options"></a>조회 옵션  
 조회 필드에 별표 와일드카드 문자(*)를 사용하거나 문자열 일부를 별표 와일드카드 문자와 함께 사용하여 결과를 필터링할 수 있습니다. 조회 필드를 비워 두면 해당 필드에서 빈 문자열만 일치하는 항목으로 필터링됩니다.  
  
 **InfoPackage**  
 조회할 InfoPackage의 이름을 입력하거나 이름의 일부와 별표 와일드카드 문자(*)를 입력합니다. 모든 InfoPackage를 포함하려면 별표 와일드카드 문자만 사용합니다.  
  
 **InfoSource**  
 InfoSource의 이름을 입력하거나 이름의 일부와 별표 와일드카드 문자(*)를 입력합니다. InfoSource에 관계없이 모든 InfoPackage를 포함하려면 별표 와일드카드 문자만 사용합니다.  
  
 **원본 시스템**  
 원본 시스템의 이름을 입력하거나 이름의 일부와 별표 와일드카드 문자(*)를 입력합니다. 원본 시스템에 관계없이 모든 InfoPackage를 포함하려면 별표 와일드카드 문자만 사용합니다.  
  
 **조회**  
 SAP Netweaver BW 시스템에 정의된 InfoPackage 중 일치하는 InfoPackage를 조회합니다.  
  
## <a name="lookup-results"></a>조회 결과  
 조회 단추를 클릭하면 SAP Netweaver BW 시스템의 InfoPackage 목록이 다음 열 머리글과 함께 표에 표시됩니다.  
  
 **InfoPackage**  
 SAP Netweaver BW 시스템에 정의된 InfoPackage의 이름을 표시합니다.  
  
 **형식**  
 InfoPackage의 유형을 표시합니다. 다음 표에서는 유형에 사용할 수 있는 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|Trans.|트랜잭션 데이터입니다.|  
|Attr.|특성 데이터입니다.|  
|텍스트|텍스트입니다.|  
  
 **설명**  
 InfoPackage에 대한 설명을 표시합니다.  
  
 **InfoSource**  
 InfoPackage와 연결된 InfoSource의 이름을 표시합니다(있는 경우).  
  
 **Source System**  
 원본 시스템의 이름을 표시합니다.  
  
 InfoPackage 목록이 표시될 때 원하는 InfoPackage를 선택하면 관련 옵션이 대상의 값으로 채워집니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 대상 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
