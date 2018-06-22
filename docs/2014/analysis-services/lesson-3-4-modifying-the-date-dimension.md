---
title: Date 차원 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4689d780-4bf6-4cf8-8fde-eb3f15dd668a
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: d4141cd5b26af4c44613b32ddc486154096d3fb6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088728"
---
# <a name="modifying-the-date-dimension"></a>Date 차원 수정
  이 항목의 태스크에서는 사용자 정의 계층을 만들고 Date, Month, Calendar Quarter 및 Calendar Semester 특성에 대해 표시되는 멤버 이름을 변경합니다. 또한 특성에 대한 복합 키를 정의하고 차원 멤버의 정렬 순서를 제어하고 특성 관계도 정의합니다.  
  
## <a name="adding-a-named-calculation"></a>명명된 계산 추가  
 계산 열로 표시되는 SQL 식인 명명된 계산을 데이터 원본 뷰의 테이블에 추가할 수 있습니다. 이 식은 테이블의 열로 나타나고 동작합니다. 명명된 계산을 사용하면 기본 데이터 원본의 테이블을 수정하지 않고 데이터 원본 뷰에서 기존 테이블의 관계형 스키마를 확장할 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
#### <a name="to-add-a-named-calculation"></a>명명된 계산을 추가하려면  
  
1.  **Adventure Works DW 2012** 데이터 원본 뷰를 열려면 솔루션 탐색기의 **데이터 원본 뷰** 폴더에서 해당 뷰를 두 번 클릭합니다.  
  
2.  하단에 있는 **테이블** 창에서 마우스 오른쪽 단추로 클릭 `Date`, 클릭 하 고 **새 명명 된 계산**합니다.  
  
3.  에 **명명 된 계산 만들기** 대화 상자에서 `SimpleDate` 에 **열 이름** 상자의 하 고 다음을 입력 하거나 복사 하 ö ½ à ´ `DATENAME` 의 문에서 **식**  상자:  
  
    ```  
    DATENAME(mm, FullDateAlternateKey) + ' ' +  
    DATENAME(dd, FullDateAlternateKey) + ', ' +  
    DATENAME(yy, FullDateAlternateKey)  
    ```  
  
     `DATENAME` 문은 FullDateAlternateKey 열에서 연도, 월 및 날짜 값을 추출합니다. 이 새 열을 FullDateAlternateKey 특성에 대한 표시 이름으로 사용합니다.  
  
4.  클릭 **확인**을 펼친 다음 `Date` 에 **테이블** 창.  
  
     `SimpleDate` 날짜 테이블의 열 목록에 표시 되는 명명 된 계산 임을 나타내는 아이콘과 함께 명명 된 계산 합니다.  
  
5.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
6.  에 **테이블** 창에서 마우스 오른쪽 단추로 클릭 `Date`, 클릭 하 고 **데이터 탐색**합니다.  
  
7.  오른쪽으로 스크롤하여 **Date 테이블 탐색** 뷰의 마지막 열을 검토합니다.  
  
     에 `SimpleDate` 원래 데이터 원본을 수정 하지 않고 기본 데이터 원본에서 여러 열의 데이터를에서 올바르게 연결한 열 데이터 원본 뷰에 나타납니다.  
  
8.  **Date 테이블 탐색** 뷰를 닫습니다.  
  
## <a name="using-the-named-calculation-for-member-names"></a>멤버 이름에 명명된 계산 사용  
 데이터 원본 뷰에서 명명된 계산을 만든 후에는 이 명명된 계산을 특성의 속성으로 사용할 수 있습니다.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>멤버 이름에 명명된 계산을 사용하려면  
  
1.  **에서 Date 차원에 대한** 차원 디자이너 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 엽니다. 이 작업을 수행 하려면 두 번 클릭은 `Date` 차원에 **차원** 의 노드 **솔루션 탐색기**합니다.  
  
