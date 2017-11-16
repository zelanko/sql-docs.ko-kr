---
title: "보고서 데이터 원본 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bd6662c7-ffbe-479d-8944-3dc858340998
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b941dc8eb4fb1f0fc14d2565c8f1f65dd3ba4d15
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-report-data-source"></a>보고서 데이터 원본 만들기
  파워 뷰를 다차원 모델에 연결하려면 SharePoint 라이브러리에서 .rsds 파일이라는 공유 보고서 데이터 원본 정의를 만들어야 합니다. .rsds 파일은 다차원 모델에 연결하는 데 사용되는 Analysis Services 서버 인스턴스의 이름, 연결 형식, 연결 문자열 및 자격 증명을 지정합니다. 사용자가 .rsds를 클릭하면 비어 있는 새 파워 뷰 보고서(.rdlx 파일)가 브라우저에 열립니다.  
  
 .rsds 연결을 만들려면 SQL Server 2012 이상의 Reporting Services와 SharePoint 2010 또는 SharePoint 2013용 Reporting Services 추가 기능을 설치해야 합니다.  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>다차원 모델에 대한 보고서 데이터 원본(.rsds) 연결 만들기  
 시작하기 전에 다음을 알아야 합니다.  
  
-   다차원 모드에서 실행하는 Analysis Services 서버 인스턴스의 이름.  
  
-   연결할 다차원 데이터베이스의 이름.  
  
-   두 개 이상 있는 경우 큐브의 이름.  
  
-   (선택 사항) 큐브 뷰 이름.  
  
-   (선택 사항) 로캘 식별자.  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>공유 데이터 원본(.rsds) 파일을 만들려면(SharePoint 2010)  
  
1.  라이브러리 리본 메뉴에 있는 **문서** 탭을 클릭합니다.  
  
2.  **새 문서** > **보고서 데이터 원본**을 클릭합니다.  
  
    > [!NOTE]  
    >  메뉴에 **보고서 데이터 원본** 항목이 표시되지 않는 경우 이 라이브러리에 대해 보고서 데이터 원본의 콘텐츠 형식이 설정되어 있지 않은 것입니다. 자세한 내용은 [SharePoint 라이브러리에 Reporting Services 콘텐츠 형식 추가](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)를 참조하세요.  
  
3.  **데이터 원본 속성** 페이지에서 **이름**에 연결 .rsds 파일의 이름을 입력합니다.  
  
4.  **데이터 원본 유형**에서 **파워 뷰용 Microsoft BI 의미 체계 모델**을 선택합니다.  
  
5.  **연결 문자열**에서 Analysis Services 서버 이름, 데이터베이스 이름, 큐브 이름 및 선택적 설정을 지정합니다.  
  
     연결 문자열: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>’`  
  
    > [!NOTE]  
    >  큐브가 두 개 이상 있는 경우 큐브 이름을 지정해야 합니다.  
  
     (선택 사항) 큐브에는 특정 차원 및/또는 측정값 그룹만 클라이언트에 표시되는 선택 뷰를 사용자에게 제공하는 큐브 뷰가 있을 수 있습니다. 큐브 뷰를 지정하려면 큐브 뷰 이름을 Cube 속성에 대한 값으로 지정합니다. `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>’`  
  
     (선택 사항) 큐브에는 모델 내의 다양한 언어에 대해 지정된 메타데이터 및 데이터 번역이 있을 수 있습니다. 번역(데이터 및 메타데이터)을 보려면 연결 문자열에 "로캘 ID" 속성을 추가해야 합니다. `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>’; Locale Identifier=<identifier number>`  
  
6.  **자격 증명**에서 보고서 서버가 외부 데이터 원본에 액세스하는 데 필요한 자격 증명을 얻는 방법을 지정합니다.  
  
    -   보고서를 연 사용자의 자격 증명을 사용하여 데이터에 액세스하려면 **Windows 인증(통합)** 을 선택합니다. SharePoint 사이트 또는 팜에서 폼 인증을 사용하거나 트러스트된 계정을 통해 보고서 서버에 연결하는 경우 이 옵션을 선택하지 마십시오. 이 보고서에 대한 구독 또는 데이터 처리를 예약하려는 경우 이 옵션을 선택하지 마십시오. 이 옵션은 도메인에 Kerberos 인증을 설정한 경우나 데이터 원본이 보고서 서버와 같은 컴퓨터에 있는 경우에 가장 잘 작동합니다. Kerberos 인증을 해제하면 Windows 자격 증명이 하나의 다른 컴퓨터로만 전달될 수 있습니다. 따라서 추가 연결이 필요한 다른 컴퓨터에 외부 데이터 원본이 있는 경우 원하는 데이터 대신 오류가 표시됩니다.  
  
    -   사용자가 보고서를 실행할 때마다 자격 증명을 입력하도록 하려면 **자격 증명 확인** 을 선택합니다. 이 보고서에 대한 구독 또는 데이터 처리를 예약하려는 경우 이 옵션을 선택하지 마십시오.  
  
    -   단일 자격 증명 집합을 사용하여 데이터에 액세스하려면 **저장된 자격 증명** 을 선택합니다. 자격 증명은 저장되기 전에 암호화됩니다. 저장된 자격 증명의 인증 방법을 결정하는 옵션을 선택할 수 있습니다. 저장된 자격 증명이 Windows 사용자 계정에 속하면 Windows 자격 증명으로 사용을 선택합니다. 데이터베이스 서버에 대한 실행 컨텍스트를 설정하려면 **이 계정에 대한 실행 컨텍스트 설정** 을 선택합니다.  
  
    -   연결 문자열에서 자격 증명을 지정하거나 최소 권한 계정을 사용하여 보고서를 실행하려면 **자격 증명 필요 없음** 을 선택합니다.  
  
7.  **연결 테스트** 를 클릭하여 유효성을 검사합니다.  
  
8.  데이터 원본을 활성화 하려면 **이 데이터 원본 사용** 을 선택합니다. 데이터 원본이 구성되었지만 활성이 아닌 경우 사용자가 보고서를 만들려고 하면 오류 메시지가 나타납니다.  
  
  

