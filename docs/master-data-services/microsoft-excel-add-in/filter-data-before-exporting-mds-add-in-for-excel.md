---
title: "Filter Data before Exporting (MDS Add-in for Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Filter Data before Exporting (MDS Add-in for Excel)
   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], 크기 또는 Excel로 내보내는 데이터의 범위를 제한 하려는 경우 데이터를 필터링 합니다.  
  
## 필수 구성 요소  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
### 내보내기 전에 데이터를 필터링 하려면  
  
1.  Excel을 열고 **마스터 데이터** 탭에서 MDS 저장소에 연결합니다. 자세한 내용은 참조 [MDS 저장소 & #40;에 연결 MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)합니다.  
  
2.  **마스터 데이터 탐색기** 창에서 모델 및 버전을 선택합니다. 엔터티 목록이 채워집니다.  
  
    -   **마스터 데이터 탐색기** 창이 표시되지 않으면 **연결 및 로드** 그룹에서 **탐색기 표시**를 클릭합니다.  
  
    -   하는 경우는 **마스터 데이터 탐색기** 기존 시트에는 이미 MDS 관리 데이터가 포함 되므로, 창이 표시 되지 않습니다. 창을 활성화하려면 새 워크시트를 엽니다.  
  
3.  **마스터 데이터 탐색기** 창의 엔터티 목록에서 필터링하려는 엔터티를 클릭합니다.  
  
4.  리본 메뉴의 **연결 및 로드** 그룹에서 **필터**를 클릭합니다.  
  
5.  완료는 **필터** 대화 상자를 표시 하는 특성 (열)을 선택 하 여는 열의 순서를 설정 하 고 필요한 경우 더 적은 행이 반환 되도록 데이터를 필터링 합니다. **요약** 창에서 반환된 데이터의 양을 확인합니다. 자세한 내용은 참조 [필터 대화 상자 및 #40; MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)합니다.  
  
6.  **데이터 로드**를 클릭합니다. 시트에 MDS 관리 데이터가 채워집니다.  
  
    > [!NOTE]  
    >  -   처음 100만 개의 멤버만 Excel에 로드됩니다.  
    > -   제약된 목록(도메인 기반 특성)의 열에는 기본적으로 처음 25000개의 값만 로드됩니다.  
  
## 다음 단계  
 [Excel에서 Master Data Services & #40;로 데이터 가져오기 MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## 참고 항목  
 [개요: Excel & #40; 데이터 내보내기 MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [필터 대화 상자 및 #40입니다. MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [열 순서 바꾸기 & #40입니다. MDS 추가 기능에서 Excel 및 #41;에 대 한](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  