2.  **차원 구조** 탭의 **특성** 창에서 **Date Key** 특성을 클릭합니다.  
  
3.  속성 창이 열려 있지 않으면 속성 창을 열고 제목 표시줄의 **자동 숨기기** 단추를 클릭하여 열린 상태를 유지합니다.  
  
4.  창 아래쪽에서 **NameColumn** 속성 필드를 클릭한 다음 줄임표 단추(**…**)를 클릭하여 **이름 열** 대화 상자를 엽니다.  
  
5.  선택 `SimpleDate` 맨 아래에 **원본 열** 목록으로 이동한 다음 클릭 **확인**합니다.  
  
6.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="creating-a-hierarchy"></a>계층 만들기  
 **특성** 창에서 **계층** 창으로 특성을 끌어 새 계층을 만들 수 있습니다.  
  
#### <a name="to-create-a-hierarchy"></a>계층을 만들려면  
  
1.  **차원 구조** 에 대 한 차원 디자이너의 탭은 `Date` 차원에서 끌어는 **역 년** 에서 특성의 **특성** 창에는 **계층** 창.  
  
2.  끌어서는 **Calendar Semester** 에서 특성의 **특성** 창에는  **\<새 수준 >** 셀에 **계층**창, 아래에서 **역 년** 수준입니다.  
  
3.  끌어서는 **Calendar Quarter** 에서 특성는 **특성** 창에는  **\<새 수준 >** 셀에 **계층**창, 아래에서 **Calendar Semester** 수준입니다.  
  
4.  끌어서는 **English Month Name** 에서 특성의 **특성** 창에는  **\<새 수준 >** 셀에 **계층**창, 아래에서 **Calendar Quarter** 수준입니다.  
  
5.  끌어서는 **Date Key** 에서 특성의 **특성** 창에는  **\<새 수준 >** 셀에 **계층** 창 아래에서 **English Month Name** 수준입니다.  
  
6.  에 **계층** 창의 제목 표시줄을 마우스 오른쪽 단추로 클릭는 **계층** 계층, 편집할 **이름 바꾸기**, 한 다음 입력 `Calendar Date`합니다.  
  
7.  오른쪽 클릭 상황에 맞는 메뉴를 사용 하 여는 `Calendar Date` 계층, 이름 바꾸기는 **English Month Name** 수준을 `Calendar Month`, 선택한 다음 이름을 **Date Key** 수준을 `Date`합니다.  
  
8.  **Full Date Alternate Key** 특성은 사용하지 않으므로 **특성** 창에서 삭제합니다. **개체 삭제** 확인 창에서 **확인** 을 클릭합니다.  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-attribute-relationships"></a>특성 관계 정의  
 기본 데이터가 특성 관계를 지원하는 경우 특성 간의 특성 관계를 정의해야 합니다. 특성 관계를 정의하면 차원, 파티션 및 쿼리 처리가 빨라집니다.  
  
#### <a name="to-define-attribute-relationships"></a>특성 관계를 정의하려면  
  
1.  에 **차원 디자이너** 에 대 한는 `Date` 차원에서 클릭 된 **특성 관계** 탭 합니다.  
  
2.  다이어그램에서 **English Month Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 클릭합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **English Month Name**입니다. **관련 특성** 을 **Calendar Quarter**로 설정합니다.  
  
4.  **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
     멤버 간의 관계는 시간이 지나도 변경되지 않으므로 관계 유형은 **고정** 입니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  다이어그램에서 **Calendar Quarter** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 클릭합니다.  
  
7.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Calendar Quarter**입니다. **관련 특성** 을 **Calendar Semester**로 설정합니다.  
  
8.  **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
9. **확인**을 클릭합니다.  
  
10. 다이어그램에서 **Calendar Semester** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 클릭합니다.  
  
11. **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **Calendar Semester**입니다. **관련 특성** 을 **Calendar Year**로 설정합니다.  
  
12. **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
13. **확인**을 클릭합니다.  
  
14. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="providing-unique-dimension-member-names"></a>고유한 차원 멤버 이름 지정  
 이 태스크에서는 **EnglishMonthName**, **CalendarQuarter**, **CalendarSemester** 특성에서 사용되는 친숙한 이름 열을 만듭니다.  
  
#### <a name="to-provide-unique-dimension-member-names"></a>고유한 차원 멤버 이름을 지정하려면  
  
1.  **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** 데이터 원본 뷰로 전환하려면 솔루션 탐색기의 **데이터 원본 뷰** 폴더에서 해당 뷰를 두 번 클릭합니다.  
  
2.  에 **테이블** 창에서 마우스 오른쪽 단추로 클릭 `Date`, 클릭 하 고 **새 명명 된 계산**합니다.  
  
3.  에 **명명 된 계산 만들기** 대화 상자에서 `MonthName` 에 **열 이름** 상자의 또는 복사 한 후에 다음 문을 붙여는 **식** 상자:  
  
    ```  
    EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)  
    ```  
  
     이 문은 테이블에 있는 월 및 각 월의 연도를 새 열에 연결합니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  에 **테이블** 창에서 마우스 오른쪽 단추로 클릭 `Date`, 클릭 하 고 **새 명명 된 계산**합니다.  
  
6.  에 **명명 된 계산 만들기** 대화 상자에서 `CalendarQuarterDesc` 에 **열 이름** 상자의 및 다음를 입력 하거나 복사한 다음 SQL 스크립트를 붙여는 **식** 상자:  
  
    ```  
    'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY ' +  
    CONVERT(CHAR (4), CalendarYear)  
    ```  
  
     이 SQL 스크립트는 테이블에 있는 분기와 각 분기의 연도를 새 열에 연결합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  에 **테이블** 창에서 마우스 오른쪽 단추로 클릭 `Date`, 클릭 하 고 **새 명명 된 계산**합니다.  
  
9. 에 **명명 된 계산 만들기** 대화 상자에서 `CalendarSemesterDesc` 에 **열 이름** 상자의 및 다음를 입력 하거나 복사한 다음 SQL 스크립트를 붙여는 **식** 상자:  
  
    ```  
    CASE  
    WHEN CalendarSemester = 1 THEN 'H1' + ' ' + 'CY' + ' '   
           + CONVERT(CHAR(4), CalendarYear)  
    ELSE  
    'H2' + ' ' + 'CY' + ' ' + CONVERT(CHAR(4), CalendarYear)  
    END  
    ```  
  
     이 SQL 스크립트는 테이블에 있는 반기와 각 반기의 연도를 새 열에 연결합니다.  
  
10. **확인.**  
  
11. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-composite-keycolumns-and-setting-the-name-column"></a>복합 KeyColumns 정의 및 이름 열 설정  
 **KeyColumns** 속성에는 특성의 키를 나타내는 열이 포함됩니다. 이 태스크에서는 복합 **KeyColumns**를 정의합니다.  
  
#### <a name="to-define-composite-keycolumns-for-the-english-month-name-attribute"></a>English Month Name 특성에 대한 복합 KeyColumns를 정의하려면  
  
1.  Date 차원에 대한 **차원 구조** 탭을 엽니다.  
  
2.  **특성** 창에서 **English Month Name** 특성을 클릭합니다.  
  
3.  **속성** 창에서 **KeyColumns** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
4.  **키 열** 대화 상자의 **사용 가능한 열** 목록에서 **CalendarYear**열을 선택한 후 **>** 단추를 클릭합니다.  
  
5.  **EnglishMonthName** 및 **CalendarYear** 열이 **키 열** 목록에 표시됩니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  **EnglishMonthName** 특성의 **NameColumn** 속성을 설정하려면 속성 창에서 **NameColumn** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
8.  에 **이름 열** 대화 상자는 **원본 열** 목록에서 `MonthName`, 클릭 하 고 **확인**합니다.  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-quarter-attribute"></a>Calendar Quarter 특성에 대한 복합 KeyColumns를 정의하려면  
  
