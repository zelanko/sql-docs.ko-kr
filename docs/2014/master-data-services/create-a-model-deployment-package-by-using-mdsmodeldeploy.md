---
title: MDSModelDeploy를 사용하여 모델 배포 패키지 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0378394c274e66d71eebd642188f20194d29236b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480000"
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>MDSModelDeploy를 사용하여 모델 배포 패키지 만들기
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 MDSModelDeploy 도구를 사용하여 패키지를 만들 수 있습니다. 지정한 명령에 따라 패키지는 다음 중 하나를 포함할 수 있습니다.  
  
-   모델 개체만  
  
-   모델 개체 및 데이터  
  
 모델 개체만 포함하는 패키지를 배포하려면 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 모델 배포 마법사를 대신 사용할 수 있습니다. 자세한 내용은 [마법사를 사용하여 모델 배포 패키지 만들기](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)를 참조하세요.  
> [!NOTE]  
> 이 버전의 MDSModelDeploy 도구는 GB 이상의 메모리를 사용할 수 없습니다. **모델 개체 및 데이터** 옵션을 사용 하 여 대량 모델을 만들거나 배포할 때 "메모리 부족" 또는 "스트림이 너무 깁니다" 오류가 발생할 수 있습니다. 이 문제를 해결 하려면 MDS 준비를 사용 하 여 데이터를 배포 합니다. 또는 업데이트 된 버전의 MDSModelDeploy 도구를 포함 하는 MDS 2016 이상 버전으로 업그레이드할 수 있습니다.
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
1.  MDSModelDeploy 도구를 실행하는 데 필요한 기본 권한은 다음과 같습니다.  
  
    -   MDS 구성 관리자와 동일한 Windows 권한(Windows 관리자)  
  
    -   MDS 데이터베이스에 대한 DBA 권한  
  
2.  MDSModelDeploy 도구를 사용하여 패키지를 만드는 데 필요한 권한은 다음과 같습니다.  
  
    -   데이터 모델에 대한 MDS 모델 관리자 권한  
  
    -   MDS 통합 관리 기능 권한  
  
3.  MDSModelDeploy 도구를 사용하여 모델을 배포하는 데 필요한 권한은 다음과 같습니다.  
  
    -   MDS 탐색기 함수 권한  
  
    -   MDS 통합 관리 기능 권한  
  
    -   MDS 시스템 관리 기능 권한  
  
4.  MDSModelDeploy 도구를 사용하여 모델을 나열하는 데 필요한 권한은 다음과 같습니다.  
  
    -   MDS 탐색기 함수 권한  
  
    -   목록의 모델을 보기 위한 데이터 모델에 대한 MDS 모델 관리자 권한  
  
 패키지를 만들 모델이 있어야 합니다. 자세한 내용은 [모델 만들기&#40;Master Data Services&#41;](create-a-model-master-data-services.md)를 참조하세요.  
  
 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>MDSModelDeploy를 사용하여 모델 배포 패키지를 만들려면  
  
1.  명령 프롬프트를 엽니다.  
  
2.  MDSModelDeploy.exe의 위치로 이동합니다.  
  
    -   MDS를 기본 위치에 설치한 경우 파일은 *드라이브*: Files\Microsoft SQL Server\120\Master Data services\configuration에 있습니다.  
  
    -   MDS를 기본 위치에 설치하지 않은 경우 로컬 컴퓨터에서 MDSModelDeploy.exe를 검색하십시오.  
  
3.  선택 사항입니다. 보기 옵션 및 도움말입니다.  
  
    -   모든 사용 가능한 옵션을 표시하려면 `MDSModelDeploy` 를 입력하고 Enter 키를 누릅니다.  
  
    -   옵션에 대한 도움말을 표시하려면 *과 같이 입력합니다. 여기서* OptionName `MDSModelDeploy help OptionName`은 옵션의 이름입니다.  
  
4.  선택 사항입니다. 여러 웹 애플리케이션이 있는 경우 이 명령을 입력하고 Enter 키를 눌러 배포할 서비스의 이름을 결정합니다.  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     값의 목록(예: `MDS1, Default Web Site, MDS`)이 반환됩니다. 이 목록의 첫 번째 값(이 경우 `MDS1`)은 모델을 배포하는 데 필요합니다.  
  
5.  모델 개체와 데이터를 포함하는 패키지를 만들려면 다음과 같이 입력하십시오. 여기서 *ModelName*, *VersionName*, *ServiceName*및 *PackageName* 은 각각 모델, 버전, 서비스 및 .pkg 출력 파일의 이름입니다.  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     데이터를 포함하지 않으려면 `-version` 및 `-includedata` 스위치를 사용하지 마십시오.  
  
6.  Enter 키를 누릅니다. 패키지가 성공적으로 만들어지면 "MDSModelDeploy 작업이 성공적으로 완료되었습니다."라는 메시지가 표시됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>참고 항목  
 [모델 배포 옵션 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md)   
 [모델 배포&#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
