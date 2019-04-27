---
title: SAP BW 원본 편집기(오류 출력 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6e23b0c-949a-46d1-8424-4dc3d9035e79
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8eb25ae1083e05ccb85dda6d07d391ca58d7951a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770715"
---
# <a name="sap-bw-source-editor-error-output-page"></a>SAP BW 원본 편집기(오류 출력 페이지)
  **SAP BW 원본 편집기** 의 **오류 출력** 페이지에서는 오류 처리 옵션을 선택하고 오류 출력 열에 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본 구성 요소에 대한 자세한 내용은 [SAP BW 원본](sap-bw-source.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 **오류 출력 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기**에서 **오류 출력** 을 클릭하여 편집기의 **오류 출력** 페이지를 엽니다.  
  
## <a name="options"></a>변수  
  
> [!NOTE]  
>  원본을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **입력 또는 출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **SAP BW 원본 편집기** 대화 상자의 **열** 페이지에서 선택한 외부(원본) 열을 표시합니다. 이 대화 상자에 대한 자세한 내용은 [SAP BW 원본 편집기&#40;열 페이지&#41;](sap-bw-source-editor-columns-page.md)을 참조하세요.  
  
 **오류**  
 오류가 발생할 경우 수행해야 할 SAP BW 원본을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **잘림**  
 잘림이 발생할 경우 수행해야 할 SAP BW 원본을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **설명**  
 오류에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림이 발생한 경우 선택한 모든 셀에 수행할 SAP BW 원본을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 원본 편집기&#40;열 페이지&#41;](sap-bw-source-editor-columns-page.md)   
 [SAP BW 원본 편집기&#40;고급 페이지&#41;](sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 도움말](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
