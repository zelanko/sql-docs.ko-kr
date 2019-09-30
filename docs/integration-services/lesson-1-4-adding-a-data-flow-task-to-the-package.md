---
title: '4단계: 패키지에 데이터 흐름 태스크 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a98437a88fc81d83c98ec2c3417df6d38bc1b421
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283829"
---
# <a name="lesson-1-4-add-a-data-flow-task-to-the-package"></a>1-4단원: 패키지에 데이터 흐름 태스크 추가

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



원본 및 대상 데이터의 연결 관리자를 만든 후에는 패키지에 데이터 흐름 태스크를 추가합니다. 데이터 흐름 태스크는 원본과 대상 사이에 데이터를 이동하는 데이터 흐름 엔진을 정의하여 데이터 이동 시 데이터를 변환, 정리 및 수정하는 기능을 제공합니다. 데이터 흐름 태스크에서 대부분의 ETL(추출, 변환 및 로드) 프로세스 작업이 발생합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 데이터 흐름을 제어 흐름과 분리합니다.  
  
## <a name="add-a-data-flow-task"></a>데이터 흐름 태스크 추가  
  
1.  **제어 흐름** 탭을 선택합니다.  
  
2.  **SSIS 도구 상자** 창에서 **즐겨찾기**를 확장하고 **데이터 흐름 태스크**를 **제어 흐름** 탭의 디자인 화면으로 끌어 놓습니다.  
  
    > [!NOTE]  
    > SSIS 도구 상자를 사용할 수 없는 경우 **SSIS** 메뉴를 선택한 다음, **SSIS 도구 상자**를 선택하여 표시합니다.  

3.  **제어 흐름** 디자인 화면에서 새 **데이터 흐름 태스크**를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택한 다음 이름을 **Extract Sample Currency Data**로 변경합니다.  
  
    디자인 화면에 추가한 모든 구성 요소에 고유한 이름을 지정합니다. 사용 및 유지 관리의 편의를 위해 각 구성 요소의 기능을 나타내는 이름을 지정해야 합니다. 이러한 명명 지침을 따르면 이해하기 쉬운 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만들 수 있습니다. 주석을 사용하여 패키지를 설명할 수도 있습니다. 주석에 대한 자세한 내용은 [패키지에서 주석 사용](../integration-services/use-annotations-in-packages.md)을 참조하세요.  
  
4.  데이터 흐름 태스크를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음 속성 창에서 **LocaleID** 속성이 **영어(미국)** 로 설정되었는지 확인합니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[5단계: 플랫 파일 원본 추가 및 구성](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>관련 항목:  
[데이터 흐름 태스크](../integration-services/control-flow/data-flow-task.md)  
  
  
  
