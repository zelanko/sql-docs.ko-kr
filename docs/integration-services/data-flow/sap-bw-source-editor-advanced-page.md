---
description: SAP BW 원본 편집기(고급 페이지)
title: SAP BW 원본 편집기(고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 433698b83ed1148f473062658b95d99e9657e6ad
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88495761"
---
# <a name="sap-bw-source-editor-advanced-page"></a>SAP BW 원본 편집기(고급 페이지)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **SAP BW 원본 편집기** 의 **고급** 페이지를 사용하여 문자열 변환 규칙과 제한 시간을 지정하고 특정 요청 ID의 상태를 다시 설정할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본 구성 요소에 대한 자세한 내용은 [SAP BW 원본](../../integration-services/data-flow/sap-bw-source.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 **연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기** 에서 **고급** 을 클릭하여 편집기의 **고급** 페이지를 엽니다.  
  
## <a name="options"></a>옵션  
  
> [!NOTE]  
>  원본을 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **문자열 변환**  
 문자열 변환을 위해 적용할 규칙을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**자동 문자열 변환**|SAP Netweaver BW 시스템이 유니코드 시스템이면 모든 문자열을 **nvarchar** 로 변환하고, 그렇지 않으면 모든 문자열을 **varchar** 로 변환합니다.|  
|**VarChar로 문자열 변환**|모든 문자열을 **varchar** 로 변환합니다.|  
|**NVarChar로 문자열 변환**|모든 문자열을 **nvarchar** 로 변환합니다.|  
  
 **제한 시간(초)**  
 원본이 대기해야 하는 최대 시간(초)을 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 편집기의 **연결 관리자** 페이지에서 **실행 모드** 의 값으로 **W - 알릴 때까지 대기** 를 선택한 경우에만 유효합니다. 자세한 내용은 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)을 참조하세요.  
  
 **요청 ID**  
 **다시 설정** 을 클릭할 때 "G - 녹색"으로 상태를 다시 설정할 요청 ID를 지정합니다.  
  
 **재설정**  
 확인 메시지를 표시한 후 지정된 요청 ID의 상태를 "G - 녹색"으로 다시 설정할 수 있습니다. 이 옵션은 문제가 발생하고 SAP Netweaver BW 시스템에서 노란색 또는 빨간색 상태로 요청에 플래그를 지정한 경우에 유용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SAP BW 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 원본 편집기&#40;열 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [SAP BW 원본 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
