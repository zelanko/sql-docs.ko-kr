---
title: '태스크 4(선택 사항): 결합, 일치 및 새 데이터 집합이 게시 | Microsoft Docs'
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489276"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>태스크 4(선택 사항): 새 데이터 세트 결합, 일치 및 게시
  시간이 지날수록 MDS 저장소에 추가하는 데이터가 늘어나게 됩니다. 데이터를 추가 하기 전에 새 데이터 중복 되거나 정확 하지 않은 데이터를 추가 하지 않는 되도록 MDS에서 이미 관리 되는 데이터를 비교할 때 유용 수 있습니다. Excel용 Master Data Services 추가 기능에서는 데이터를 MDS에 게시하기 전에 두 워크시트의 데이터를 결합하고 데이터를 비교해서 중복된 항목을 식별하고 제거할 수 있습니다. MDS Excel 추가 기능의 일치 기능에는 데이터에서 일치 항목을 식별하기 위해 DQS 일치 기능이 사용됩니다. 이 작업에서는 MDS에 데이터를 게시하기 전에 두 워크시트의 데이터를 하나로 결합한 후 일치 작업을 수행해서 중복된 항목을 식별하고 제거합니다. 참조 [MDS 추가 기능에서 Excel 용 데이터 품질 일치](https://msdn.microsoft.com/library/hh548681.aspx) 하 고 [데이터 결합](https://msdn.microsoft.com/library/hh548680.aspx) 자세한 세부 정보에 대 한 항목입니다.  
  
1.  새 인스턴스를 시작할 **Excel**합니다. 클릭 **시작**, 가리킨 **실행**, 형식 **Excel**를 클릭 하 고 **확인**합니다.  
  
2.  으로 전환 합니다 **마스터 데이터** 탭을 클릭 하 여 **마스터 데이터** 메뉴 모음에서.  
  
3.  클릭 **Connect** 리본의 **연결 및 로드** 그룹에 연결 하는 **MDS 서버**합니다. 이 연결은 이 단원의 앞 부분에서 구성했습니다.  
  
     ![Excel-마스터 데이터 탭의 탐색기 단추를 보여 줍니다](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel-마스터 데이터 탭의 탐색기 단추를 표시 합니다.")  
  
4.  표시 되어야 합니다 **마스터 데이터 탐색기** 오른쪽에 있는 창입니다. 마스터 데이터 탐색기에 표시 되지 않으면, 클릭 **탐색기 표시** 리본의 단추입니다.  
  
5.  에 **마스터 데이터 탐색기** 창에서 **Suppliers** 드롭 다운 목록에서를 **모델**합니다. 모델 엔터티 하나에 표시 됩니다. **공급 업체**합니다.  
  
     ![Excel-마스터 데이터 탐색기 창](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel-마스터 데이터 탐색기 창")  
  
6.  두 번 클릭 **공급 업체** 엔터티 멤버를 Excel 워크시트로 로드 하려면 엔터티 목록에서.  
  
7.  클릭 **Sheet2** 전환 하려면 맨 아래에 **Sheet2** 탭 합니다. 표시 되지 않으면 **Sheet2**를 새 워크시트를 추가 합니다.  
  
8.  오픈 **Suppliers.xls** (원래 입력된 파일 자습서 파일에 포함 된) 파일과의 (3) 모든 행을 복사 합니다 **CombineAndCleanse** 워크시트 **Sheet2**합니다.  
  
9. 으로 전환 합니다 **공급 업체** 에서 시트를 **Book 1-Microsoft Excel** (하지를 **Cleansed and Matched Supplier List** Excel)에 연결 된 **MDS**.  
  
10. 메뉴 모음에서 **마스터 데이터** 를 클릭합니다.  
  
11. 클릭 **데이터 결합** 리본 메뉴에 있습니다. 표시 됩니다는 **데이터 결합** 대화 상자.  
  
12. 에 **데이터 결합** 대화 상자에서 다음 단추를 클릭 **MDS 데이터와 결합할 범위** 다음 이미지와 같이 텍스트 상자입니다.  
  
     ![Excel-데이터 결합 대화 상자](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel-데이터 결합 대화 상자")  
  
13. 지금은 대화 상자가 축소된 상태로 표시됩니다. 이제 클릭 **Sheet2** 으로 전환 합니다 **Sheet2** 4 개의 행 (하나의 머리글 행 포함)를 사용 하 여 새로운 공급자 데이터가 있는 탭입니다.  
  
14. 에 **Sheet2**를 선택 **머리글 행을 포함 한 모든 행** (보이는 경우에 이미 선택). 표시 되어야 합니다 **MDS 데이터와 결합할 범위** 자동으로 업데이트 됩니다.  
  
     ![Excel-데이터 결합 대화 상자-최소화](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel-데이터 결합 대화 상자-최소화")  
  
15. 으로 전환 합니다 **공급 업체** 닫지 않고 탭을 **데이터 결합** 대화 상자.  
  
16. 클릭 합니다 **단추** 옆에 **텍스트 상자**합니다. 이제 대화 상자가 확장된 상태로 표시됩니다. 열 사이의 모든 매핑이 표시 됩니다는 **공급 업체** MDS **엔터티** 하 **Excel** 열은 자동으로 채워집니다.  
  
     ![Excel-데이터 결합 대화 상자 데이터로 채워진](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel-데이터로 채워진 데이터 대화 상자를 결합 합니다.")  
  
17. 있는지 확인 **코드** 엔터티 열에 매핑되는 **SupplierID** 워크시트의 열 및 **우편** 엔터티 열에 매핑되는 **우편** 워크시트의 열입니다.  
  
18. 에 **데이터 결합** 대화 상자, 클릭 **결합**합니다.  
  
19. 세 개의 데이터 행이 워크시트 하단에 추가되었고 색상으로 표시되었는지 확인합니다.  
  
     ![Excel-결합 후 새 요소](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel-결합 후 새 요소")  
  
20. 클릭 **수학 데이터** 중복 항목을 식별 하려면 리본 메뉴에 있습니다. 이 기능은 DQS의 일치 기능을 사용합니다.  
  
21. 에 **데이터 일치** 대화 상자에서 **Suppliers** 에 대 한 **DQS 기술 자료**합니다.  
  
     ![Excel-데이터 일치 대화 상자](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel-데이터 일치 대화 상자")  
  
22. 다음 표에 표시된 대로 워크시트 열을 도메인에 매핑합니다.  
  
    |워크시트 열|도메인|  
    |----------------------|------------|  
    |Code(MDS에서 Supplier 엔터티에 대한 Code로 업로드한 Supplier ID)|Supplier ID|  
    |Name(MDS에 Supplier 엔터티에 대한 이름으로 업로드한 Supplier Name)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. 선택 **필수 구성 요소** 에 대 한 합니다 **코드** 열 매핑.  
  
24. 입력 **70%** 으로 **가중치** 에 대 한 **Supplier Name** 고 **30%** 로 **가중치** 에대한**Contact Email** 이미지에 표시 된 대로 합니다.  
  
25. **확인**을 클릭합니다.  
  
26. 일치 하는 과정을 가진 공급 업체에 대 한 중복 항목이 하나 식별 해야 **코드: S1**.  
  
     ![Excel-일치 결과](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel-일치 결과")  
  
27. 선택 된 **중복 행 (주황색)** 를 마우스 오른쪽 단추로 클릭 하 고 **삭제** 행을 삭제 합니다.  
  
28. 삭제 된 **CLUSTER_ID** 더 이상 필요 하지 않으므로 열입니다.  
  
29. 클릭 **게시** 다른 두 개의 새 레코드를 사용 하 여 게시할 **Codes S66** 하 고 **S57** MDS에 있습니다.  
  
30. 에 **게시 및 주석** 대화 상자에서 추가 **주석**, 클릭 **게시**합니다.  
  
31. 으로 전환 합니다 **마스터 데이터 관리자 웹 응용 프로그램**합니다.  
  
32. 홈 페이지에서 있는지 확인 합니다 **공급 업체** 가 선택 합니다 **모델**, 클릭 **탐색기**합니다. 이미 있는 경우는 **탐색기** 엽니다, 인터넷 브라우저를 새로 고칩니다.  
  
33. **정렬** 별로 목록을 **코드** 사용 하 여 레코드를 찾아서 **S57** 하 고 **S66** 코드로 합니다. 사용할 수도 있습니다는 **필터** 모음의 목록에서 특정 레코드를 검색 합니다.  
  
34. 이제 닫습니다 **Book1-Microsoft Excel** 파일을 저장 하지 않고 창입니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 5: Excel에서 도메인 기반 특성 만들기](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
