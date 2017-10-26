---
title: "캐시 만들기 및 배포는 조회 변환에 대 한 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating cache files for Lookup transformation
- deploying cache files for Lookup transformation
- Lookup transformation cache files
ms.assetid: cedf5cad-2fac-42d0-ad91-9461e117d330
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 88d6515c29c789c12818dfc51c86c5b1d4537247
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="create-and-deploy-a-cache-for-the-lookup-transformation"></a>조회 변환에 대한 캐시 만들기 및 배포
  조회 변환에 대한 캐시 파일(.caw)을 만들고 배포할 수 있습니다. 참조 데이터 집합은 캐시 파일에 저장됩니다.  
  
 조회 변환은 연결된 데이터 원본의 입력 열에 있는 데이터를 참조 데이터 집합의 열과 조인하여 조회합니다.  
  
 캐시 연결 관리자와 캐시 변환을 사용하여 캐시 파일을 만듭니다. 자세한 내용은 [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) 및 [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md)를 참조하세요.  
  
 조회 변환 및 캐시 파일에 대한 자세한 내용은 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
### <a name="to-create-a-cache-file"></a>캐시 파일을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 열고 패키지를 엽니다.  
  
2.  **제어 흐름** 탭에서 데이터 흐름 태스크를 추가합니다.  
  
3.  **데이터 흐름** 탭에서 데이터 흐름에 캐시 변환을 추가한 다음 변환을 데이터 원본에 연결합니다.  
  
     필요한 경우 데이터 원본을 구성합니다.  
  
4.  캐시 변환을 두 번 클릭한 다음 **캐시 변환 편집기**의 **연결 관리자** 페이지에서 **새로 만들기** 를 클릭하여 새 캐시 연결 관리자를 만듭니다.  
  
5.  **캐시 연결 관리자 편집기**의 **일반** 탭에서 다음 옵션을 선택하여 캐시를 저장하도록 캐시 연결 관리자를 구성합니다.  
  
    1.  **파일 캐시 사용**을 선택합니다.  
  
    2.  **파일 이름**에 파일 경로를 입력합니다.  
  
     패키지를 실행할 때 시스템이 파일을 만듭니다.  
  
    > [!NOTE]  
    >  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
6.  **열** 탭을 클릭한 다음 **인덱스 위치** 옵션을 사용하여 인덱스 열이 되는 열을 지정합니다.  
  
     비인덱스 열의 경우 인덱스 위치는 0입니다. 인덱스 열의 경우 인덱스 위치는 일련의 양수입니다.  
  
    > [!NOTE]  
    >  조회 변환은 캐시 연결 관리자를 사용하도록 구성된 경우 참조 데이터 집합의 인덱스 열만 입력 열에 매핑할 수 있습니다. 또한 모든 인덱스 열을 매핑해야 합니다.  
  
     자세한 내용은 [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)을 참조하세요.  
  
7.  필요한 경우 캐시 변환을 구성합니다.  
  
     자세한 내용은 [캐시 변환 편집기&#40;연결 관리자 페이지&#41;](../../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md) 및 [캐시 변환 편집기&#40;매핑 페이지&#41;](../../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)를 참조하세요.  
  
8.  패키지를 실행합니다.  
  
### <a name="to-deploy-a-cache-file"></a>캐시 파일을 배포하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 열고 패키지를 엽니다.  
  
2.  필요에 따라 패키지 구성을 만듭니다. 자세한 내용은 [패키지 구성 만들기](../../../integration-services/packages/create-package-configurations.md)를 참조하세요.  
  
3.  다음을 수행하여 프로젝트에 캐시 파일을 추가합니다.  
  
    1.  1단계에서 연 프로젝트를 솔루션 탐색기에서 선택합니다.  
  
    2.  **프로젝트** 메뉴에서 **기존 항목 추가**를 클릭합니다.  
  
    3.  캐시 파일을 선택한 다음 **추가**를 클릭합니다.  
  
     솔루션 탐색기의 **기타** 폴더에 파일이 표시됩니다.  
  
4.  배치 유틸리티를 만들도록 프로젝트를 구성한 다음 프로젝트를 빌드합니다. 자세한 내용은 [Create a Deployment Utility](../../../integration-services/packages/create-a-deployment-utility.md)를 참조하세요.  
  
     매니페스트 파일인 \< *프로젝트 이름을*> 합니다. X m l 프로젝트, 패키지 및 패키지 구성에 기타 파일을 나열 하는 생성 됩니다.  
  
5.  파일 시스템에 패키지를 배포합니다. 자세한 내용은 [Deploy Packages by Using the Deployment Utility](../../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [배포 유틸리티 만들기](../../../integration-services/packages/create-a-deployment-utility.md)  
  
  