1.  **특성** 창에서 **Calendar Quarter** 특성을 클릭합니다.  
  
2.  **속성** 창에서 **KeyColumns** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
3.  **키 열** 대화 상자의 **사용 가능한 열** 목록에서 **CalendarYear** 열을 선택한 후 **>** 단추를 클릭합니다.  
  
     **CalendarQuarter** 및 **CalendarYear** 열이 **키 열** 목록에 표시됩니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **Calendar Quarter** 특성의 **NameColumn** 속성을 설정하려면 속성 창에서 **NameColumn** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
6.  에 **이름 열** 대화 상자는 **원본 열** 목록에서 `CalendarQuarterDesc`, 클릭 하 고 **확인**합니다.  
  
7.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-semester-attribute"></a>Calendar Semester 특성에 대한 복합 KeyColumns를 정의하려면  
  
1.  **특성** 창에서 **Calendar Semester** 특성을 클릭합니다.  
  
2.  **속성** 창에서 **KeyColumns** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
3.  **키 열** 대화 상자의 **사용 가능한 열** 목록에서 **CalendarYear**열을 선택한 후 **>** 단추를 클릭합니다.  
  
     **CalendarSemester** 및 **CalendarYear** 열이 **키 열** 목록에 표시됩니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **Calendar Semester** 특성의 **NameColumn** 속성을 설정하려면 속성 창에서 **NameColumn** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
6.  에 **이름 열** 대화 상자는 **원본 열** 목록에서 `CalendarSemesterDesc`, 클릭 하 고 **확인**합니다.  
  
7.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="deploying-and-viewing-the-changes"></a>변경 내용 배포 및 표시  
 특성과 계층을 변경한 후에 변경 내용을 표시하려면 먼저 변경 내용을 배포하고 관련 개체를 다시 처리해야 합니다.  
  
#### <a name="to-deploy-and-view-the-changes"></a>변경 내용을 배포하고 표시하려면  
  
1.  **의** 빌드 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  받은 후는 **배포가 완료 되었습니다.** 메시지는 **브라우저** 탭 **차원 디자이너** 에 대 한는 `Date` 차원 및 그런 다음 디자이너 도구 모음에서 다시 연결 단추를 클릭 합니다.  
  
3.  **계층** 목록에서 **Calendar Quarter** 를 선택합니다. **Calendar Quarter** 특성 계층의 멤버를 검토합니다.  
  
     이름으로 사용할 명명된 계산을 만든 덕분에 **Calendar Quarter** 특성 계층의 멤버 이름이 보다 명확하고 알아보기 쉬움을 확인할 수 있습니다. 이제 **Calendar Quarter** 특성 계층에 각 연도의 각 분기에 대한 멤버가 있습니다. 멤버는 시간순으로 정렬되지 않고 분기순으로 정렬된 다음 연도순으로 정렬됩니다. 이 항목의 다음 태스크에서는 이 동작을 수정하여 이 특성 계층의 멤버를 연도순으로 정렬한 다음 분기순으로 정렬합니다.  
  
4.  **English Month Name** 및 **Calendar Semester** 특성 계층의 멤버를 검토합니다.  
  
     이 계층의 멤버도 시간순으로 정렬되지 않고 각각 월이나 반기순으로 정렬된 다음 연도순으로 정렬됩니다. 이 항목의 다음 태스크에서는 이 동작을 수정하여 이 정렬 순서를 변경합니다.  
  
## <a name="changing-the-sort-order-by-modifying-composite-key-member-order"></a>복합 키 멤버 순서를 수정하여 정렬 순서 변경  
 이 태스크에서는 복합 키를 구성하는 키의 순서를 변경하여 정렬 순서를 변경합니다.  
  
