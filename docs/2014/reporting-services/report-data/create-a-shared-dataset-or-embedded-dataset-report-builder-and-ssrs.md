---
title: 공유 데이터 세트 또는 포함된 데이터 세트 만들기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d1d7bc71-f0e9-4ce5-b3ad-6fee54388a31
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 208c5608037d99b9dc02f1ab7fefd151cd4bdecf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107433"
---
# <a name="create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs"></a>공유 데이터 세트 또는 포함된 데이터 세트 만들기(보고서 작성기 및 SSRS)
  단일 보고서에 사용할 포함된 데이터 세트를 만들거나 여러 보고서에 사용하기 위해 보고서 서버에 저장할 공유 데이터 세트를 만들 수 있습니다. 데이터 세트를 만들려면 포함된 데이터 원본 또는 공유 데이터 원본이 있어야 합니다.  
  
 보고서 작성기를 사용하여 다음 태스크를 수행합니다.  
  
-   데이터 세트 디자인 뷰에서 공유 데이터 세트를 만듭니다. 공유 데이터 세트는 게시된 공유 데이터 원본을 사용해야 합니다.  
  
-   보고서 디자인 뷰에서 포함된 데이터 세트를 만듭니다.  
  
-   데이터 세트를 보고서 서버 또는 SharePoint 사이트에 직접 저장합니다.  
  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 보고서 작성기를 사용하여 다음 태스크를 수행합니다.  
  
1.  솔루션 탐색기에서 공유 데이터 세트를 만듭니다. 공유 데이터 세트는 솔루션 탐색기의 공유 데이터 원본 폴더에 있는 데이터 원본을 사용해야 합니다.  
  
2.  보고서 데이터 창에서 포함된 데이터 세트를 만듭니다.  
  
3.  필요에 따라 공유 데이터 세트 및 공유 데이터 원본과 보고서를 함께 배포합니다. 각 항목 유형에 대해 프로젝트 속성을 사용하여 보고서 서버나 SharePoint 사이트에 폴더의 경로를 지정합니다.  
  
 자세한 내용은 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-open-report-builder-and-create-a-shared-dataset"></a>보고서 작성기를 열고 공유 데이터 세트를 만들려면  
  
1.  보고서 작성기를 엽니다. 다음 그림과 같이 **새 보고서 또는 데이터 세트** 창이 열립니다.  
  
     ![rs_NewSharedDataset](../media/rs-newshareddataset.gif "rs_NewSharedDataset")  
  
    > [!NOTE]  
    >  
  **새 보고서 또는 데이터 세트 창**이 나타나지 않으면 보고서 작성기 단추에서 **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창의 **데이터 세트 만들기**에서 **공유 데이터 세트**를 클릭합니다.  
  
3.  오른쪽 창에서 **찾아보기** 를 클릭하여 보고서 서버에서 공유 데이터 원본을 선택한 다음 **만들기**를 클릭합니다. 공유 데이터 원본과 연결된 쿼리 디자이너가 열립니다.  
  
4.  쿼리 디자이너에서 데이터 세트에 포함할 필드를 지정합니다.  
  
5.  
  **실행** (**!**)을 클릭하여 쿼리를 실행합니다.  
  
6.  
  **보고서 작성기** 단추에서 **저장** 또는 **다른 이름으로 저장**을 클릭하여 공유 데이터 세트를 보고서 서버에 저장합니다.  
  
7.  보고서 작성기를 종료하려면 **보고서 작성기**를 클릭한 다음 **보고서 작성기 끝내기**를 클릭합니다. 보고서로 작업하려면 **보고서 작성기**를 클릭한 다음 **새로 만들기** 또는 **열기**를 클릭합니다.  
  
### <a name="to-set-query-parameter-options"></a>쿼리 매개 변수 옵션을 설정하려면  
  
1.  보고서 작성기를 엽니다.  
  
2.  **열기**를 클릭합니다.  
  
3.  보고서 서버로 이동하여 공유 데이터 원본의 폴더를 선택합니다.  
  
