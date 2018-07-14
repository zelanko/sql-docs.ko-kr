---
title: 미리 보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 551494c4-9e27-4592-9200-c6bf19e80c9a
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fa7f94ad690362189b29c7e86e34519d1a937bc1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37281599"
---
# <a name="preview"></a>미리 보기
  **미리 보기** 대화 상자를 사용하여 SAP BW 원본이 추출할 데이터를 미리 볼 수 있습니다.  
  
> [!IMPORTANT]  
>  **SAP BW 원본 편집기** 의 **연결 관리자** 페이지에서 사용할 수 있는 **미리 보기**옵션은 데이터를 실제로 추출합니다. 이전 추출 이후에 변경된 데이터만 추출하도록 SAP Netweaver BW를 구성한 경우 **미리 보기** 를 선택하면 미리 본 데이터가 다음 추출에서 제외됩니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 원본 구성 요소에 대한 자세한 내용은 [SAP BW 원본](sap-bw-source.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
 **미리 보기 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 원본이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 원본을 두 번 클릭합니다.  
  
3.  **SAP BW 원본 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  SAP BW 원본을 구성합니다.  
  
5.  SAP BW 원본을 구성한 후 **연결 관리자** 페이지에서 **미리 보기** 를 클릭하여 **미리 보기** 대화 상자에서 데이터를 미리 봅니다.  
  
    > [!NOTE]  
    >  **미리 보기** 를 클릭하면 **요청 로그** 대화 상자도 열립니다. 이 대화 상자에 대한 자세한 내용은 [Request Log](request-log.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **미리 보기** 대화 상자에는 SAP Netweaver BW 시스템에서 요청된 행이 표시됩니다. 표시되는 열은 원본 데이터에 정의된 열입니다.  
  
 이 대화 상자에 다른 옵션은 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SAP BW 원본 편집기 &#40;연결 관리자 페이지&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 도움말](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
