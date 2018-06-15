---
title: 'Analysis Services 자습서 1 단원: 새 테이블 형식 모델 프로젝트 만들기 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 403e6d04d339e3126afe964bd919304d04295c0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044197"
---
# <a name="create-a-tabular-model-project"></a>테이블 형식 모델 프로젝트 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 Visual Studio를 사용 하면 SQL Server Data Tools (SSDT) 또는 Microsoft Analysis Services 프로젝트 VSIX와 Visual Studio 2017 1400 호환성 수준에서 새 테이블 형식 모델 프로젝트를 만듭니다. 새 프로젝트를 만든 후 하기 데이터를 추가 하 고 모델을 작성 합니다. 이 단원에서는 테이블 형식 모델 제작 환경 Visual Studio에에 대 한 간략 한 소개를 제공 합니다.  
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>필수 구성 요소

이 문서는 테이블 형식 모델 제작 자습서의에서 첫 번째 단원입니다. 이 단원을 완료 하려면 몇 가지 필수 구성 요소 내부 필요가 있습니다. 자세한 내용은 참고 [Analysis Services-Adventure Works 자습서](../tutorial-tabular-1400/as-adventure-works-tutorial.md)합니다.  
  
## <a name="create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트 만들기  
  
#### <a name="to-create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트를 만들려면  
  
1.  Visual Studio에서에 **파일** 메뉴를 클릭 하 여 **새로** > **프로젝트**합니다.  
  
2.  에 **새 프로젝트** 대화 상자에서 **설치 됨** > **Business Intelligence** > **Analysis Services**, 클릭 하 고 **Analysis Services 테이블 형식 프로젝트**합니다.  
  
3.  **이름**, 형식 **AW Internet Sales**, 프로젝트 파일의 위치를 지정 합니다.  
  
    하지만 기본적으로 **솔루션 이름** 프로젝트 이름을; 동일 다른 솔루션 이름을 입력할 수 있습니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  에 **테이블 형식 모델 디자이너** 대화 상자에서 **통합된 작업 영역**합니다.  
  
    작업 영역 모델 제작 중 프로젝트와 이름이 같은 테이블 형식 모델 데이터베이스를 호스팅합니다. 통합된 작업 영역 모델 제작에 대 한 별도 Analysis Services 서버 인스턴스를 설치 하지 않아도 Visual Studio에서는 기본 제공 된 인스턴스를 의미 합니다.
      
6.  **호환성 수준이**선택, **SQL Server 2017 / Azure Analysis Services (1400)** 합니다.   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    SQL Server 2017 / Azure Analysis Services (1400) 호환성 수준 목록 상자에 표시 되지 않으면, SQL Server Data Tools의 최신 버전을 사용 하는 하지 않습니다. 최신 버전을 다운로드하려면 [SQL Server Data Tools 설치](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)를 참조하세요.  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>SSDT 테이블 형식 모델 제작 환경 이해  

새 테이블 형식 모델 프로젝트를 만들었으므로 이제 제작 환경 Visual Studio에서 테이블 형식 모델을 탐색할 잠시 하겠습니다.  
  
프로젝트를 만든 후 Visual Studio에서 열립니다. 오른쪽에서에서 **테이블 형식 모델 탐색기**, 모델에 있는 개체의 트리 보기를 표시 합니다. 데이터를 가져온 아직 하지 않은 이후 폴더는 비어 있습니다. 메뉴 모음과 비슷한 작업을 수행 하는 개체 폴더를 마우스 오른쪽 단추로 클릭 수 있습니다. 이 자습서를 실행할 때는 모델 프로젝트에서 서로 다른 개체를 탐색 하는 테이블 형식 모델 탐색기 사용 합니다.

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

클릭는 **솔루션 탐색기** 탭 합니다. 확인할 있습니다 프로그램 **Model.bim** 파일입니다. 디자이너 창의 왼쪽 (Model.bim 탭 된 빈 창)에 표시 되지 않는 경우 **솔루션 탐색기**아래 **AW Internet Sales 프로젝트**, 두 번 클릭은 **Model.bim** 파일입니다. Model.bim 파일 모델 프로젝트에 대 한 메타 데이터를 포함 합니다. 

![as-lesson1-se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
클릭 **Model.bim**합니다. 에 **속성** 창 표시 되며이 중 가장 중요 한 모델 속성은 **DirectQuery 모드** 속성입니다. 이 속성 (Off) 메모리 내 모드 또는 DirectQuery 모드 (On)에서 모델을 배포 하는 경우를 지정 합니다. 이 자습서에 대 한 작성 및 메모리 내 모드에서 모델을 배포 합니다.

![as-lesson1-properties](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
특정 모델 속성에 지정할 수 있는 데이터 모델링 설정에 따라 자동으로 설정 됩니다 모델 프로젝트를 만들면 사용자는 **도구** 메뉴 > **옵션** 대화 상자. 데이터 백업, 작업 영역 보존 및 작업 영역 서버 속성은 작업 영역 데이터베이스(모델 제작 데이터베이스)가 백업되고 메모리에 보관되고 작성되는 방법을 지정합니다. 필요한 경우 나중에 이러한 설정을 변경할 수 있지만 지금은 이러한 속성 그대로 둡니다.  

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **AW Internet Sales** (프로젝트)를 클릭 하 고 **속성**합니다. **AW Internet Sales 속성 페이지** 대화 상자가 나타납니다. 이러한 속성 중 일부 나중 때 설정한 모델을 배포 합니다.  
  
SSDT를 설치할 때 몇 가지 새 메뉴 항목이 Visual Studio 환경에 추가 되었습니다. 클릭는 **모델** 메뉴. 여기에서 있습니다 수 데이터를 가져올 작업 영역 데이터 새로 고침, Excel에서 모델 찾아보기, 큐브 뷰 및 역할을 만들, 모델 뷰를 선택한 계산 옵션을 설정 합니다. 클릭는 **테이블** 메뉴. 여기에서 있습니다 수 및 관계를 관리, 날짜 테이블 설정 지정, 파티션을 만들고, 만들고 테이블 속성 편집 합니다. 클릭는 **열** 메뉴를 추가 하 고 테이블의 열 삭제, 열을 고정 및 정렬 순서를 지정할 수 있습니다. 또한 SSDT 모음에 일부 단추를 추가합니다. 선택한 열에 대 한 표준 집계 측정값을 만들려면 자동 합계 기능을 가장 유용 합니다. 다른 도구 모음 단추를 사용하면 자주 사용하는 기능과 명령에 빠르게 액세스할 수 있습니다.  
  
테이블 형식 모델 제작과 관련된 다양한 기능의 위치와 대화 상자를 살펴보십시오. 일부 항목은 아직 활성, 테이블 형식 모델 제작 환경에 대 한 유용한 정보를 얻을 수 있습니다.  
  

## <a name="whats-next"></a>다음 단계

[2 단원: 데이터 가져오기](../tutorial-tabular-1400/as-lesson-2-get-data.md)합니다.

  
  
  
