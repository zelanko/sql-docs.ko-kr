---
title: MDS에서 Excel로 데이터 로드 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbe1188773d0770ff345cd54ea47e03a3c05555f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482711"
---
# <a name="load-data-from-mds-into-excel"></a>MDS에서 Excel로 데이터 로드
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]에서 데이터를 사용 하려면 MDS 저장소에서 데이터를 로드 해야 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]합니다.  
  
 로드 하기 전에 데이터 집합을 필터링 하려는 경우에는 [&#40;Excel용 MDS 추가 기능&#41;를 로드 하기 전에 데이터 필터링](filter-data-before-exporting-mds-add-in-for-excel.md) 을 참조 하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   
  **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
### <a name="to-load-data-from-mds-into-excel"></a>MDS에서 Excel로 데이터를 로드하려면  
  
1.  Excel을 열고 **마스터 데이터** 탭에서 MDS 저장소에 연결합니다. 자세한 내용은 [MDS 리포지토리에 연결&#40;Excel용 MDS 추가 기능&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)을 참조하세요.  
  
2.  
  **마스터 데이터 탐색기** 창에서 모델 및 버전을 선택합니다. 엔터티 목록이 채워집니다.  
  
    -   
  **마스터 데이터 탐색기** 창이 표시되지 않으면 **연결 및 로드** 그룹에서 **탐색기 표시**를 클릭합니다.  
  
    -   
  **마스터 데이터 탐색기** 창이 해제되어 있으면 기존 시트에 이미 MDS 관리 데이터가 포함되어 있기 때문입니다. 창을 활성화하려면 새 워크시트를 엽니다.  
  
3.  
  **마스터 데이터 탐색기** 창의 엔터티 목록에서 로드할 엔터티를 두 번 클릭합니다.  
  
    > [!NOTE]  
    >  -   처음 100만 개의 멤버만 Excel에 로드됩니다. 로드하기 전에 목록을 필터링하려면 리본의 **연결 및 로드** 그룹에서 **필터**를 클릭합니다.  
    > -   제약된 목록(도메인 기반 특성)의 열에는 처음 25,000개의 값만 로드됩니다. 이 숫자는 Excel이 설치된 컴퓨터에 있는 excelusersettings.config 파일의 MaximumDbaEntitySize 속성에서 변경할 수 있습니다. 이 파일은 C:\Users\\<USER\>\AppData\Local\Microsoft\Microsoft SQL Server\120\MasterDataServices\\에 있습니다.  
  
    > [!NOTE]  
    >  32비트 Excel에서 Microsoft Excel용 추가 기능을 사용하여 텍스트 구분 데이터를 로드하면 **로드할 셀 개** 및 **게시할 셀 개수** 속성에 대한 설정이 모두 최대값 1000으로 설정되어 메모리 부족 오류가 발생합니다. 
  **로드할 셀 개수** 및 **게시할 셀 개수**에 대한 최대값 설정을 사용하려면 64비트 Excel을 사용해야 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [Excel의 데이터를 MDS &#40;Excel용 MDS 추가 기능에 게시&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 &#40;Excel용 MDS 추가 기능&#41;로드](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [필터 대화 상자 &#40;Excel용 MDS 추가 기능&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [데이터 &#40;Excel용 MDS 추가 기능&#41;게시](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
