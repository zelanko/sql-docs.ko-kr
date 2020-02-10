---
title: '작업 4 (선택 사항): 새 데이터 집합 결합, 일치 및 게시 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2d27a5bcd87ffd84b33de229d955dc9494846a72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489276"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>태스크 4(선택 사항): 새 데이터 집합 결합, 일치 및 게시
  시간이 지날수록 MDS 저장소에 추가하는 데이터가 늘어나게 됩니다. 데이터를 추가 하기 전에 MDS에서 이미 관리 되는 데이터와 새 데이터를 비교 하 여 중복 되거나 부정확 한 데이터를 추가 하지 않도록 하는 것이 유용할 수 있습니다. Excel용 Master Data Services 추가 기능에서는 데이터를 MDS에 게시하기 전에 두 워크시트의 데이터를 결합하고 데이터를 비교해서 중복된 항목을 식별하고 제거할 수 있습니다. MDS Excel 추가 기능의 일치 기능에는 데이터에서 일치 항목을 식별하기 위해 DQS 일치 기능이 사용됩니다. 이 작업에서는 MDS에 데이터를 게시하기 전에 두 워크시트의 데이터를 하나로 결합한 후 일치 작업을 수행해서 중복된 항목을 식별하고 제거합니다. 자세한 내용은 Excel용 MDS 추가 기능 및 [데이터 결합](https://msdn.microsoft.com/library/hh548680.aspx) 항목 [의 데이터 품질 일치](https://msdn.microsoft.com/library/hh548681.aspx) 를 참조 하세요.  
  
1.  새 **Excel**인스턴스를 시작 합니다. **시작**을 클릭 하 고 **실행**을 가리킨 다음 **Excel**을 입력 하 고 **확인**을 클릭 합니다.  
  
2.  메뉴 모음에서 **마스터 데이터** 를 클릭 하 여 **마스터 데이터** 탭으로 전환 합니다.  
  
3.  연결 **및 로드** 그룹의 리본에서 **연결** 을 클릭 하 여 **MDS 서버**에 연결 합니다. 이 연결은 이 단원의 앞 부분에서 구성했습니다.  
  
     ![Excel - 마스터 데이터 탭의 탐색기 표시 단추](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - 마스터 데이터 탭의 탐색기 표시 단추")  
  
4.  오른쪽에 **마스터 데이터 탐색기** 창이 표시 됩니다. 마스터 데이터 탐색기 표시 되지 않으면 리본에서 **탐색기 표시** 단추를 클릭 합니다.  
  
5.  **마스터 데이터 탐색기** 창의 **모델**드롭다운 목록에서 **Suppliers** 를 선택 합니다. 모델에는 **공급자**가 하나씩 있습니다.  
  
     ![Excel - 마스터 데이터 탐색기 창](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - 마스터 데이터 탐색기 창")  
  
6.  엔터티 목록에서 **공급자** 를 두 번 클릭 하 여 엔터티 멤버를 Excel 워크시트로 로드 합니다.  
  
7.  맨 아래에 있는 **sheet2** 를 클릭 하 여 **sheet2** 탭으로 전환 합니다. **Sheet2**가 표시 되지 않으면 새 워크시트를 추가 합니다.  
  
8.  **Suppliers** 파일 (자습서 파일에 포함 된 원본 입력 파일)을 열고 **CombineAndCleanse** 워크시트의 모든 행 (3 개)을 **Sheet2**로 복사 합니다.  
  
9. **MDS**에 연결 된 **Microsoft excel** ( **정리 및 일치 하는 공급자 목록** Excel이 아님)의 **공급 업체** 시트로 다시 전환 합니다.  
  
10. 메뉴 모음에서 **마스터 데이터** 를 클릭합니다.  
  
11. 리본에서 **데이터 결합** 을 클릭 합니다. **데이터 결합** 대화 상자가 표시 됩니다.  
  
12. **데이터 결합** 대화 상자에서 다음 이미지에 표시 된 것과 같이 **MDS 데이터와 결합할 범위** 옆의 단추를 클릭 합니다.  
  
     ![Excel - 데이터 결합 대화 상자](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - 데이터 결합 대화 상자")  
  
13. 지금은 대화 상자가 축소된 상태로 표시됩니다. 이제 **sheet2** 를 클릭 하 여 행이 4 개 (헤더 행 포함) 인 새 공급자 데이터가 있는 **sheet2** 탭으로 전환 합니다.  
  
14. **Sheet2**에서 **머리글 행을 포함 하는 모든 행** 을 선택 합니다 (이미 선택 되어 있는 경우에도). **MDS 데이터와 결합할 범위가** 자동으로 업데이트 되는 것을 볼 수 있습니다.  
  
     ![Excel - 데이터 결합 대화 상자 - 최소화됨](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - 데이터 결합 대화 상자 - 최소화됨")  
  
15. **데이터 결합** 대화 상자를 닫지 않고 **Suppliers** 탭으로 다시 전환 합니다.  
  
16. **텍스트 상자**옆에 있는 **단추** 를 클릭 합니다. 이제 대화 상자가 확장된 상태로 표시됩니다. **공급자** MDS **엔터티** 열과 **Excel** 열 간의 모든 매핑이 자동으로 채워집니다.  
  
     ![Excel - 데이터로 채워진 데이터 결합 대화 상자](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - 데이터로 채워진 데이터 결합 대화 상자")  
  
17. **Code** 엔터티 열이 워크시트의 **공급자** 열에 매핑되고 **우편** 번호 엔터티 열이 워크시트의 **우편** 번호 열에 매핑되는지 확인 합니다.  
  
18. **데이터 결합** 대화 상자에서 **결합**을 클릭 합니다.  
  
19. 세 개의 데이터 행이 워크시트 하단에 추가되었고 색상으로 표시되었는지 확인합니다.  
  
     ![Excel - 결합 후 새 요소](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - 결합 후 새 요소")  
  
20. 리본에서 **수학 데이터** 를 클릭 하 여 중복 항목을 식별 합니다. 이 기능은 DQS의 일치 기능을 사용합니다.  
  
21. **데이터 일치** 대화 상자에서 **DQS 기술 자료**에 대 한 **공급자** 를 선택 합니다.  
  
     ![Excel - 데이터 일치 대화 상자](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - 데이터 일치 대화 상자")  
  
22. 다음 표에 표시된 대로 워크시트 열을 도메인에 매핑합니다.  
  
    |워크시트 열|도메인|  
    |----------------------|------------|  
    |Code(MDS에서 Supplier 엔터티에 대한 Code로 업로드한 Supplier ID)|Supplier ID|  
    |Name(MDS에 Supplier 엔터티에 대한 이름으로 업로드한 Supplier Name)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. **코드** 열 매핑의 **필수 구성 요소** 를 선택 합니다.  
  
24. 이미지에 **표시 된 것** 처럼 **연락처 전자 메일** 의 **가중치** 로 **70%** 를 **공급 업체 이름** 및 **30%** 로 입력 합니다.  
  
25. **확인**을 클릭합니다.  
  
26. 일치 프로세스에서 **코드: S1**의 공급자에 대해 하나의 중복 항목을 식별 해야 합니다.  
  
     ![Excel - 일치 결과](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - 일치 결과")  
  
27. **중복 행 (주황)** 을 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 **삭제** 를 클릭 하 여 행을 삭제 합니다.  
  
28. **CLUSTER_ID** 열은 더 이상 필요 하지 않으므로 삭제 합니다.  
  
29. **게시** 를 클릭 하 여 S66 및 **S57** **코드가** 포함 된 다른 두 개의 새 레코드를 MDS에 게시 합니다.  
  
30. **게시 및 주석 달기** 대화 상자에서 **주석을**추가 하 고 **게시**를 클릭 합니다.  
  
31. **마스터 데이터 관리자 웹 응용 프로그램**으로 전환 합니다.  
  
32. 홈 페이지에서 **모델**에 대해 **Suppliers** 를 선택 했는지 확인 하 고 **탐색기**를 클릭 합니다. **탐색기** 가 이미 열려 있는 경우 인터넷 브라우저를 새로 고칩니다.  
  
33. **코드** 를 기준으로 목록을 **정렬** 하 고 **S57** 및 **S66** 를 코드로 사용 하 여 레코드를 찾습니다. 도구 모음의 **필터** 단추를 사용 하 여 목록에서 특정 레코드를 검색할 수도 있습니다.  
  
34. 이제 파일을 저장 하지 않고 **book1.xlsx-Microsoft Excel** 창을 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 5: Excel에서 도메인 기반 특성 만들기](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
