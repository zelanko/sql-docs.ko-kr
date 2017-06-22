---
title: "연습: 데이터베이스 다이어그램 추가 및 변경 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2c1a211f11917f54f0f2c69bd2d1b96034cba41
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>연습: 데이터베이스 다이어그램 추가 및 변경
이 연습에서는 데이터베이스 다이어그램을 만들고 수정하는 방법과 데이터베이스 다이어그램 구성 요소를 통해 데이터베이스를 변경하는 방법을 설명합니다. 또한 다이어그램에 테이블을 추가하고, 테이블 간에 관계를 만들고, 열에 대해 제약 조건과 인덱스를 만들며 각 테이블에 대해 표시할 정보 수준을 변경하는 방법을 설명합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 연습을 완료하려면 다음이 필요합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 예제 데이터베이스를 포함하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] 에 대한 액세스 권한  
  
-   데이터베이스 소유자 **dbo** 권한이 있는 계정  
  
> [!NOTE]  
> 충분한 권한이 없는 계정을 사용하여 테이블을 변경하려고 시도하면 오류 메시지가 나타납니다.  
  
## <a name="creating-a-diagram"></a>다이어그램 만들기  
  
#### <a name="to-create-a-new-database-diagram"></a>새 데이터베이스 다이어그램을 만들려면  
  
1.  **보기** 메뉴에서 **개체 탐색기**를 클릭합니다.  
  
2.  데이터베이스 노드를 연 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] 노드를 엽니다.  
  
3.  데이터베이스 다이어그램 노드를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스 다이어그램**을 선택합니다.  
  
    데이터베이스에 다이어그램을 만드는 데 필요한 개체가 없는 경우에는 다음과 같은 메시지가 나타납니다. **이 데이터베이스에는 데이터베이스 다이어그램을 사용하는 데 필요한 지원 개체가 하나 이상 없습니다. 지원 개체를 만드시겠습니까?**라는 메시지가 나타납니다. **예**를 선택합니다.  
  
    **테이블 추가** 대화 상자가 표시됩니다.  
  
4.  **AddressType (Person)** 및 **Address (Person)** 를 선택하고 **추가**를 클릭합니다.  
  
    다이어그램에 두 개의 테이블이 추가됩니다.  
  
5.  **테이블 추가** 대화 상자를 닫습니다.  
  
#### <a name="to-view-different-column-data"></a>서로 다른 열 데이터를 보려면  
  
1.  `Address` 테이블을 마우스 오른쪽 단추로 클릭합니다. 바로 가기 메뉴에서 **테이블 뷰**를 가리킨 다음 **표준**을 클릭합니다.  
  
    테이블 표에 **열 이름**, **데이터 형식**및 **Null 허용**의 세 열이 표시됩니다.  
  
2.  `Address` 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 뷰** 를 클릭한 다음 **키**를 선택합니다.  
  
    테이블 표에 테이블 열 이름이 있는 하나의 열이 표시됩니다. 이때 인덱스에 참여하는 열만 나타납니다.  
  
## <a name="creating-new-tables"></a>새 테이블 만들기  
  
#### <a name="to-create-tables-within-diagram-designer"></a>다이어그램 디자이너 내에서 테이블을 만들려면  
  
1.  기존 테이블 외부에서 다이어그램 디자이너를 마우스 오른쪽 단추로 클릭한 다음 **새 테이블**을 선택합니다.  
  
2.  **이름 선택** 대화 상자에서 **확인** 을 클릭하여 기본 이름인 **Table1**을 적용합니다.  
  
    새 테이블 표에 **열 이름**, **데이터 형식**및 **Null 허용**의 세 열이 나타납니다.  
  
3.  **Table1**에 다음 정보를 추가합니다.  
  
    |**열 이름**|**데이터 형식**|**Null 허용**|  
    |-------------------|-----------------|-------------------|  
    |**T1col1**|**int**|선택|  
    |**T1col2**|**varchar(50)**|선택|  
    |**T1col3**|**float**|선택|  
  
4.  `T1col1` 을 마우스 오른쪽 단추로 클릭한 다음 **기본 키 설정**을 선택합니다.  
  
    열 이름 옆에 키 아이콘이 나타납니다.  
  
5.  **파일** 메뉴에서 **Diagram1 저장**을 클릭합니다.  
  
6.  **이름 선택** 대화 상자에서 **확인** 을 클릭하여 기본 이름인 **Diagram1**을 적용합니다.  
  
7.  **을 데이터베이스에 저장한다는 메시지가 포함된** 저장 `Table1` 대화 상자가 나타납니다. **예**를 클릭합니다.  
  
## <a name="modifying-table-structure"></a>테이블 구조 수정  
다이어그램 디자이너에서 CHECK 제약 조건을 추가하고 테이블 간에 관계를 만들 수 있습니다.  
  
#### <a name="to-create-check-constraints"></a>CHECK 제약 조건을 만들려면  
  
1.  `Table1`에서 `T1col3` 행을 마우스 오른쪽 단추로 클릭한 다음 **CHECK 제약 조건**을 선택합니다.  
  
    **CHECK 제약 조건** 대화 상자가 나타납니다.  
  
2.  **추가**를 클릭합니다.  
  
    **선택한 CHECK 제약 조건** 목록에 새 제약 조건은 기본 이름인 `CK_Table1`로 나타납니다.  
  
3.  표에서 **식** 행을 선택하고 줄임표 단추를 클릭합니다.  
  
    **CHECK 제약 조건 식** 대화 상자가 나타납니다.  
  
4.  **T1col3 > 5**를 입력하고 **확인**을 클릭합니다.  
  
    `Table1` 이제 `T1col3` 에 입력하는 모든 값이 5보다 커야 한다는 제약 조건이 지정됩니다.  
  
