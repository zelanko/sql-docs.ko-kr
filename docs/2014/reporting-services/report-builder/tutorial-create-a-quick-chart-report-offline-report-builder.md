---
title: '자습서: 오프라인에서 빠른 차트 보고서 만들기(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f345eaa2a51b5e6789f2a03968f8a1e68b12519a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107567"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>자습서: 오프라인에서 빠른 차트 보고서 만들기(보고서 작성기)
  이 자습서에서는 마법사를 사용하여 원형 차트를 만든 다음 차트를 어떤 식으로 수정할 수 있는지 보여 주기 위해 차트를 조금 수정합니다. 이 자습서는 다음 두 가지 방법으로 진행할 수 있습니다. 두 방법 모두 다음 그림에 나와 있는 것과 같은 원형 차트와 동일한 결과를 가집니다.  
  
 ![실행 뷰에 표시된 "My First Pie Chart"](../media/rs-my1stpierunview.gif "실행 뷰의 내 첫 번째 원형 차트")  
  
## <a name="prerequisites"></a>사전 요구 사항  
 XML 데이터나 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 사용하려면 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 보고서 작성기에 대한 액세스 권한이 있어야 합니다. 보고서 관리자나 SharePoint 사이트에서 사용할 수 있는 ClickOnce 버전 또는 독립 실행형 버전을 실행할 수 있습니다. ClickOnce 버전의 경우 첫 번째 단계, 즉 보고서 작성기를 여는 방법만 다릅니다. 자세한 내용은 [설치, 제거 및 보고서 작성기 지원](../install-uninstall-and-report-builder-support.md)을 참조 하세요.  
  
##  <a name="TwoWays"></a>이 자습서를 수행 하는 두 가지 방법  
  
