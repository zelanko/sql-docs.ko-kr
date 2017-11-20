---
title: "요청 로그 | Microsoft Docs"
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
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 754f96b5e43b26d59bb1e42be6dd2af008c28dd2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="request-log"></a>요청 로그
  **요청 로그** 대화 상자를 사용하여 샘플 데이터에 대해 SAP Netweaver BW 시스템에 요청하는 동안 기록된 이벤트를 확인할 수 있습니다. SAP BW 원본의 구성 문제를 해결해야 하는 경우 이 정보가 유용할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본 구성 요소에 대한 자세한 내용은 [SAP BW 원본](../../integration-services/data-flow/sap-bw-source.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 **요청 로그 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  SAP BW 원본을 구성한 후 **미리 보기** 를 클릭하여 **요청 로그** 대화 상자에서 이벤트를 미리 봅니다.  
  
    > [!NOTE]  
    >  **미리 보기** 를 클릭하면 **미리 보기** 대화 상자도 열립니다. 이 대화 상자에 대한 자세한 내용은 [Preview](../../integration-services/data-flow/preview.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **Time**  
 이벤트가 기록된 시간을 표시합니다.  
  
 **형식**  
 기록된 이벤트의 유형을 표시합니다. 다음 표에서는 가능한 이벤트 유형을 나열합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|S|성공 메시지입니다.|  
|E|오류 메시지입니다.|  
|W|경고 메시지입니다.|  
|I|정보 메시지.|  
|변수를 잠그기 위한|작업이 중단되었습니다.|  
  
 **메시지**  
 기록된 이벤트와 관련된 메시지 텍스트를 표시합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

