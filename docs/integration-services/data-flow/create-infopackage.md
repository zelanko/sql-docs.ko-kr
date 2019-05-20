---
title: InfoPackage 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9cd4a848-409f-4681-a390-1c49a2aadbd7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ec8b4ee24e4217492c34319f94976aed44550037
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727077"
---
# <a name="create-infopackage"></a>InfoPackage 만들기

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **InfoPackage 만들기** 대화 상자를 사용하여 SAP Netweaver BW 시스템에서 새 InfoPackage를 만들 수 있습니다.  
  
 **InfoPackage 만들기** 대화 상자는 **SAP BW 대상 편집기** 의 **연결 관리자**페이지에서 열 수 있습니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **InfoPackage 만들기 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **SAP BW 개체 만들기** 그룹 상자에서 **InfoPackage**를 선택한 다음 **만들기**를 클릭합니다.  
  
## <a name="options"></a>옵션  
 **InfoSource**  
 새 InfoPackage의 기준으로 사용할 InfoSource의 이름을 입력합니다.  
  
 **간단한 설명**  
 새 InfoPackage에 대한 설명을 입력합니다.  
  
 **원본 시스템**  
 새 InfoPackage에 연결할 원본 시스템을 선택합니다.  
  
 **특성**  
 InfoPackage가 특성 데이터를 로드함을 나타냅니다.  
  
 **텍스트**  
 InfoPackage가 텍스트 데이터를 로드함을 나타냅니다.  
  
 **트랜잭션**  
 InfoPackage가 트랜잭션 데이터를 로드함을 나타냅니다.  
  
 **저장 및 활성화**  
 새 InfoPackage를 저장하고 활성화합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
