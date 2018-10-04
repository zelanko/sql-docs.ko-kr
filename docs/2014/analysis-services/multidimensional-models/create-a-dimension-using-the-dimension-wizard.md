---
title: 차원 마법사를 사용 하 여 차원 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], creating
ms.assetid: d84f66ae-7551-49bf-99d0-88368ca2dd0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad05272b38a2f3dec72c4be160f48981e4fd43a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118077"
---
# <a name="create-a-dimension-using-the-dimension-wizard"></a>차원 마법사를 사용하여 차원 만들기
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 차원 마법사를 사용하여 새 차원을 만들 수 있습니다.  
  
### <a name="to-create-a-new-dimension"></a>새 차원을 만들려면  
  
1.  **솔루션 탐색기**에서 **차원**을 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다.  
  
2.  차원 마법사의 **생성 방법 선택** 페이지에서 **기존 테이블 사용**을 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  기존 테이블 없이 차원을 만들어야 하는 경우도 있습니다. 자세한 내용은 [데이터 원본에 시간이 아닌 테이블을 생성하여 차원 만들기](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) 및 [시간 테이블을 생성하여 시간 차원 만들기](create-a-time-dimension-by-generating-a-time-table.md)를 참조하세요.  
  
3.  **원본 정보 지정** 페이지에서 다음 절차를 수행합니다.  
  
    1.  **데이터 원본 뷰** 목록에서 데이터 원본 뷰를 선택합니다.  
  
    2.  **주 테이블** 목록에서 주 차원 테이블을 선택합니다.  
  
    3.  **키 열** 목록에서 주 차원 테이블에 정의된 기본 키에 따라 자동으로 선택된 키 열을 검토합니다. 이 기본 설정을 변경하려면 차원 테이블을 팩트 테이블에 연결하는 키 열을 지정합니다.  
  
    4.  **이름 열** 드롭다운 목록에서 자동으로 선택된 이름 열을 검토합니다.  
  
         이 기본 이름은 열에 설명 정보가 포함된 경우에 적합합니다. 그러나 최종 사용자에게 보다 의미 있는 가치를 포함하는 이름을 지정할 수도 있습니다. 예를 들어 Products 차원에 있는 제품 범주 특성의 키 열로 **ProductCategoryKey** 열이 사용되면 **ProductCategoryName** 열을 해당 이름 열로 지정할 수 있습니다.  
  
         **키 열** 목록에 키 열이 여러 개 있는 경우 키 특성에 대한 멤버 값을 제공하는 이름 열을 지정해야 합니다. 이를 위해 데이터 원본 뷰에서 명명된 계산을 만들고 이를 이름 열로 사용할 수 있습니다.  
  
    5.  **다음**을 클릭합니다.  
  
4.  **관련 테이블 선택** 페이지에서 차원에 포함시킬 관련 테이블을 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  지정된 주 차원 테이블에 다른 차원 테이블에 대한 관계가 있을 경우 **관련 테이블 선택** 페이지가 나타납니다.  
  
5.  **차원 특성 선택** 페이지에서 차원에 포함시킬 특성을 선택한 후 **다음**을 클릭합니다.  
  
     필요에 따라 특성 이름을 변경하고 찾아보기를 설정 또는 해제하며 특성 유형을 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  특성의 **찾아보기 사용** 및 **특성 유형** 필드를 활성화하려면 차원에 포함시킬 특성 이름을 선택해야 합니다.  
  
6.  **계정 인텔리전스 정의** 페이지의 **기본 제공 계정 유형** 열에서 계정 유형을 선택한 후 **다음**을 클릭합니다.  
  
     계정 유형은 **원본 테이블 계정 유형** 열에 나열된 원본 테이블의 계정 유형에 대응해야 합니다.  
  
    > [!NOTE]  
    >  **계정 인텔리전스 정의** 페이지는 마법사의 **차원 특성 선택** 페이지에서 **계정 유형** 차원 특성을 정의한 경우에 나타납니다.  
  
7.  **마법사 완료** 페이지에서 새 차원의 이름을 입력하고 차원 구조를 검토합니다. 변경하려면 **뒤로**를 클릭하고 변경하지 않으려면 **마침**을 클릭합니다.  
  
    > [!NOTE]  
    >  차원 마법사를 완료한 후에는 차원 디자이너를 사용하여 차원의 특성과 계층을 추가, 제거 및 구성할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [기존 테이블을 사용하여 차원 만들기](create-a-dimension-by-using-an-existing-table.md)  
  
  
