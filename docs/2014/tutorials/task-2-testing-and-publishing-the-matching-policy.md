---
title: '작업 2: 일치 정책 테스트 및 게시 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 17723cfd2c1c694f21130e985b6bd65736f90236
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373941"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>작업 2: 일치 정책 테스트 및 게시
  이 태스크에서는 테스트 하 고이 게시 합니다 **Remove Duplicate Suppliers** 일치 정책입니다.  
  
1.  에 **일치 결과** 페이지에서 클릭 **시작** 전체 정책을 테스트 하려면. 여기에서는 정책에 규칙이 하나만 있으므로 규칙 및 정책을 테스트한 결과가 동일합니다.  
  
2.  모든 일치 레코드 및 일치 점수를 목록 상자에서 검토합니다. 가 있는 레코드를 **녹색** 아이콘이 연결 된 피벗 레코드 앞에 있는 중복 됩니다. 이에 대한 몇 가지 예는 다음과 같습니다.  
  
    1.  **레코드 ID: 1000005** 레코드와 일치 하는 항목이 **레코드 Id: 1000004** 사용 하 여 **점수: 100%** 두 레코드 값이 같은 있으므로 **SupplierID (필수)** 합니다 **Supplier Name**, 및 **ContactEmailAddress 열**합니다. DQS는 클러스터의 피벗 레코드로 아무 레코드나 선택합니다.  
  
    2.  레코드 **1000023** 레코드의 일치 하는 항목이 **1000022** 일치 점수를 사용 하 여: 93% 있으므로 두 레코드 값이 같은 **SupplierID (필수)** 및 **Supplier Name** 열, 하지만 다른 값을 **ContactEmailAddress** 열입니다.  
  
    3.  목록 아래쪽으로 스크롤해서 레코드 ID: **1000051** 하 고 **1000052**합니다. 레코드 **1000052** 일치 점수와 일치 하는 것으로 간주 됩니다 **91%** 두 레코드가 동일한 값이 있으므로 합니다 **SupplierID** 고  **ContactEmailAddress** 열에 있지만 다른 값을 **Supplier Name** 열입니다.  
  
     ![정책 정의-정책 결과](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "정책 정의-정책 결과")  
  
3.  모든 일치 하는 레코드 (녹색 아이콘)를 마우스 오른쪽 단추로 클릭 하 고 클릭 **세부 정보 보기** 일치 하는 등의 전체 일치 점수에 각 필드 점수가 기여 하는 방법에 대 한 세부 정보를 확인 합니다.  
  
     ![일치 점수 정보 대화 상자](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "일치 점수 정보 대화 상자")  
  
4.  클릭 **닫습니다** 닫으려면 합니다 **일치 점수 정보** 대화 상자.  
  
5.  클릭 **일치 결과** 페이지의 아래쪽에 있는 탭입니다. 이 탭에는 일치한 레코드 수, 일치하지 않은 레코드 수, 일치한 레코드가 포함된 클러스터 수, 평균 클러스터 크기, 최소 클러스터 크기 및 최대 클러스터 크기와 같은 세부 정보가 표시됩니다. 참조 [일치 정책 만들기](https://msdn.microsoft.com/library/hh270290.aspx) 대 한 자세한 내용은 합니다. 이 작업에서는 결과를 내보낼 수 없습니다. 여기에서는 예제 데이터에 대해 규칙 및 정책을 테스트하기 위해 예제 데이터를 사용하여 일치 정책을 정의하기만 합니다.  
  
     ![일치 결과 탭](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "일치 결과 탭")  
  
6.  클릭 **완료** 일치 정책 만들기를 완료 합니다.  
  
    > [!NOTE]  
    >  여기에서는 일치 정책을 정의했습니다. 따라서 결과를 출력 파일로 내보낼 수 없습니다. 기본적으로 정책 정의를 위해 예제 입력 파일을 사용하고, 규칙을 만들고, 예제 데이터에 대해 규칙 및 정책을 테스트했습니다.  
  
7.  SQL Server Data Quality Services 대화 상자에서 클릭 **게시** 누릅니다 **확인** 메시지 상자에서. 에 해당 하는 정책 정의 게시 하는 이제 합니다 **공급 업체** 기술 자료입니다. 이 기술 자료를 사용해서 입력 파일에 대해 일치 프로세스를 실행하여 중복 항목을 식별하고 제거할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 3: 만들기 및 일치에 대 한 데이터 품질 프로젝트 실행](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
