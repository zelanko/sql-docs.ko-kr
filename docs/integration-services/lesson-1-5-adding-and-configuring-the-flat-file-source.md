---
title: '5단계: 플랫 파일 원본 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e95b86d2d29bb3883f6fd76db29f17e5936d1b53
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283685"
---
# <a name="lesson-1-5-add-and-configure-the-flat-file-source"></a>1-5단원: 플랫 파일 원본 추가 및 구성

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 태스크에서는 플랫 파일 원본을 패키지에 추가하고 구성합니다. 플랫 파일 원본은 플랫 파일 연결 관리자에서 정의한 메타데이터를 사용하는 데이터 흐름 구성 요소입니다. 이 메타데이터는 변환 프로세스를 통해 플랫 파일에서 추출할 데이터 형식과 구조를 지정합니다. 플랫 파일 원본은 플랫 파일 연결 관리자의 형식 정의를 사용하여 단일 플랫 파일에서 데이터를 추출합니다.  
  
이 태스크에서는 이전에 생성한 **Sample Flat File Source Data** 연결 관리자를 사용하도록 플랫 파일 원본을 구성합니다.  
  
## <a name="add-a-flat-file-source-component"></a>플랫 파일 원본 구성 요소 추가  
  
1.  **데이터 흐름** 디자이너를 열려면 **Extract Sample Currency Data** 데이터 흐름 태스크를 두 번 클릭하거나 **데이터 흐름** 탭을 선택합니다.  
  
2.  **SSIS 도구 상자**에서 **기타 원본**을 확장한 다음 **플랫 파일 원본** 을 **데이터 흐름** 탭의 디자인 화면으로 끌어다 놓습니다.  
  
3.  **데이터 흐름** 디자인 화면에서 새로 추가한 **플랫 파일 원본**을 마우스 오른쪽 단추로 클릭하고, **이름 바꾸기**를 선택하고, 이름을 **Extract Sample Currency Data**로 변경합니다.  
  
4.  플랫 파일 원본을 두 번 클릭하여 **플랫 파일 원본 편집기** 대화 상자를 엽니다.  
  
5.  **플랫 파일 연결 관리자** 필드에서 **Sample Flat File Source Data**를 선택합니다.  
  
6.  **열** 을 선택하고 열 이름이 올바른지 확인합니다.  
  
7.  **확인**을 선택합니다.  
  
8.  플랫 파일 원본을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
9. **속성** 창에서 **LocaleID** 속성이 **영어(미국)** 로 설정되어 있는지 확인합니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[6단계: 조회 변환 추가 및 구성](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>관련 항목:  
[플랫 파일 원본](../integration-services/data-flow/flat-file-source.md)  
[플랫 파일 연결 관리자](../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
  
