---
title: SAP BW 원본 편집기(열 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.columns.f1
ms.assetid: c2ec8bb7-be9b-4783-ad88-32512de784b0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 60b888d1a17d56c41b586a0ffa0d2b869aa2ab4f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923234"
---
# <a name="sap-bw-source-editor-columns-page"></a>SAP BW 원본 편집기(열 페이지)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **SAP BW 원본 편집기** 의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본 구성 요소에 대한 자세한 내용은 [SAP BW 원본](../../integration-services/data-flow/sap-bw-source.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 **열 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기**에서 **열** 을 클릭하여 편집기의 **열** 페이지를 엽니다.  
  
## <a name="options"></a>옵션  
  
> [!NOTE]  
>  원본을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록을 확인한 다음 데이터 흐름에 포함할 열을 선택합니다.  
  
 데이터 흐름에 열을 포함하려면 포함하려는 열에 해당하는 확인란을 선택합니다. 확인란을 선택하는 순서에 따라 열이 출력되는 순서가 결정됩니다. 즉, 선택하는 첫 번째 확인란이 첫 번째 출력 열이 되고 두 번째 확인란이 두 번째 출력 열이 됩니다.  
  
 **외부 열**  
 선택된 외부(원본) 열을 표시합니다. 이 원본의 데이터를 소비하는 다운스트림 구성 요소를 구성할 때 선택된 열의 순서대로 해당 출력 열이 표시됩니다.  
  
 열 순서를 변경하려면 **사용 가능한 외부 열** 목록에서 모든 열에 대한 확인란의 선택을 취소합니다. 그런 다음 표시할 순서대로 열을 선택합니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택된 외부(원본) 열의 이름입니다. 하지만 설명이 포함된 고유 이름을 입력할 수도 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에는 해당 열에 대한 **출력 열** 이름이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 원본 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [SAP BW 원본 편집기&#40;고급 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
