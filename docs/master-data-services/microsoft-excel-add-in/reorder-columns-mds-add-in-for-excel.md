---
title: "열 순서 바꾸기(Excel용 MDS 추가 기능) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 열 순서 바꾸기(Excel용 MDS 추가 기능)
  에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], 를 로드 하기 전에 목록을 필터링 하 여 열 순서를 바꿀 수 있습니다.  
  
 **필터** 대화 상자에서 특성의 순서를 조정하면 데이터가 새 순서로 Excel에 로드됩니다. 하지만 다음에 특성 데이터를 필터링하면 순서가 원래 디자인된 순서로 되돌아갑니다. 순서를 영구적으로 변경하려면 관리자가 마스터 데이터 관리자의 **시스템 관리** 영역에서 순서를 변경해야 합니다. 자세한 내용은 [Change the Order of Attributes](../../master-data-services/change-the-order-of-attributes.md)을 참조하세요.  
  
## 필수 구성 요소  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
### MDS 관리 열의 순서를 바꾸려면  
  
1.  Excel을 열고 **마스터 데이터** 탭에서 MDS 저장소에 연결합니다. 자세한 내용은 참조 [MDS 저장소 & #40;에 연결 MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)합니다.  
  
2.  **마스터 데이터 탐색기** 창에서 모델 및 버전을 선택합니다. 엔터티 목록이 채워집니다.  
  
    -   **마스터 데이터 탐색기** 창이 표시되지 않으면 **연결 및 로드** 그룹에서 **탐색기 표시**를 클릭합니다.  
  
    -   하는 경우는 **마스터 데이터 탐색기** 기존 시트에는 이미 MDS 관리 데이터가 포함 되므로, 창이 표시 되지 않습니다. 창을 활성화하려면 새 워크시트를 엽니다.  
  
3.  **마스터 데이터 탐색기** 창에서 엔터티를 클릭합니다.  
  
4.  **연결 및 로드** 그룹에서 **필터**를 클릭합니다.  
  
5.  **필터** 대화 상자의 **열** 섹션에 있는 특성 목록에서 이동하려는 특성을 클릭합니다.  
  
6.  목록 오른쪽에서 **위쪽** 또는 **아래쪽** 화살표를 클릭하여 워크시트에서 특성을 왼쪽 및 오른쪽으로 이동합니다.  
  
7.  워크시트에서 원하는 왼쪽-오른쪽 순서에 맞게 위쪽-아래쪽 순서가 정렬될 때까지 각 특성에 대해 7단계를 반복합니다.  
  
8.  **데이터 로드**를 클릭합니다. 시트에 MDS 관리 데이터가 채워지고 사용자가 지정한 순서에 따라 열이 표시됩니다.  
  
## 참고 항목  
 [개요: Excel & #40; 데이터 내보내기 MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  