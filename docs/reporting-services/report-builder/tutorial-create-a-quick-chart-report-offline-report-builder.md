---
title: "자습서:에서 빠른 차트 보고서 만들기 오프 라인 (보고서 작성기) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
caps.latest.revision: 31
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a09ebdeda6679c80f3eb32602d38068114e7bf36
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---

# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>자습서: 오프라인에서 빠른 차트 보고서 만들기(보고서 작성기)

  이 자습서에서는 마법사를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]의 페이지가 매겨진 보고서로 원형 차트를 만듭니다. 그런 다음 백분율을 추가하고 원형 차트를 약간 수정합니다. 
  
이 자습서는 다음 두 가지 방법으로 진행할 수 있습니다. 두 방법 모두 결과는 동일하며 이 그림의 원형 차트와 같은 원형 차트가 만들어집니다.  
  
 ![보고서 작성기 빠른 원형 차트](../../reporting-services/report-builder/media/report-builder-quick-pie-chart.png "빠른 원형 차트 보고서 작성기")  
  
## <a name="prerequisites"></a>필수 구성 요소  
 XML 데이터를 사용 하 든 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리, 보고서 작성기에 대 한 액세스 하도록 해야 합니다. [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 보고서 서버에서 기본 모드 또는 SharePoint 통합 모드로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 시작하거나 Microsoft 다운로드 센터에서 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 를 다운로드할 수 있습니다. 자세한 내용은 [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md)를 참조하세요.  
  
##  <a name="TwoWays"></a> 이 자습서에서 수행하는 두 가지 방법  
  
-   [XML 데이터로 원형 차트 만들기](#CreatePieChartXML)  
  
-   [데이터를 포함 하는 TRANSACT-SQL 쿼리로 원형 차트 만들기](#CreatePieQueryData)  
  
### <a name="using-xml-data-for-this-tutorial"></a>이 자습서에서 XML 데이터 사용  
 이 항목에서 복사한 XML 데이터를 사용하여 마법사에 붙여 넣을 수 있습니다. 에 연결할 필요가 없습니다는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버가 기본 모드 또는 SharePoint 통합 모드 및 SQL Server의 인스턴스에 대 한 액세스를 필요 하지 않습니다.  
  
 [XML 데이터로 원형 차트 만들기](#CreatePieChartXML)  
  
### <a name="using-a-includetsqlincludestsql-mdmd-query-that-contains-data-for-this-tutorial"></a>이 자습서의 데이터가 포함된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 사용  
 이 항목에서 데이터가 포함된 쿼리를 복사하여 마법사에 붙여 넣을 수 있습니다. 이름이 필요 합니다는 자격 증명 및 SQL Server 인스턴스의 모든 데이터베이스에 대 한 읽기 전용 액세스에 대 한 충분 한 합니다. 자습서의 데이터 집합 쿼리에서 리터럴 데이터를 사용 하지만 쿼리는 보고서 데이터 집합에 필요한 메타 데이터를 반환 하도록 SQL Server의 인스턴스에서 처리 해야 합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하는 경우 이점은 나머지 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 자습서에서도 동일한 방법을 사용하기 때문에 다른 자습서를 이용하는 방식을 미리 알 수 있다는 점입니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하려면 몇 가지 다른 필수 구성 요소가 있어야 합니다. 자세한 내용은 [자습서의 사전 요구 사항 &#40;보고서 작성기&#41;](../../reporting-services/prerequisites-for-tutorials-report-builder.md)를 참조하세요.  
  
 [데이터를 포함 하는 TRANSACT-SQL 쿼리로 원형 차트 만들기](#CreatePieQueryData)  
  
##  <a name="CreatePieChartXML"></a> XML 데이터로 원형 차트 만들기  
  
1.  [웹 포털 또는 SharePoint 통합 모드의 보고서 서버 또는 컴퓨터에서](../../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
     ![보고서 작성기 시작](../../reporting-services/media/rb-getstarted.png "보고서 작성기 시작")  
  
     경우는 **시작** 대화 상자가 나타나지 않으면를 클릭 **파일** >**새로**합니다. **새 보고서 또는 데이터 집합** 대화 상자에 **시작** 대화 상자와 같은 내용이 가장 많이 들어 있습니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭한 다음 **만들기**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭하고 **다음**을 클릭합니다.  
  
5.  **데이터 원본에 대한 연결 선택** 페이지에서 **새로 만들기**를 클릭합니다.  
  
     **데이터 원본 속성** 대화 상자가 열립니다.  
  
6.  데이터 원본 이름으로 원하는 이름을 지정할 수 있습니다. **이름** 상자에 **MyPieChart**를 입력합니다.  
  
7.  **연결 유형 선택** 상자에서 **XML**을 클릭합니다.  
  
8.  **자격 증명** 탭을 클릭하고 **현재 Windows 사용자 사용을 선택하세요. Kerberos 위임이 필요할 수도 있습니다.**를 선택한 후 **확인**을 클릭합니다.  
  
9. **데이터 원본에 대한 연결 선택** 페이지에서 **MyPieChart**를 클릭하고 **다음**을 클릭합니다.  
  
10. 다음 텍스트를 복사하여 **쿼리 디자인** 페이지 상단에 있는 큰 상자에 붙여 넣습니다.  
  
    ```  
    <Query>  
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>  
    <XmlData>  
    <Root>  
    <S Sales="150">  
      <C FullName="Jae Pak" />  
    </S>  
    <S Sales="350">  
      <C FullName="Jillian  Carson" />  
    </S>  
    <S Sales="250">  
      <C FullName="Linda C Mitchell" />  
    </S>  
    <S Sales="500">  
      <C FullName="Michael Blythe" />  
    </S>  
    <S Sales="450">  
      <C FullName="Ranjit Varkey" />  
    </S>  
    </Root>  
    </XmlData>  
    </Query>  
    ```  
  
11. (선택 사항) 클릭는 **실행** 단추 (**!**) 차트를 기반으로 합니다 데이터를 볼 수 있습니다.  
  
     ![보고서 작성기 쿼리 디자인](../../reporting-services/report-builder/media/rb-designquery.png "보고서 작성기 쿼리 디자인")  
  
12. **다음**을 클릭합니다.  
  
13. **차트 종류 선택** 페이지에서 **원형**을 클릭하고 **다음**을 클릭합니다.  
  
14. 에 **차트 필드 정렬** 페이지에서 두 번 클릭은 **Sales** 필드에 **사용 가능한 필드** 상자입니다.  
  
     Sales 필드는 숫자 값이므로 자동으로 **값** 상자로 이동합니다.  
  
     ![보고서 작성기 마법사 필드 정렬](../../reporting-services/report-builder/media/rb-wizarrangefields.png "보고서 작성기 마법사 필드 정렬")  
  
15. 끌어서는 **FullName** 필드를 **사용 가능한 필드** 상자를 **범주** 상자 (또는 두 번 클릭;으로 이동 합니다는 **범주** 상자)를 클릭 하 고 **다음**합니다.  
  
     미리 보기 페이지에는 대표적 데이터를 이용한 새 원형 차트가 표시됩니다. 영업 사원 이름 대신 Full Name 1, Full Name 2 등의 범례가 표시되고 원형 차트의 각 조각 크기도 정확하게 나타나지 않습니다. 이 보고서는 단순히 보고서의 대략적인 모양을 보여 주는 역할을 합니다.  
  
     ![보고서 작성기 미리 보기를 새로 차트](../../reporting-services/report-builder/media/rb-newchartpreview.png "작성기 새 차트 미리 보기 보고서")  
  
16. **마침**을 클릭합니다.  
  
     그러면 이번에도 대표적 데이터를 이용한 새 원형 차트 보고서가 디자인 보기에 표시됩니다.  
  
     ![보고서 작성기 디자인 보기에서 새 원형](../../reporting-services/report-builder/media/rb-newpiedesign.png "보고서 작성기 디자인 보기에서 새 원형")  
  
17. 실제 원형 차트를 보려면 리본 메뉴의 **홈** 탭에서 **실행** 을 클릭합니다.  
  
     ![보고서 작성기 실행을 새 차트](../../reporting-services/report-builder/media/rb-newchartrun.png "작성기 새 차트 실행 보고서")  
  
18. 원형 차트를 계속 수정하려면 이 문서의 [마법사 실행 후 작업](#AfterWizard) 으로 이동하십시오.  
  
##  <a name="CreatePieQueryData"></a>[!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리로 원형 차트 만들기  
  
1.  [웹 포털, SharePoint 통합 모드의 보고서 서버 또는 컴퓨터에서](../../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  경우는 **시작** 대화 상자가 나타나지 않으면를 클릭 **파일** >**새로**합니다. **새 보고서 또는 데이터 집합** 대화 상자에 **시작** 대화 상자와 같은 내용이 가장 많이 들어 있습니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭한 다음 **만들기**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭하고 **다음**을 클릭합니다.  
  
5.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택하고 **다음**을 클릭합니다. 사용자 이름과 암호를 입력해야 할 수 있습니다.  
  
    > [!NOTE]  
    >  적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [자습서의 사전 요구 사항 &#40;보고서 작성기&#41;](../../reporting-services/prerequisites-for-tutorials-report-builder.md)를 참조하세요.  
  
6.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
7.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 150 AS Sales, 'Jae Pak' AS FullName   
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName   
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName   
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName   
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName   
    ```  
  
8.  (옵션) 실행 단추(**!**)를 클릭하여 차트의 기반으로 사용될 데이터를 확인합니다.  
  
9. **다음**을 클릭합니다.  
  
10. **차트 종류 선택** 페이지에서 **원형**을 클릭하고 **다음**을 클릭합니다.  
  
11. 에 **차트 필드 정렬** 페이지에서 두 번 클릭은 **Sales** 필드에 **사용 가능한 필드** 상자입니다.  
  
     Sales 필드는 숫자 값이므로 자동으로 **값** 상자로 이동합니다.  
  
12. 끌어서는 **FullName** 필드를 **사용 가능한 필드** 상자를 **범주** 상자 (또는 두 번 클릭;으로 이동 합니다는 **범주** 상자)를 클릭 하 고 **다음**합니다.  
  
13. **마침**을 클릭합니다.  
  
     이제 새 원형 차트 보고서가 디자인 화면에 나타납니다. 이 원형 차트 보고서에는 보고서 내용이 대략적으로 나타납니다. 영업 사원 이름 대신 Full Name 1, Full Name 2 등의 범례가 표시되고 원형 차트의 각 조각 크기도 정확하게 나타나지 않습니다. 이 보고서는 단순히 보고서의 대략적인 모양을 보여 주는 역할을 합니다.  
  
15. 실제 원형 차트를 보려면 리본 메뉴의 **홈** 탭에서 **실행** 을 클릭합니다.  
 
##  <a name="AfterWizard"></a> 마법사 실행 후 작업  
 원형 차트 보고서를 만들었으므로 이제 보고서를 사용할 수 있습니다. 리본 메뉴의 **실행** 탭에서 **디자인**을 클릭하면 계속해서 보고서를 수정할 수 있습니다.  
  
## <a name="make-the-chart-bigger"></a>차트를 크게 만들기  
 원형 차트를 좀 더 크게 만들어 봅니다. 
 
*  차트의 요소가 아니라 차트를 클릭하여 선택한 다음 오른쪽 아래 모퉁이를 끌어 크기를 조정합니다.  

끌면 디자인 화면이 더 커집니다.
  
## <a name="add-a-report-title"></a>보고서 제목 추가  
1. 차트 위쪽의 **차트 제목** 을 선택하고 **Sales Pie Chart**와 같은 제목을 입력합니다.  
2. 속성 창에서 선택한 제목 변경 **색** 를 **검정** 및 **FontSize** 를 **12pt**합니다.
  
## <a name="add-percentages"></a>백분율 추가  
 
1.  원형 차트를 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 레이블 표시**합니다. 원형 차트의 각 조각 내에 데이터 레이블이 표시됩니다.  
  
2.  레이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **계열 레이블 속성**합니다. **계열 레이블 속성** 대화 상자가 표시됩니다.  
  
3.  에 **데이터에 레이블을** 상자에서 입력 **#PERCENT {P0}**합니다.  
  
     **{P0}** 을 추가하면 백분율이 소수 자릿수 없이 표시됩니다. 만 입력 **#PERCENT**, 하면 숫자가 소수점 두 자리까지 표시 됩니다. **#PERCENT** 키워드 수에 대 한 계산 이나 기능을 수행 하는;도 많은 키워드가 있습니다.  
     
4. **예** 를 클릭하여 **UseValueAsLabel** 을 **False**로 설정할 것임을 확인합니다.

5. **글꼴** 탭에서 **굵게** 를 선택하고 **색** 을 **흰색**으로 변경합니다.

6. **확인**을 클릭합니다.     
  
 차트 레이블 및 범례를 사용자 지정하는 방법에 대한 자세한 내용은 [원형 차트에서 백분율 값 표시 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) 및 [범례 항목의 텍스트 변경 #40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)를 참조하세요.  
  
##  <a name="WhatsNext"></a> 다음 단계  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]에서 첫 번째 보고서를 만들었으므로 이제 다른 자습서를 수행하고 고유의 데이터로 보고서를 만들 수 있습니다. [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]를 실행하려면 *연결 문자열*을 사용하여 데이터베이스 등의 데이터 원본에 액세스할 수 있는 권한이 있어야 합니다. 연결 문자열은 실제로 사용자를 데이터 원본에 연결하는 역할을 합니다. 시스템 관리자가 연결 문자열 정보를 가지고 있으며 사용자에 대해 데이터 원본 연결을 설정할 수 있습니다.  
  
 다른 자습서를 진행 하려면 SQL Server 및 자격 증명의 인스턴스 이름을 모든 데이터베이스에 대 한 읽기 전용 액세스에 대 한 충분 한 합니다. 데이터베이스 액세스 권한은 시스템 관리자가 대신 설정할 수 있습니다.  
  
 마지막으로, 보고서를 보고서 서버나 보고서 서버와 통합된 SharePoint 사이트에 저장하려면 URL 및 해당 권한이 있어야 합니다. 만든 보고서를 사용자의 컴퓨터에서 직접 실행할 수도 있지만 보고서 서버나 SharePoint 사이트에서 실행하면 더 많은 기능을 사용할 수 있습니다. 자신이 만든 보고서나 다른 사용자의 보고서를 보고서가 게시된 보고서 서버나 SharePoint 사이트에서 실행할 수 있는 권한이 있어야 합니다. 시스템 관리자에게 액세스 권한을 요청하십시오.  
  
 시작하기 전에 몇 가지 개념이나 용어에 대해 알아 두면 좋습니다. [보고서 제작 개념&#40;보고서 작성기 및 SSRS&#41; SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)를 참조하세요. 또한 처음 보고서를 만들 때는 사전에 시간을 들여 계획을 세우는 것이 좋습니다. [보고서 계획&#40;보고서 작성기&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)를 참조하세요.  

## <a name="next-steps"></a>다음 단계

[보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)   
[SQL Server 2016의 보고서 작성기](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
