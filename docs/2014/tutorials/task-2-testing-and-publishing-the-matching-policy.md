---
title: '작업 2: 테스트 및 게시 하는 정책 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8f67535e5ad4969983b06fcb710c1dfce1d97cb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182378"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>태스크 2: 일치 정책 테스트 및 게시
  이 태스크에서는 테스트 하 고이 게시는 **Remove Duplicate Suppliers** 일치 정책입니다.  
  
1.  에 **일치 결과** 페이지 **시작** 전체 정책을 테스트 합니다. 여기에서는 정책에 규칙이 하나만 있으므로 규칙 및 정책을 테스트한 결과가 동일합니다.  
  
2.  모든 일치 레코드 및 일치 점수를 목록 상자에서 검토합니다. 가 있는 레코드는 **녹색** 연결 된 아이콘이 앞에 있는 피벗 레코드와 중복 됩니다. 이에 대한 몇 가지 예는 다음과 같습니다.  
  
    1.  지정 된 레코드 **레코드 ID: 1000005** 인 레코드의 일치 하는 항목이 **레코드 Id: 1000004** 와 **점수: 100%** 에대한동일한값이있는두레코드모두때문에**SupplierID (필수)**, **Supplier Name**, 및 **ContactEmailAddress 열**합니다. DQS는 클러스터의 피벗 레코드로 아무 레코드나 선택합니다.  
  
    2.  레코드 **1000023** 레코드의 일치 하는 항목이 **1000022** 일치 점수와: 93% 하기 때문에 두 개의 레코드에 대 한 동일한 값이 있는 **SupplierID (필수)** 및  **Supplier Name** 열 하지만 대 한 값이 다른는 **ContactEmailAddress** 열입니다.  
  
    3.  레코드 Id와 두 개의 레코드를 목록의 아래쪽으로 스크롤하여: **1000051** 및 **1000052**합니다. 레코드 **1000052** 일치 점수와 일치 하는 것으로 간주 됩니다 **91%** 두 레코드가 동일한 값에 대 한 하므로 **SupplierID** 및  **ContactEmailAddress** 열 하지만 대 한 값이 다른는 **Supplier Name** 열입니다.  
  
     ![정책 정의-정책 결과](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "정책 정의-정책 결과")  
  
3.  (녹색 아이콘)와 일치 하는 레코드를 마우스 오른쪽 단추로 클릭 하 고 클릭 **세부 정보 보기** 전체 일치 점수에 각 필드 점수가 기여 같이 일치 하는 방법에 대 한 자세한 정보를 확인할 수 있습니다.  
  
     ![대화 상자에 자세히 설명 일치 점수](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "일치 점수에 자세히 설명 대화 상자")  
  
4.  클릭 **닫습니다** 를 닫으려면는 **일치 점수 정보** 대화 상자.  
  
5.  클릭 **일치 결과** 탭 페이지의 맨 아래에 있습니다. 이 탭에는 일치한 레코드 수, 일치하지 않은 레코드 수, 일치한 레코드가 포함된 클러스터 수, 평균 클러스터 크기, 최소 클러스터 크기 및 최대 클러스터 크기와 같은 세부 정보가 표시됩니다. 참조 [Create a Matching Policy](http://msdn.microsoft.com/library/hh270290.aspx) 내용을 확인 합니다. 이 작업에서는 결과를 내보낼 수 없습니다. 여기에서는 예제 데이터에 대해 규칙 및 정책을 테스트하기 위해 예제 데이터를 사용하여 일치 정책을 정의하기만 합니다.  
  
     ![일치 결과 탭](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "일치 결과 탭")  
  
6.  클릭 **마침** 일치 정책 만들기를 완료 합니다.  
  
    > [!NOTE]  
    >  여기에서는 일치 정책을 정의했습니다. 따라서 결과를 출력 파일로 내보낼 수 없습니다. 기본적으로 정책 정의를 위해 예제 입력 파일을 사용하고, 규칙을 만들고, 예제 데이터에 대해 규칙 및 정책을 테스트했습니다.  
  
7.  SQL Server Data Quality Services 대화 상자에서 클릭 **게시** 클릭 **확인** 메시지 상자에서 합니다. 사용자가 정의한 일치 정책에 게시 되는 이제는 **Suppliers** 기술 자료입니다. 이 기술 자료를 사용해서 입력 파일에 대해 일치 프로세스를 실행하여 중복 항목을 식별하고 제거할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 3: 일치에 대한 데이터 품질 프로젝트 만들기 및 실행](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  