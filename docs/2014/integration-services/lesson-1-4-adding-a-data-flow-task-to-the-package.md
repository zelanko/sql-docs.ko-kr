---
title: '4단계: 패키지에 데이터 흐름 태스크 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 542b7e3ffcc4a1db5b2053c840b785f775384fe1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62891804"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>4단계: 패키지에 Data Flow Task 추가
  원본 및 대상 데이터의 연결 관리자를 만든 후에는 패키지에 데이터 흐름 태스크를 추가합니다. 데이터 흐름 태스크는 원본과 대상 사이에 데이터를 이동하는 데이터 흐름 엔진을 캡슐화하여 데이터 이동 시 데이터를 변환, 정리 및 수정하는 기능을 제공합니다. 데이터 흐름 태스크에서 대부분의 ETL(추출, 변환 및 로드) 프로세스 작업이 발생합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 데이터 흐름을 제어 흐름과 분리 합니다.  
  
### <a name="to-add-a-data-flow-task"></a>데이터 흐름 태스크를 추가하려면  
  
1.  **제어 흐름** 탭을 클릭합니다.  
  
2.  **SSIS 도구 상자**에서 **즐겨찾기**를 확장하고 **데이터 흐름 태스크** 를 **제어 흐름** 탭의 디자인 화면으로 끌어옵니다.  
  
    > [!NOTE]  
    >  SSIS 도구 상자를 사용할 수 없는 경우 기본 메뉴에서 SSIS 다음에 SSIS 도구 상자를 선택하여 SSIS 도구 상자를 표시합니다.  
  
3.  **제어 흐름** 디자인 화면에서 새로 추가한 **데이터 흐름 태스크**를 마우스 오른쪽 단추로 클릭 하 고 이름 **바꾸기**를 클릭 한 다음 이름을로 `Extract Sample Currency Data`변경 합니다.  
  
     디자인 화면에 추가한 모든 구성 요소에 고유한 이름을 지정하는 것이 좋습니다. 사용 및 유지 관리의 편의를 위해 각 구성 요소가 수행하는 기능을 나타내는 이름을 지정해야 합니다. 이러한 명명 지침을 따르면 이해하기 쉬운 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만들 수 있습니다. 주석을 사용하여 패키지를 설명할 수도 있습니다. 주석에 대한 자세한 내용은 [패키지에서 주석 사용](use-annotations-in-packages.md)을 참조하세요.  
  
4.  데이터 흐름 태스크를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 속성 창에서 `LocaleID` 속성이 **영어 (미국)** 로 설정 되어 있는지 확인 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [5단계: 플랫 파일 원본 추가 및 구성](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름 태스크](control-flow/data-flow-task.md)  
  
  
