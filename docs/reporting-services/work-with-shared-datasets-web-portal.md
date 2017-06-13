---
title: "공유 데이터 집합 작업 (웹 포털) | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2641ea84-9343-4e6f-aec1-25339031b163
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6dfbc134c0f0e351648d19cf8c485fe25a58eb99
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="work-with-shared-datasets---web-portal"></a>공유 데이터 집합-웹 포털 작업

[!INCLUDE[ssrs-appliesto-sql2016-preview](../includes/ssrs-appliesto-sql2016-preview.md)]

공유 데이터 집합을 사용하면 데이터 집합의 설정을, 해당 설정을 사용하는 보고서 및 기타 카탈로그 항목과 별도로 관리할 수 있습니다. 공유 데이터 집합은 KPI와 함께 페이지가 매겨진 모바일 보고서에 사용할 수 있습니다.

웹 포털 내에서 공유 데이터 집합의 속성을 보고 관리할 수 있습니다. 웹 포털에서 공유 데이터집합을 만들거나 편집하도록 보고서 작성기를 시작할 수 있습니다.

## <a name="create-a-shared-dataset"></a>공유 데이터 집합 만들기
  
새 공유 데이터 집합을 만들려면 다음을 수행합니다.  
  
1.  메뉴 모음에서 새로 만들기를 선택합니다.  
  
2.  **데이터 집합**을 선택합니다.  
  
    ![ssRSDataset-NewDataset](../reporting-services/media/ssrsdataset-newdataset.png)  
  
3.  보고서 작성기가 시작되거나 보고서 작성기를 다운로드하라는 메시지가 표시됩니다.  
  
4.  **새 보고서 또는 데이터 집합** 대화 상자에서, 데이터 집합에 사용할 데이터 원본 연결을 선택합니다. 공유 데이터 원본의 위치를 찾아서 선택해야 하는 경우도 있습니다.  
  
5.  **만들기**를 선택합니다.  
  
6.  데이터 집합을 작성한 후 왼쪽 위에 있는 **저장** 아이콘을 선택하여 데이터 집합을 보고서 서버에 다시 저장합니다.  
  
## <a name="manage-an-existing-shared-dataset"></a>기존 공유 데이터 집합 관리
  
기존 공유 데이터 집합을 관리하려면, 다음을 수행합니다.  
  
> [!NOTE]
> 폴더에 공유 데이터 집합이 보이지 않는 경우에는 데이터 집합을 보고 있는지 확인합니다. 웹 포털 오른쪽 위에 있는 메뉴 모음에서 **보기** 를 선택할 수 있습니다. **데이터 집합** 이 선택되어 있는지 확인합니다.  
  
1.  선택 된 **줄임표 (...)**  관리 하려는 데이터 집합에 대 한 합니다.  
  
    ![ssRSDataset-Ellipse](../reporting-services/media/ssrsdataset-ellipse.png)  
  
2.  **관리** 를 선택하여 편집 화면으로 이동합니다.  
  
    ![ssRSDataset-Manage](../reporting-services/media/ssrsdataset-manage.png)  
  
## <a name="properties"></a>속성
  
속성 화면에서 데이터 집합의 **이름** 과 **설명** 을 변경할 수 있습니다. **삭제**, **이동**, **보고서 작성기에서 편집**, **다운로드** 또는 **대체**도 가능합니다.  
  
![ssRSdataset-Properties](../reporting-services/media/ssrsdataset-properties.png)  
  
## <a name="caching"></a>캐싱
  
데이터 집합의 데이터 캐싱에 대한 옵션도 제공됩니다. 간단한 선택부터 시작할 수 있습니다.  
  
1.  **항상 최신 데이터로 이 보고서 실행** 은 요청 시 데이터 원본에 대한 쿼리를 생성합니다.  
  
2.  **이 보고서의 복사본을 캐시하고 사용 가능할 때 사용** 은 데이터 임시 사본을 캐시에 보관하여 이 데이터 집합을 사용하는 항목과 사용할 수 있도록 합니다. 캐시를 사용하면 데이터 집합 쿼리를 다시 실행하지 않고 캐시에서 바로 가져오기 때문에 일반적으로 성능이 향상됩니다.  
  
![ssRSDataset-Caching1](../reporting-services/media/ssrsdataset-caching1.png)  
  
**이 보고서의 복사본을 캐시하고 사용 가능할 때 사용** 을 선택하면 몇 가지 옵션이 더 제공됩니다.  
  
![ssRSDataset-Caching2](../reporting-services/media/ssrsdataset-caching2.png)  
  
### <a name="cache-expiration"></a>캐시 만료  
  
일정 시간이 지난 후에 공유 데이터 집합의 캐시를 만료시킬지 또는 예약을 통해 만료시킬지를 제어할 수 있습니다. 공유 일정을 사용할 수 있습니다.  
  
![ssRSDataset-Caching3](../reporting-services/media/ssrsdataset-caching3.png)  
  
> [!NOTE]
> 만료를 설정하더라도 캐시가 새로 고쳐지지는 않습니다. 캐시 새로 고침 계획이 없는 경우, 데이터 집합을 다음에 실행할 때 데이터가 새로 고쳐집니다.  
  
### <a name="cache-refresh-plans"></a>캐시 새로 고침 계획  
  
캐시 새로 고침 계획을 사용하여 공유 데이터 집합의 데이터 임시 사본으로 캐시를 사전에 로드할 일정을 만들 수 있습니다. 새로 고침 계획에는 일정 및 매개 변수 값을 지정하거나 재정의하는 옵션이 포함됩니다. 읽기 전용으로 표시된 매개 변수의 값은 재정의할 수 없습니다. 새로 고침 계획을 여러 개 만들어 사용할 수 있습니다.   
  
캐시 새로 고침 계획의 공유 데이터 집합을 추가, 삭제, 변경할 수 있는 기본 역할 할당은 내용 관리자, 내 보고서 및 게시자입니다.  
  
위의 캐시 옵션을 적용한 후에 캐시 새로 고침 계획을 정의할 수 있습니다. 그러려면 캐시 설정을 적용한 후에 표시되는 **새로 고침 계획 관리** 링크를 선택합니다. 캐시 새로 고침 계획 페이지가 열립니다.   
  
캐시 계획을 새로 만들려면 **새 캐시 새로 고침 계획**을 선택합니다. 그 다음 계획의 이름을 입력하고 일정을 지정할 수 있습니다. 데이터 집합에 정의된 매개 변수가 있으면 해당 목록이 표시되며, 읽기 전용으로 표시되어 있지 않다면 값을 제공할 수 있습니다.  
  
완료한 후에 **캐시 새로 고침 계획 만들기**를 선택합니다.  
  
![ssRSDataset-Caching4](../reporting-services/media/ssrsdataset-caching4.png)  
  
> [!NOTE]
> 캐시 새로 고침 계획을 만들려면 SQL Server 에이전트를 실행해야 합니다.  
  
그런 다음 나열된 계획을 **편집** 또는 **삭제** 할 수 있습니다. **기존 계획에서 새로 만들기** 옵션은 캐시 새로 고침 계획을 하나 선택한 경우에만 설정됩니다. 이 옵션은 원래 계획에서 복사하여 새로운 새로 고침 옵션을 만듭니다. 캐시 새로 고침 계획 페이지의 정보가 선택한 계획의 정보로 채워져서 열립니다. 그런 다음 새로 고침 계획 옵션을 수정하고 새로운 설명과 함께 계획을 저장할 수 있습니다.  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