#### <a name="to-modify-the-composite-key-member-order"></a>복합 키 멤버 순서를 수정하려면  
  
1.  열기는 **차원 구조** 에 대 한 차원 디자이너의 탭에서 `Date` 차원을 선택한 후 **Calendar Semester** 에 **특성** 창.  
  
2.  속성 창에서 **OrderBy** 속성 값을 검토합니다. **키**로 설정되어 있습니다.  
  
     **Calendar Semester** 특성 계층의 멤버는 키 값을 기준으로 정렬됩니다. 복합 키를 사용하면 멤버 키가 먼저 첫 번째 멤버 키의 값을 기준으로 정렬된 다음 두 번째 멤버 키 값을 기준으로 정렬됩니다. 즉 **Calendar Semester** 특성 계층의 멤버는 먼저 반기순으로 정렬된 다음 연도순으로 정렬됩니다.  
  
3.  속성 창에서 줄임표 단추(**...**)를 클릭하여 **KeyColumns** 속성 값을 변경합니다.  
  
4.  **키 열** 대화 상자의 **키 열** 목록에서 **CalendarSemester** 가 선택되어 있는지 확인한 후 아래쪽 화살표를 클릭하여 이 복합 키 멤버의 순서를 반대로 바꿉니다. **확인**을 클릭합니다.  
  
     이제 특성 계층의 멤버가 연도순으로 정렬된 다음 반기순으로 정렬됩니다.  
  
5.  **특성** 창에서 **Calendar Quarter** 를 선택하고 속성 창에서**KeyColumns**속성의 줄임표 단추( **...** )를 클릭합니다.  
  
6.  **키 열** 대화 상자의 **키 열** 목록에서 **CalendarQuarter** 가 선택되어 있는지 확인한 후 아래쪽 화살표를 클릭하여 이 복합 키 멤버의 순서를 반대로 바꿉니다. **확인**을 클릭합니다.  
  
     이제 특성 계층의 멤버가 연도순으로 정렬된 다음 분기순으로 정렬됩니다.  
  
7.  **특성** 창에서 **English Month Name** 을 선택하고 속성 창에서**KeyColumns**속성의 줄임표 단추( **...** )를 클릭합니다.  
  
8.  **키 열** 대화 상자의 **키 열** 목록에서 **EnglishMonthName** 이 선택되어 있는지 확인한 후 아래쪽 화살표를 클릭하여 이 복합 키 멤버의 순서를 반대로 바꿉니다. **확인**을 클릭합니다.  
  
     이제 특성 계층의 멤버가 연도순으로 정렬된 다음 월순으로 정렬됩니다.  
  
9. **의** 빌드 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다. 배포가 성공적으로 완료 되 면 클릭는 **브라우저** 탭에 대 한 차원 디자이너에는 `Date` 차원입니다.  
  
10. **브라우저** 탭의 도구 모음에서 다시 연결 단추를 클릭합니다.  
  
11. **Calendar Quarter** 및 **Calendar Semester** 특성 계층의 멤버를 검토합니다.  
  
     이 계층의 멤버는 이제 시간순으로 정렬되고 연도순으로 정렬된 다음 각각 분기순이나 반기순으로 정렬됩니다.  
  
12. **English Month Name** 특성 계층의 멤버를 검토합니다.  
  
     이제 계층의 멤버가 연도순으로 정렬된 다음 월 이름의 사전순으로 정렬됩니다. 이는 기본 관계형 데이터베이스의 nvarchar 데이터 형식에 기초하여 데이터 원본 뷰의 EnglishCalendarMonth 열에 대한 데이터 형식이 문자열 열이기 때문입니다. 각 연도 내에서 월을 시간 순으로 정렬하는 방법에 대한 자세한 내용은 [보조 특성을 기준으로 특성 멤버 정렬](lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)을 참조하세요.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [배포된 큐브 찾아보기](lesson-3-5-browsing-the-deployed-cube.md)  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  