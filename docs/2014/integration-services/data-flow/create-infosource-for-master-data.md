---
title: 마스터 데이터용 InfoSource 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 87ada4ef6cf9266720ac0c9742440d0d60345c88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827954"
---
# <a name="create-infosource-for-master-data"></a>마스터 데이터용 InfoSource 만들기
  **마스터 데이터용 InfoSource 만들기** 대화 상자에서는 SAP Netweaver BW 시스템의 마스터 데이터에 대한 새 InfoSource를 만듭니다.  
  
 **SAP BW 대상 편집기** 의 **연결 관리자** 페이지에서 **마스터 데이터용 InfoSource 만들기**대화 상자를 열 수 있습니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **마스터 데이터용 InfoSource 만들기 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기**에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **SAP BW 개체 만들기** 그룹 상자에서 **InfoSource**를 선택한 다음 **만들기**를 클릭합니다.  
  
5.  **InfoSource 만들기** 대화 상자에서 **마스터 데이터**를 선택한 다음 **확인**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **InfoObject 이름**  
 새 InfoSource의 기준으로 사용할 InfoObject 이름을 입력합니다.  
  
 **조회**  
 InfoObject를 조회합니다. 이 옵션을 선택하면 InfoObject를 선택할 수 있는 **InfoObject 조회** 대화 상자가 열립니다. 이 대화 상자에 대한 자세한 내용은 [Look Up InfoObject](look-up-infoobject.md)을 참조하십시오.  
  
 InfoObject를 선택하면 선택한 InfoObject 이름으로 **InfoObject 이름** 입력란이 채워집니다.  
  
 **새로 만들기**  
 새 InfoObject를 만듭니다. 이 옵션을 선택하면 새 InfoObject를 만들 수 있는 **새 InfoObject 만들기** 대화 상자가 열립니다. 이 대화 상자에 대한 자세한 내용은 [Create New InfoObject](create-new-infoobject.md)을 참조하십시오.  
  
 InfoObject를 만들면 새 InfoObject 이름으로 **InfoObject 이름** 입력란이 채워집니다.  
  
 **간단한 설명**  
 새 InfoSource에 대한 간단한 설명을 입력합니다.  
  
 **자세한 설명**  
 새 InfoSource에 대한 자세한 설명을 입력합니다.  
  
 **원본 시스템**  
 새 InfoSource에 연결할 원본 시스템을 선택합니다.  
  
 **응용 프로그램**  
 새 InfoSource에 연결할 애플리케이션의 이름을 입력 합니다.  
  
 **특성**  
 마스터 데이터가 특성으로 구성되었음을 나타냅니다.  
  
 **텍스트**  
 마스터 데이터가 특성으로 구성되었음을 나타냅니다.  
  
 **저장 및 활성화**  
 새 InfoSource를 저장하고 활성화합니다.  
  
## <a name="see-also"></a>관련 항목  
 [InfoSource 만들기](create-infosource.md)   
 [Microsoft Connector 1.1 for SAP BW F1 도움말](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
