---
title: "프로세스 체인 조회 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29791eaade29aa28089dfb579206c2dbddbed1ad
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="look-up-process-chain"></a>프로세스 체인 조회
  **프로세스 체인 조회** 대화 상자에서는 SAP Netweaver BW 시스템에 정의된 프로세스 체인을 조회할 수 있습니다. 사용할 수 있는 프로세스 체인 목록이 표시될 때 원하는 체인을 선택하면 관련 옵션이 원본의 값으로 채워집니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본은 **프로세스 체인 조회** 대화 상자를 사용합니다. SAP BW 원본에 대한 자세한 내용은 [SAP BW Source](../../integration-services/data-flow/sap-bw-source.md)을 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **프로세스 체인 조회 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **프로세스 체인** 그룹 상자에서 **조회** 를 클릭하여 **프로세스 체인 조회** 대화 상자를 표시합니다.  
  
     **프로세스 체인** 그룹 상자는 **실행 모드** 의 값이 **P - 프로세스 체인 트리거**인 경우에만 나타납니다.  
  
## <a name="lookup-options"></a>조회 옵션  
 조회 필드에 별표 와일드카드 문자(*)를 사용하거나 문자열 일부를 별표 와일드카드 문자와 함께 사용하여 결과를 필터링할 수 있습니다. 조회 필드를 비워 두면 해당 필드에서 빈 문자열만 일치하는 항목으로 필터링됩니다.  
  
 **Process chain**  
 조회할 프로세스 체인의 이름을 입력하거나 이름의 일부와 별표 와일드카드 문자(*)를 입력합니다. 모든 프로세스 체인을 포함하려면 별표 와일드카드 문자만 사용합니다.  
  
 **조회**  
 SAP Netweaver BW 시스템에 정의된 프로세스 체인 중 일치하는 프로세스 체인을 조회합니다.  
  
## <a name="lookup-results"></a>조회 결과  
 조회 단추를 클릭하면 SAP Netweaver BW 시스템의 프로세스 체인 목록이 다음 열 머리글과 함께 표에 표시됩니다.  
  
 **프로세스 체인**  
 SAP Netweaver BW 시스템에 정의된 프로세스 체인의 이름을 표시합니다.  
  
 **설명**  
 프로세스 체인에 대한 설명을 표시합니다.  
  
 사용할 수 있는 프로세스 체인 목록이 표시될 때 원하는 체인을 선택하면 관련 옵션이 원본의 값으로 채워집니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
