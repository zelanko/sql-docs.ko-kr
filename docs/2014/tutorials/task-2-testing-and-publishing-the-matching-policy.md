---
title: '작업 2: 일치 정책 테스트 및 게시 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 434052f26f8cddcb818decdae42e573a10edc678
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006547"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>태스크 2: 일치 정책 테스트 및 게시
  이 태스크에서는 **Remove Duplicate Suppliers** 일치 정책을 테스트 하 고 게시 합니다.  
  
1.  **일치 결과** 페이지에서 **시작** 을 클릭 하 여 전체 정책을 테스트 합니다. 여기에서는 정책에 규칙이 하나만 있으므로 규칙 및 정책을 테스트한 결과가 동일합니다.  
  
2.  모든 일치 레코드 및 일치 점수를 목록 상자에서 검토합니다. **녹색** 아이콘이 연결 된 레코드는 앞에 있는 피벗 레코드와 중복 됩니다. 이에 대한 몇 가지 예는 다음과 같습니다.  
  
    1.  레코드 ID가 **1000005** 인 레코드는 두 레코드의 레코드 **id가 1000004** **(필수 구성 요소)**, **공급자 이름**및 **ContactEmailAddress 열**에 대해 모두 동일 하기 때문에 **점수: 100%** 인 레코드와 일치 합니다. DQS는 클러스터의 피벗 레코드로 아무 레코드나 선택합니다.  
  
    2.  레코드 **1000023** 는 일치 점수가 있는 레코드 **1000022** 과 일치 합니다. 93%는 두 레코드의 공급 업체 **(필수 구성 요소)** 및 **공급자 이름** 열에 동일한 값이 있지만 **ContactEmailAddress** 열에 대 한 다른 값이 있기 때문입니다.  
  
    3.  목록 아래쪽으로 스크롤하여 레코드 Id가 **1000051** 및 **1000052**인 두 레코드를 확인 합니다. 레코드 **1000052는** 및 **ContactEmailAddress** **열에 대해** 동일한 값을 갖지만 **공급자 이름** 열에 대해 다른 값을 가지 므로 일치 점수 **91%** 와 일치 하는 것으로 간주 됩니다.  
  
     ![정책 정의 - 정책 결과](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "정책 정의 - 정책 결과")  
  
3.  일치 하는 레코드를 마우스 오른쪽 단추로 클릭 하 고 (녹색 아이콘 사용), **세부 정보 보기** 를 클릭 하 여 전체 일치 점수에 대 한 각 필드 점수의 기여도와 같은 일치 항목에 대 한 자세한 정보를 확인 합니다.  
  
     ![일치 점수 정보 대화 상자](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "일치 점수 정보 대화 상자")  
  
4.  **일치 점수 정보** 대화 상자를 닫으려면 **닫기** 를 클릭 합니다.  
  
5.  페이지 아래쪽에서 **일치 결과** 탭을 클릭 합니다. 이 탭에는 일치한 레코드 수, 일치하지 않은 레코드 수, 일치한 레코드가 포함된 클러스터 수, 평균 클러스터 크기, 최소 클러스터 크기 및 최대 클러스터 크기와 같은 세부 정보가 표시됩니다. 자세한 내용은 [일치 정책 만들기](https://msdn.microsoft.com/library/hh270290.aspx) 를 참조 하세요. 이 작업에서는 결과를 내보낼 수 없습니다. 여기에서는 예제 데이터에 대해 규칙 및 정책을 테스트하기 위해 예제 데이터를 사용하여 일치 정책을 정의하기만 합니다.  
  
     ![일치 결과 탭](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "일치 결과 탭")  
  
6.  **마침** 을 클릭 하 여 일치 정책 만들기를 마칩니다.  
  
    > [!NOTE]  
    >  여기에서는 일치 정책을 정의했습니다. 따라서 결과를 출력 파일로 내보낼 수 없습니다. 기본적으로 정책 정의를 위해 예제 입력 파일을 사용하고, 규칙을 만들고, 예제 데이터에 대해 규칙 및 정책을 테스트했습니다.  
  
7.  SQL Server Data Quality Services 대화 상자에서 **게시** 를 클릭 하 고 메시지 상자에서 **확인** 을 클릭 합니다. 이제 정의한 일치 정책이 **Suppliers** 기술 자료에 게시 됩니다. 이 기술 자료를 사용해서 입력 파일에 대해 일치 프로세스를 실행하여 중복 항목을 식별하고 제거할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 3: 일치에 대한 데이터 품질 프로젝트 만들기 및 실행](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
