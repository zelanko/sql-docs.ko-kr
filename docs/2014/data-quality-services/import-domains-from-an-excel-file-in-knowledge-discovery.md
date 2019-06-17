---
title: 기술 자료 검색 시 Excel 파일에서 도메인 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4d3a3940-6c2a-4dc4-90eb-86f26012c165
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0ca7391a025cf0fe4477cc9008c51c0a06a59f00
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480541"
---
# <a name="import-domains-from-an-excel-file-in-knowledge-discovery"></a>기술 자료 검색 시 Excel 파일에서 도메인 가져오기
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] ) 기술 자료 검색 작업을 통해 Excel 파일에서 하나 이상의 도메인을 가져오는 방법에 대해 설명합니다. 가져오기 프로세스는 기술 자료 생성 프로세스를 간소화하여 시간과 노력을 절감합니다. Excel 파일이나 텍스트 파일에 데이터가 있는 사용자는 이 프로세스를 통해 해당 데이터를 포함한 기술 자료를 만들 수 있습니다. (기존 기술 자료의 도메인에 값을 가져오는 방법에 대한 자세한 내용은 [Excel 파일에서 도메인으로 값 가져오기](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)를 참조하세요.) Excel 파일로의 내보내기는 지원되지 않습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 Excel 파일에서 도메인을 가져오려면 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 가 설치된 컴퓨터에 Excel이 설치되어 있어야 합니다. 도메인 값이 포함된 Excel 파일을 생성한 상태여야 합니다( [How the import works](#How)참조). 그리고 도메인을 가져올 기술 자료를 만들고 열어 두어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 Excel 파일에서 도메인을 가져오려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Import"></a> Excel 파일에서 기술 자료로 도메인 가져오기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 다음 중 하나를 수행합니다.  
  
    -   **새 기술 자료**를 클릭하고, 기술 자료의 이름을 입력하고, **기술 자료 만들기** 에 대해 **없음**을 선택하고, **기술 자료 검색** 작업을 선택한 후 **만들기**를 클릭하여 도메인을 가져올 새 기술 자료를 만듭니다.  
  
    -   **기술 자료 열기**를 클릭하고, 기술 자료를 선택하고, **기술 자료 검색**을 선택한 후 **다음**을 클릭하여 도메인을 가져올 기존 기술 자료를 엽니다.  
  
3.  **맵** 페이지에서 **데이터 원본** 에 대해 **Excel 파일**을 선택합니다.  
  
4.  **Excel 파일** 줄에서 **찾아보기** 를 클릭합니다.  
  
5.  **Excel 파일 선택** 대화 상자에서 가져올 Excel 파일이 포함된 폴더로 이동하고 Excel 파일을 선택한 후 **열기**를 클릭합니다.  
  
6.  **워크시트** 드롭다운 목록에서 가져올 Excel 파일의 워크시트를 선택합니다.  
  
7.  첫 번째 행을 데이터 헤더로 간주하려는 경우, 그리고 첫 번째 행의 값을 열 이름으로 사용하려는 경우 **첫 번째 행을 헤더로 사용하세요** 를 선택합니다. DQS에서 Excel의 열 머리글 값(영문자)을 사용할 경우 첫 번째 행을 데이터 값으로 간주하려면 **첫 번째 행을 헤더로 사용하세요** 를 선택 취소합니다.  
  
8.  열을 선택한 다음 기존 도메인을 열에 매핑하거나 **도메인 만들기** 아이콘을 클릭하고 **도메인 만들기** 대화 상자에서 도메인을 만든 후 도메인을 열에 매핑하여 새 도메인을 만듭니다. 도메인의 데이터 형식이 열의 데이터 형식과 일치해야 합니다. 스프레드시트의 모든 열에 대해 위의 작업을 반복합니다.  
  
9. **다음**을 클릭합니다.  
  
10. **검색** 페이지에서 **시작** 을 클릭하여 Excel 스프레드시트의 데이터를 분석합니다.  
  
    > [!NOTE]  
    >  데이터가 업로드되기 전에 페이지에서 나가면 파일 업로드 프로세스가 종료됩니다.  
  
11. 분석이 올바르게 완료되었는지 확인하고 **다음**을 클릭합니다.  
  
12. **도메인 값 관리** 페이지에서 **도메인** 목록에 올바른 도메인이 나열되어 있고 도메인 테이블에 값을 입력했는지 확인합니다.  
  
13. **마침**을 클릭한 다음 **게시** 를 클릭하여 기술 자료를 게시하거나 **아니요** 를 클릭하여 게시하지 않습니다.  
  
14. 기술 자료가 게시되었는지 확인한 후 **확인**을 클릭합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: Excel 파일에서 도메인을 가져온 후  
 Excel 파일에서 도메인을 가져온 후 도메인에 정보를 추가하거나 도메인의 내용에 따라 정리 또는 일치 프로젝트에서 도메인을 사용할 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](../../2014/data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../../2014/data-quality-services/managing-a-domain.md), [복합 도메인 관리](../../2014/data-quality-services/managing-a-composite-domain.md), [일치 정책 만들기](../../2014/data-quality-services/create-a-matching-policy.md), [데이터 정리](../../2014/data-quality-services/data-cleansing.md) 또는 [데이터 일치](../../2014/data-quality-services/data-matching.md)를 참조하세요.  
  
##  <a name="How"></a> How the import works  
 가져오기 작업에서 DQS는 Excel 파일을 다음과 같이 해석합니다.  
  
-   열은 도메인을 나타냅니다.  
  
-   행은 데이터 레코드를 나타냅니다.  
  
-   첫 번째 행은 **첫 번째 행을 헤더로 사용하세요** 확인란의 설정에 따라 도메인 이름을 나타내거나 첫 번째 데이터 값 또는 레코드입니다.  
  
 가져오기 작업에는 다음 규칙이 적용됩니다.  
  
-   이 작업은 도메인 값을 기술 자료로 가져옵니다. 도메인 규칙 또는 일치 정책은 가져오지 않습니다.  
  
-   Excel 파일의 확장명은 .xlsx, .xls 또는 .csv입니다. 도메인 값 또는 전체 도메인을 가져오려면 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 컴퓨터에 Microsoft Excel이 설치되어 있어야 합니다. Excel 2003 이상 버전이 지원됩니다. 64비트 버전의 Excel이 사용된 경우 Excel 2003 파일만 지원됩니다. Excel 2007 또는 2010 파일은 지원되지 않습니다.  
  
-   Excel 파일 형식 .xlsx는 Excel 64비트 설치에서 지원되지 않습니다. 64비트 Excel을 사용 중인 경우 스프레드시트 파일을 .xls 파일로 저장하세요.  
  
-   .xlsx 및 .xls 파일에서는 처음 8개 행에서 가장 많이 사용된 데이터 형식에 의해 열의 데이터 형식이 결정됩니다. 데이터 형식을 따르지 않는 셀에는 null 값이 지정됩니다.  
  
-   .csv 파일에서는 처음 8개 행에서 가장 많이 사용된 데이터 형식에 의해 데이터 형식이 결정됩니다.  
  
-   도메인 규칙을 따르지 않는 Excel 스프레드시트의 값을 가져오면 잘못된 값으로 표시됩니다.  
  
-   Excel 파일이 올바른 형식이 아니거나 손상된 경우 가져오기 작업에서 오류가 발생합니다.  
  
  