4.  
  **항목 유형**의 드롭다운 목록에서 데이터 세트(*.rsd)를 클릭합니다.  
  
5.  공유 데이터 세트를 선택한 다음, **열기**를 클릭합니다. 연결된 쿼리 디자이너가 열립니다.  
  
6.  리본에서 **데이터 세트 속성**을 클릭합니다.  
  
7.  **매개 변수**를 클릭합니다. 이 페이지에서 기본값을 상수나 식으로 설정하고 매개 변수를 읽기 전용, Null 허용 또는 **쿼리에서 생략**으로 표시합니다. 자세한 내용은 [데이터 세트 속성 대화 상자, 매개 변수&#40;보고서 작성기&#41;](../dataset-properties-dialog-box-parameters-report-builder.md)를 참조하세요.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
### <a name="to-create-a-dataset-from-a-sql-server-relational-database"></a>SQL Server 관계형 데이터베이스에서 데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본의 이름을 마우스 오른쪽 단추로 클릭한 다음, **데이터 세트 추가**를 클릭합니다. 
  **데이터 세트 속성** 대화 상자의 **쿼리** 페이지가 열립니다.  
  
2.  
  **이름**에 데이터 세트의 이름을 입력하거나 기본 이름을 적용합니다.  
  
    > [!NOTE]  
    >  데이터 세트 이름은 보고서 내에서만 사용됩니다. 의미를 명확하게 전달하기 위해 쿼리에서 반환하는 데이터에 대한 설명이 포함된 데이터 세트 이름을 사용하는 것이 좋습니다.  
  
3.  
  **데이터 원본**에서 기존 공유 데이터 원본의 이름을 찾아 선택하거나 **새로 만들기** 를 클릭하여 포함된 데이터 원본을 새로 만듭니다.  
  
4.  
  **쿼리 유형** 옵션을 선택합니다. 데이터 원본 유형에 따라 옵션이 달라집니다.  
  
    -   데이터 원본의 쿼리 언어를 사용하여 쿼리를 작성하려면 **Text** 를 선택합니다.  
  
    -   관계형 데이터베이스 테이블의 모든 필드를 반환하려면 **Table** 을 선택합니다.  
  
    -   저장 프로시저를 이름으로 실행하려면 **StoredProcedure** 를 선택합니다.  
  
5.  
  **쿼리**에 쿼리, 저장 프로시저 또는 테이블 이름을 입력합니다. 또는 **쿼리 디자이너** 를 클릭하여 그래픽 또는 텍스트 기반 쿼리 디자이너 도구를 열거나 **가져오기** 를 클릭하여 기존 보고서에서 쿼리를 가져옵니다.  
  
     경우에 따라 데이터 원본에서 쿼리를 실행해야만 쿼리로 지정된 필드 컬렉션을 확인할 수 있습니다. 예를 들어 저장 프로시저는 결과 집합에 가변적 필드 집합을 반환할 수 있습니다. 
  **필드 새로 고침**을 클릭하여 데이터 원본에서 쿼리를 실행하고 보고서 데이터 창에서 데이터 세트 필드 컬렉션을 채우는 데 필요한 필드 이름을 검색합니다. 필드 컬렉션은 **데이터 세트 속성** 대화 상자를 닫은 후 데이터 세트 노드 아래에 나타납니다.  
  
6.  
  **제한 시간**에 보고서 서버에서 데이터베이스의 응답을 기다리는 시간(초)을 입력합니다. 기본값은 0초입니다. 제한 시간 값이 0초이면 쿼리 시간이 제한되지 않습니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     데이터 세트 및 해당 필드 컬렉션이 데이터 원본 노드 아래의 보고서 데이터 창에 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [쿼리 디자이너 &#40;보고서 작성기&#41;](../query-designers-report-builder.md)   
 [대화 상자, 창 및 마법사에 대 한 보고서 작성기 도움말](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [보고서 &#40;보고서 작성기 및 SSRS&#41;에 데이터를 추가 합니다.](report-datasets-ssrs.md)   
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [포함 된 데이터 집합 및 공유 데이터 집합 &#40;보고서 작성기 및 SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
