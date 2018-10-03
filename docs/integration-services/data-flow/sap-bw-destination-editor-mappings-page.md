---
title: SAP BW 대상 편집기(매핑 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f2f72788f600c853b638673b1ab1d143059ea0ab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686111"
---
# <a name="sap-bw-destination-editor-mappings-page"></a>SAP BW 대상 편집기(매핑 페이지)
  **SAP BW 대상 편집기** 의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 대상에 대한 자세한 내용은 [SAP BW 대상](../../integration-services/data-flow/sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **매핑 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **매핑** 을 클릭하여 편집기의 **매핑** 페이지를 엽니다.  
  
## <a name="options"></a>Options  
  
> [!NOTE]  
>  대상을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **SAP BW 대상 편집기** 의 **매핑** 페이지는 두 개의 섹션으로 구성되어 있습니다.  
  
-   위쪽 섹션에는 사용 가능한 입력 및 대상 열이 표시되고 이 두 종류의 열 사이에 매핑을 만들 수 있습니다.  
  
-   아래쪽 섹션은 입력 열과 출력 열 사이의 매핑을 보여 주는 표입니다.  
  
### <a name="upper-section-options"></a>위쪽 섹션 옵션  
 위쪽 섹션에는 다음과 같은 옵션이 있습니다.  
  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다.  
  
 입력 열을 대상 열에 매핑하려면 **사용 가능한 입력 열** 목록의 열을 **사용 가능한 대상 열** 목록으로 끌어서 놓습니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다.  
  
 입력 열을 대상 열에 매핑하려면 **사용 가능한 입력 열** 목록의 열을 **사용 가능한 대상 열** 목록으로 끌어서 놓습니다.  
  
 위쪽 섹션에는 백그라운드에서 마우스 오른쪽 단추를 클릭하여 열 수 있는 상황에 맞는 메뉴도 포함되어 있습니다. 상황에 맞는 메뉴에는 다음 옵션이 있습니다.  
  
-   **모든 매핑 선택**  
  
-   **선택한 매핑 삭제**  
  
-   **일치하는 이름별 항목 매핑**  
  
### <a name="lower-section-columns"></a>아래쪽 섹션 열  
 아래쪽 섹션은 매핑 표이며, 다음과 같은 열로 구성되어 있습니다.  
  
 **입력 열**  
 선택한 입력 열을 표시합니다.  
  
 다른 입력 열을 동일한 대상 열에 매핑하려면 목록에서 다른 입력 열을 선택합니다. 매핑을 제거하려면 **\<무시>** 를 선택하여 해당 입력 열을 출력에서 제외합니다.  
  
 **대상 열**  
 열의 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 대상 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 대상 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [SAP BW 대상 편집기&#40;고급 페이지&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
