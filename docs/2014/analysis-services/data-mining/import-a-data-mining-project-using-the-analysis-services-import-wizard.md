---
title: Analysis Services 가져오기 마법사를 사용 하 여 데이터 마이닝 프로젝트 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 62bc9fc5-c6ff-4517-b598-d92df76743a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c34694012a69285ee92fa90c58f293654c961890
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524195"
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>Analysis Services 가져오기 마법사를 사용하여 데이터 마이닝 프로젝트 가져오기
  이 항목에서는 **의**서버에서 가져오기(다차원 및 데이터 마이닝) 프로젝트 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]템플릿을 사용하여 다른 서버의 기존 데이터 마이닝 프로젝트에서 메타데이터를 가져와 새로운 데이터 마이닝 프로젝트를 만드는 방법을 설명합니다.  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>기존 데이터 마이닝 프로젝트에서 데이터 원본, 마이닝 구조 및 마이닝 모델 가져오기  
 **서버에서 가져오기(다차원 및 데이터 마이닝) 프로젝트**템플릿을 사용하면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 새 데이터 마이닝 프로젝트를 만든 다음 지정된 데이터 마이닝 프로젝트에서 메타데이터를 복사합니다. 새 프로젝트에는 가져온 ssASnoversion 데이터베이스와 동일한 데이터 원본, 데이터 원본 뷰, 마이닝 구조 및 마이닝 모델이 포함됩니다. 그러나 프로젝트를 사용하려면 먼저 아래 설명된 대로 특정 속성을 업데이트하고 개체를 처리해야 합니다.  
  
-   새 데이터 마이닝 프로젝트 전용 데이터 원본과 데이터 원본 뷰 정의 가져오는 데이터 자체가 원본 서버에서 복사 되지 않습니다. 따라서 가져오기 프로세스가 완료되고 개체가 만들어진 후 마이닝 구조 및 종속 모델을 학습하여 개체를 데이터로 채워야 합니다. 데이터 마이닝 디자이너의 **모두 처리** 명령을 사용하여 모델 및 구조를 학습할 수 있습니다.  
  
-   이전 버전의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 만들어진 프로젝트를 가져올 경우 데이터 원본에서 프로젝트를 가져올 서버에 설치되지 않은 공급자를 사용할 수도 있습니다. 가져온 마이닝 구조를 처리할 때 오류가 발생하면 데이터 원본을 마우스 오른쪽 단추로 클릭하고 **디자이너 열기** 를 선택하여 연결 문자열을 편집하고 공급자 속성을 검토합니다.  
  
     이때 데이터 마이닝 개체를 처리하거나 데이터 마이닝 모델을 쿼리하는 데 사용한 계정에 데이터 원본에 대한 필요한 사용 권한이 있는지 확인해야 할 수도 있습니다.  
  
-   기본적으로 프로젝트를 가져올 때 작업 영역 데이터베이스가 localhost로 설정되거나 모든 기본 인스턴스가 **에서** 기본 대상 서버 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]로 구성됩니다. 이 속성을 설정하려면 **옵션** 메뉴에서 **비즈니스 인텔리전스 디자이너**, **Analysis Services**, **일반**을 차례로 선택합니다.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 모델 프로젝트에 대한 기본 배포 서버를 구성하기 위해 설정할 수 있는 또 다른 별도의 옵션이 있습니다. **기본 배포 서버**설정은 테이블 형식 프로젝트에 대한 기본 작업 영역 데이터베이스를 결정합니다. 테이블 형식 모델을 지원하는 인스턴스는 데이터 마이닝 프로젝트에 사용할 수 없습니다.  
  
     다차원 또는 데이터 마이닝 모드로 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스를 사용하도록 기본 배포 데이터베이스를 변경할 수 없는 경우 항상 **프로젝트 속성** 대화 상자를 사용하여 배포 데이터베이스를 지정할 수 있습니다.  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>기존 데이터 마이닝 프로젝트를 가져와 새 데이터 마이닝 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트** 대화 상자의 **설치된 템플릿**에서 **비즈니스 인텔리전스**, **Analysis Services**, **서버에서 가져오기(다차원 및 데이터 마이닝)** 를 차례로 클릭합니다.  
  
3.  **이름**에 프로젝트의 이름을 입력하고 위치 및 솔루션 이름을 지정한 다음 **확인**을 클릭합니다.  
  
     **Analysis Services 데이터베이스 가져오기 마법사** 가 시작됩니다. 시작 페이지에서 확인을 클릭하여 계속 진행합니다.  
  
4.  **원본 데이터베이스 선택**페이지의 **서버**에서 가져올 솔루션이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 지정합니다.  
  
     **데이터베이스**에서 가져올 데이터 마이닝 개체가 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 선택합니다.  
  
    > [!WARNING]  
    >  가져올 개체는 지정할 수 없습니다. 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 선택한 경우 모든 다차원 및 데이터 마이닝 개체를 가져옵니다.  
  
     **다음**을 클릭합니다.  
  
5.  **마법사 완료**페이지에 가져오기 작업의 진행률이 표시됩니다. 작업을 취소하거나 가져오는 개체를 변경할 수 없습니다. 완료되었으면 **마침** 을 클릭합니다.  
  
     [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 새 프로젝트가 자동으로 열립니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로젝트 속성&#40;SSAS 테이블 형식&#41;](../tabular-models/properties-ssas-tabular.md)  
  
  