-   [XML 데이터로 원형 차트 만들기](#CreatePieChartXML)  
  
-   [데이터를 포함 하는 Transact-sql 쿼리로 원형 차트 만들기](#CreatePieQueryData)  
  
### <a name="using-xml-data-for-this-tutorial"></a>이 자습서에서 XML 데이터 사용  
 이 항목에서 복사한 XML 데이터를 사용하여 마법사에 붙여 넣을 수 있습니다. 보고서 서버나 SharePoint 통합 모드에 있는 보고서 서버에 연결되어 있지 않아도 되며 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 인스턴스에 액세스하지 않아도 됩니다.  
  
 [XML 데이터로 원형 차트 만들기](#CreatePieChartXML)  
  
### <a name="using-a-transact-sql-query-that-contains-data-for-this-tutorial"></a>이 자습서에서 데이터가 포함된 Transact-SQL 쿼리 사용  
 이 항목에서 데이터가 포함된 쿼리를 복사하여 마법사에 붙여 넣을 수 있습니다. 
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 인스턴스 이름과 모든 데이터베이스에 대한 읽기 전용 액세스 권한이 있는 자격 증명이 있어야 합니다. 자습서의 데이터 세트 쿼리에서는 리터럴 데이터를 사용하지만 쿼리를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 인스턴스에서 처리해야 보고서 데이터 세트에 필요한 메타데이터가 반환됩니다.  
  
 
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 사용하는 경우 좋은 점은, 다른 모든 보고서 작성기 자습서에서도 같은 방법을 사용하므로 다른 자습서를 사용할 때 수행할 작업을 미리 알게 된다는 것입니다.  
  
 
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 사용하려면 몇 가지 다른 필수 구성 요소가 있어야 합니다. 자세한 내용은 [자습서의 사전 요구 사항 &#40;보고서 작성기&#41;](../report-builder-tutorials.md)를 참조하세요.  
  
 [데이터를 포함 하는 Transact-sql 쿼리로 원형 차트 만들기](#CreatePieQueryData)  
  
## <a name="also-in-this-article"></a>문서 내용  
 [마법사 실행 후 작업](#AfterWizard)  
  
 [다음 단계](#WhatsNext)  
  
##  <a name="CreatePieChartXML"></a>XML 데이터로 원형 차트 만들기  
  
#### <a name="to-create-the-pie-chart-with-xml-data"></a>XML 데이터로 원형 차트를 만들려면  
  
1.  
  **시작**을 클릭하고 **프로그램**, **Microsoft SQL Server 2012 보고서 작성기**를 차례로 가리킨 다음 **보고서 작성기**를 클릭합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  
  **시작** 대화 상자가 나타나지 않으면 **보고서 작성기** 단추에서 **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에서 **보고서** 가 선택 되어 있는지 확인 합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭한 다음 **만들기**를 클릭합니다.  
  
4.  
  **데이터 세트 선택** 페이지에서 **데이터 세트 만들기**를 클릭한 후, **다음**을 클릭합니다.  
  
5.  
  **데이터 원본에 대한 연결 선택** 페이지에서 **새로 만들기**를 클릭합니다.  
  
     
  **데이터 원본 속성** 대화 상자가 열립니다.  
  
6.  데이터 원본 이름으로 원하는 이름을 지정할 수 있습니다. 
  **이름** 상자에 **MyPieChart**를 입력합니다.  
  
7.  **연결 유형 선택** 상자에서 XML을 클릭 **합니다.**  
  
8.  **자격 증명** 탭을 클릭 하 고 **현재 Windows 사용자 사용을 선택 합니다. Kerberos 위임이 필요할 수 있습니다**. 그런 다음 **확인**을 클릭 합니다.  
  
9. 
  **데이터 원본에 대한 연결 선택** 페이지에서 **MyPieChart**를 클릭하고 **다음**을 클릭합니다.  
  
10. 다음 텍스트를 복사 하 여 **쿼리 디자인** 페이지의 가운데에 있는 크게 상자에 붙여넣습니다.  
  
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
  
11. (옵션) 실행 단추( **!** )를 클릭하여 차트의 기반으로 사용될 데이터를 확인합니다.  
  
12. **다음**을 클릭합니다.  
  
13. 
  **차트 종류 선택** 페이지에서 **원형**을 클릭하고 **다음**을 클릭합니다.  
  
14. 
  **차트 필드 정렬** 페이지의 **사용 가능한 필드** 상자에서 **Sales** 필드를 두 번 클릭합니다.  
  
     Sales 필드는 숫자 값이므로 자동으로 **값** 상자로 이동합니다.  
  
15. 
  **사용 가능한 필드** 상자에서 **FullName** 필드를 **범주** 상자로 끌어 오거나 FullName 필드를 두 번 클릭하여 **범주** 상자로 이동한 후 **다음**을 클릭합니다.  
  
16. **스타일 선택** 페이지에서 **해양** 는 기본적으로 선택 되어 있습니다. 다른 스타일을 클릭하여 모양을 확인합니다.  
  
17. **Finish**를 클릭합니다.  
  
     이제 새 원형 차트 보고서가 디자인 화면에 나타납니다. 이 원형 차트 보고서에는 보고서 내용이 대략적으로 나타납니다. 영업 사원 이름 대신 Full Name 1, Full Name 2 등의 범례가 표시되고 원형 차트의 각 조각 크기도 정확하게 나타나지 않습니다. 이 보고서는 단순히 보고서의 대략적인 모양을 보여 주는 역할을 합니다.  
  
18. 실제 원형 차트를 보려면 리본 메뉴의 **홈** 탭에서 **실행** 을 클릭합니다.  
  
 ![맨 위로 이동 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [](#TwoWays)  
  
##  <a name="CreatePieQueryData"></a>[!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리로 원형 차트 만들기  
  
#### <a name="to-create-the-pie-chart-with-a-includetsqlincludestsql-mdmd-query-that-contains-data"></a>데이터를 포함하는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리로 원형 차트를 만들려면  
  
1.  
  **시작**을 클릭하고 **프로그램**, **Microsoft SQL Server 2012 보고서 작성기**를 차례로 가리킨 다음 **보고서 작성기**를 클릭합니다.  
  
2.  **새 보고서 또는 데이터 집합** 대화 상자의 왼쪽 창에서 **보고서** 가 선택 되어 있는지 확인 합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭한 다음 **만들기**를 클릭합니다.  
  
4.  
  **데이터 세트 선택** 페이지에서 **데이터 세트 만들기**를 클릭한 후, **다음**을 클릭합니다.  
  
5.  
  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택하고 **다음**을 클릭합니다. 사용자 이름과 암호를 입력해야 할 수 있습니다.  
  
    > [!NOTE]  
    >  적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [자습서의 사전 요구 사항 &#40;보고서 작성기&#41;](../report-builder-tutorials.md)를 참조하세요.  
  
6.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
7.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 150 AS Sales, 'Jae Pak' AS FullName   
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName   
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName   
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName   
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName   
    ```  
  
8.  (옵션) 실행 단추( **!** )를 클릭하여 차트의 기반으로 사용될 데이터를 확인합니다.  
  
9. **다음**을 클릭합니다.  
  
10. 
  **차트 종류 선택** 페이지에서 **원형**을 클릭하고 **다음**을 클릭합니다.  
  
11. 
  **차트 필드 정렬** 페이지의 **사용 가능한 필드** 상자에서 **Sales** 필드를 두 번 클릭합니다.  
  
     Sales 필드는 숫자 값이므로 자동으로 **값** 상자로 이동합니다.  
  
12. 
  **사용 가능한 필드** 상자에서 **FullName** 필드를 **범주** 상자로 끌어 오거나 FullName 필드를 두 번 클릭하여 **범주** 상자로 이동한 후 **다음**을 클릭합니다.  
  
13. 
  **스타일 선택** 페이지에 Ocean이 기본적으로 선택되어 있습니다. 다른 스타일을 클릭하여 모양을 확인합니다.  
  
14. **Finish**를 클릭합니다.  
  
     이제 새 원형 차트 보고서가 디자인 화면에 나타납니다. 이 원형 차트 보고서에는 보고서 내용이 대략적으로 나타납니다. 영업 사원 이름 대신 Full Name 1, Full Name 2 등의 범례가 표시되고 원형 차트의 각 조각 크기도 정확하게 나타나지 않습니다. 이 보고서는 단순히 보고서의 대략적인 모양을 보여 주는 역할을 합니다.  
  
15. 실제 원형 차트를 보려면 리본 메뉴의 **홈** 탭에서 **실행** 을 클릭합니다.  
  
 ![맨 위로 이동 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [](#TwoWays)  
  
##  <a name="AfterWizard"></a>마법사를 실행 한 후  
 원형 차트 보고서를 만들었으므로 이제 보고서를 사용할 수 있습니다. 리본 메뉴의 **실행** 탭에서 **디자인**을 클릭하면 계속해서 보고서를 수정할 수 있습니다.  
  
### <a name="make-the-chart-bigger"></a>차트를 크게 만들기  
 원형 차트를 좀 더 크게 만들어 봅니다. 차트의 요소가 아니라 차트를 클릭하여 선택한 다음 오른쪽 아래 모퉁이를 끌어 크기를 조정합니다.  
  
### <a name="add-a-report-title"></a>보고서 제목 추가  
 차트 위쪽의 **차트 제목** 을 선택하고 **Sales Pie Chart**와 같은 제목을 입력합니다.  
  
### <a name="add-percentages"></a>백분율 추가  
  
##### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>원형 차트에 레이블로 백분율 값을 표시하려면  
  
1.  원형 차트를 마우스 오른쪽 단추로 클릭 하 고 **데이터 레이블 표시**를 선택 합니다. 원형 차트의 각 조각 내에 데이터 레이블이 표시됩니다.  
  
2.  레이블을 마우스 오른쪽 단추로 클릭 하 고 **계열 레이블 속성**을 선택 합니다. 
  **계열 레이블 속성** 대화 상자가 표시됩니다.  
  
3.  `#PERCENT{P0}` **레이블 데이터** 옵션에를 입력 합니다.  
  
     
  `{P0}`을 추가하면 백분율이 소수 자릿수 없이 표시됩니다. 
  `#PERCENT`만 입력하면 숫자가 소수점 두 자리까지 표시됩니다. 
  `#PERCENT`는 자동으로 계산이나 기능을 수행하는 키워드이며 이외에도 많은 키워드가 있습니다.  
  
 차트 레이블 및 범례를 사용자 지정하는 방법에 대한 자세한 내용은 [원형 차트에서 백분율 값 표시 &#40;보고서 작성기 및 SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) 및 [범례 항목의 텍스트 변경 #40;보고서 작성기 및 SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md)를 참조하세요.  
  
 ![맨 위로 이동 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [](#TwoWays)  
  
##  <a name="WhatsNext"></a>다음 단계  
 보고서 작성기에서 첫 번째 보고서를 만들었으므로 이제 다른 자습서를 수행하고 고유의 데이터로 보고서를 만들 수 있습니다. 보고서 작성기를 실행 하려면 연결 문자열을 사용 하 여 데이터베이스와 같은 데이터 원본에 액세스할 수 있는 권한이 있어야 합니다. *연결 문자열*은 실제로 사용자를 데이터 원본에 연결 합니다. 시스템 관리자가 연결 문자열 정보를 가지고 있으며 사용자에 대해 데이터 원본 연결을 설정할 수 있습니다.  
  
 다른 자습서를 진행하려면 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 인스턴스 이름과 모든 데이터베이스에 대한 읽기 전용 액세스 권한이 있는 자격 증명만 있으면 됩니다. 데이터베이스 액세스 권한은 시스템 관리자가 대신 설정할 수 있습니다.  
  
 마지막으로, 보고서를 보고서 서버나 보고서 서버와 통합된 SharePoint 사이트에 저장하려면 URL 및 해당 권한이 있어야 합니다. 만든 보고서를 사용자의 컴퓨터에서 직접 실행할 수도 있지만 보고서 서버나 SharePoint 사이트에서 실행하면 더 많은 기능을 사용할 수 있습니다. 자신이 만든 보고서나 다른 사용자의 보고서를 보고서가 게시된 보고서 서버나 SharePoint 사이트에서 실행할 수 있는 권한이 있어야 합니다. 시스템 관리자에게 액세스 권한을 요청하십시오.  
  
 시작하기 전에 몇 가지 개념이나 용어에 대해 알아 두면 좋습니다. 자세한 내용은 [보고서 제작 개념 &#40;보고서 작성기 및 SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)를 참조 하세요. 또한 처음 보고서를 만들 때는 사전에 시간을 들여 계획을 세우는 것이 좋습니다. 자세한 내용은 [보고서 계획 &#40;보고서 작성기&#41;](../report-design/planning-a-report-report-builder.md)를 참조 하세요.  
  
 ![맨 위로 이동 링크와 함께 사용 되는 화살표 아이콘](../../2014-toc/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [](#TwoWays)  
  
## <a name="see-also"></a>참고 항목  
 [자습서 &#40;보고서 작성기&#41;](../report-builder-tutorials.md)   
 [SQL Server 2014의 보고서 작성기](report-builder-in-sql-server-2016.md)  
  
  