5.  **닫기**를 클릭합니다.  
  
#### <a name="to-create-relationships-between-tables"></a>테이블 간에 관계를 만들려면  
  
1.  다이어그램 디자이너에서 다음 열이 있는 `Table2` 라는 새 테이블을 만듭니다.  
  
    |**열 이름**|**데이터 형식**|**Null 허용**|  
    |-------------------|-----------------|-------------------|  
    |**T2col1**|**int**|선택 안 함|  
    |**T2col2**|**varchar(50)**|선택|  
    |**T2col3**|**xml**|선택|  
  
    > [!NOTE]  
    > 외래 키 관계의 기본 키 쪽에 있는 열은 기본 키나 UNIQUE 제약 조건에 참여해야 합니다.  
  
2.  `T2col1` 을 `T1col1`로 끕니다.  
  
    백그라운드의 **외래 키 관계** 대화 상자와 포그라운드의 **테이블 및 열** 대화 상자 두 개가 나타납니다.  
  
3.  **확인** 을 클릭하여 새 관계를 저장합니다.  
  
4.  **확인** 을 다시 클릭합니다.  
  
## <a name="creating-indexes"></a>인덱스 만들기  
XML을 포함하여 대부분의 데이터 형식에 대해 인덱스를 만들 수 있습니다.  
  
#### <a name="to-create-a-standard-index"></a>표준 인덱스를 만들려면  
  
1.  `Table1` 을 마우스 오른쪽 단추로 클릭한 다음 **인덱스/키**를 선택합니다.  
  
    **인덱스/키** 대화 상자가 나타납니다.  
  
2.  **추가**를 클릭합니다.  
  
    **선택한 Primary/Unique 키 또는 인덱스** 목록에 새 인덱스가 `IX_Table1`과 비슷한 기본 이름으로 나타납니다.  
  
3.  **열** 행을 선택하고 줄임표 단추를 클릭합니다.  
  
    **인덱스 열** 대화 상자가 나타납니다.  
  
4.  **열 이름** 아래의 드롭다운 화살표를 클릭하고 `T1col2`를 선택합니다.  
  
    > [!NOTE]  
    > `T1col2` 아래의 셀을 선택하고 다른 열 이름을 선택하여 이 인덱스에 열을 추가할 수 있습니다.  
  
5.  **확인** 을 클릭하여 이 인덱스를 저장합니다.  
  
6.  **인덱스/키** 대화 상자에서 **닫기** 를 클릭합니다.  
  
#### <a name="to-create-an-xml-index"></a>XML 인덱스를 만들려면  
  
1.  `T2col1` 을 마우스 오른쪽 단추로 클릭한 다음 **기본 키 설정**을 선택합니다.  
  
    > [!NOTE]  
    > XML 인덱스를 추가하려면 테이블의 다른 열을 클러스터형 기본 키로 설정해야 합니다.  
  
2.  `T2col3` 의 `Table2` 행을 마우스 오른쪽 단추로 클릭한 다음 **XML 인덱스**를 선택합니다.  
  
    **XML 인덱스** 대화 상자가 나타납니다.  
  
3.  **추가**를 클릭합니다.  
  
    **선택한 XML 인덱스** 목록에 기본값이 지정된 XML 인덱스가 추가됩니다.  
  
4.  **닫기**를 클릭합니다.  
  
    > [!NOTE]  
    > XML 인덱스는 열별로 생성됩니다. 첫 번째 XML 인덱스는 기본 인덱스이고 추가 인덱스는 모두 보조 인덱스입니다.  
  
## <a name="saving-the-diagram"></a>다이어그램 저장  
저장하기 전까지는 다이어그램에 대한 변경 내용이 데이터베이스에 게시되지 않습니다. 문제 또는 충돌이 있을 경우 대화 상자에 추가 정보가 나타납니다.  
  
#### <a name="to-save-a-database-diagram"></a>데이터베이스 다이어그램을 저장하려면  
  
1.  **파일** 메뉴에서 **Diagram1 저장**을 선택합니다.  
  
    **저장** 대화 상자가 나타납니다. **영향을 받는 테이블 경고** 를 선택하면 새 테이블이나 변경된 테이블에 대한 정보가 표시됩니다.  
  
2.  **확인**을 클릭합니다.  
  
3.  오류가 발생하면 **저장 후 알림** 대화 상자에 오류와 원인이 나타납니다. 오류를 수정하고 다이어그램을 다시 저장합니다.  
  
## <a name="next-steps"></a>다음 단계  
이는 기존 테이블 두 개와 새 테이블 두 개만으로 이루어진 기본 다이어그램이지만 이 다이어그램을 만들어본 사용자라면 시각적으로 새 스키마를 만들거나 기존 데이터베이스를 다이어그램으로 만들 수 있습니다. 다음을 추가로 살펴볼 수 있습니다.  
  
-   관련 테이블 그룹을 포함하는 새 다이어그램 만들기  
  
-   각 테이블에 대해 표시되는 정보의 양 사용자 지정  
  
-   레이아웃 변경 및 주석 추가  
  
-   비트맵으로 다이어그램 복사  
  
## <a name="see-also"></a>참고 항목  
[다이어그램에 표시된 정보의 양 사용자 지정&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)  
[데이터베이스 다이어그램 디자이너 설정&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
[다이어그램에 테이블 추가&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
[다이어그램에서 테이블 간의 관계 만들기&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/create-relationships-between-tables-on-a-diagram-visual-database-tools.md)  
[XML 인덱스 만들기](http://msdn.microsoft.com/en-us/6ecac598-355d-4408-baf7-1b2e8d4cf7c1)  
[데이터베이스 다이어그램의 이미지를 클립보드로 복사&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)  
[다이어그램 레이아웃 작업&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  

