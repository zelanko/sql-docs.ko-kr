---
title: RFC 대상 조회 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 046ec13269181eedda2d9fcfd891e7dd823db372
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282237"
---
# <a name="look-up-rfc-destination"></a>RFC 대상 조회
  **RFC 대상 조회** 대화 상자에서는 SAP Netweaver BW 시스템에 정의된 RFC 대상을 조회할 수 있습니다. 사용할 수 있는 RFC 대상 목록이 표시될 때 원하는 대상을 선택하면 관련 옵션이 필요한 값으로 채워집니다.  
  
 SAP BW 원본과 SAP BW 대상은 모두 **RFC 대상 조회** 대화 상자를 사용합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 구성 요소에 대한 자세한 내용은 [SAP BW 원본](../../integration-services/data-flow/sap-bw-source.md) 및 [SAP BW 대상](../../integration-services/data-flow/sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **RFC 대상 조회 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본 또는 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본 또는 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기** 또는 **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **RFC 대상** 그룹 상자에서 **조회** 를 클릭하여 **RFC 대상 조회** 대화 상자를 표시합니다.  
  
     **SAP BW 원본 편집기**에서 **RFC 대상** 그룹 상자는 **실행 모드** 가 **P - 프로세스 체인 트리거** 또는 **W - 알릴 때까지 대기**인 경우에만 표시됩니다.  
  
## <a name="options"></a>옵션  
 **대상**  
 SAP Netweaver BW 시스템에 정의된 RFC 대상의 이름을 표시합니다.  
  
 **게이트웨이 호스트**  
 게이트웨이 호스트의 서버 이름 또는 IP 주소를 표시합니다. 일반적으로 이름 또는 IP 주소는 SAP 애플리케이션 서버와 동일합니다.  
  
 **게이트웨이 서비스**  
 게이트웨이 서비스 이름을 **sapgwNN**형식으로 표시합니다. 여기서 **NN** 은 시스템 번호입니다.  
  
 **프로그램 ID**  
 RFC 대상과 연결된 프로그램 ID를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 대상 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
