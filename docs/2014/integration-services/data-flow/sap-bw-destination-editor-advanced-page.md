---
title: SAP BW 대상 편집기(고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5396a6a94e1d5c4bfde39153081f3c4137a2c922
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62901041"
---
# <a name="sap-bw-destination-editor-advanced-page"></a>SAP BW 대상 편집기(고급 페이지)
  **SAP BW 대상 편집기** 의 **고급** 페이지를 사용하여 패키지 크기 및 제한 시간 정보와 같은 고급 설정을 지정할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 대상에 대한 자세한 내용은 [SAP BW 대상](sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **고급 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **고급** 을 클릭하여 편집기의 **고급** 페이지를 엽니다.  
  
## <a name="options"></a>옵션  
  
> [!NOTE]  
>  대상을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **패키지 크기**  
 한 번에 전송될 데이터 행 수를 지정합니다. 이 매개 변수에 대한 최적의 값은 SAP Netweaver BW 시스템과 발생할 수 있는 데이터의 추가 처리에 따라 달라집니다. 일반적으로 2000과 20000 사이의 값이 최상의 성능을 제공합니다.  
  
 **프로세스 체인 트리거**  
 (선택 사항) 데이터 로드가 완료된 후 트리거될 프로세스 체인의 이름을 지정합니다.  
  
 **InfoPackage 대기 제한 시간**  
 대상이 InfoPackage가 완료될 때까지 대기해야 하는 최대 시간(초)을 지정합니다.  
  
 **데이터 전송이 완료될 때까지 대기**  
 대상이 SAP Netweaver BW 시스템에서 데이터 로드를 완료할 때까지 대기해야 하는지 여부를 지정합니다.  
  
 **InfoPackage 시작 안 함(대기만)**  
 대상이 InfoPackage를 트리거하지 않고 SAP Netweaver BW 시스템에서 데이터 로드를 시작했다는 알림을 받을 때까지 대기하도록 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 대상 편집기&#40;연결 관리자 페이지&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 대상 편집기&#40;매핑 페이지&#41;](sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 대상 편집기&#40;오류 출력 페이지&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 도움말](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
