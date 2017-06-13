---
title: "Excel 2003 행 제한을 해결 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8533cd39c8a3d5efde78fee3e045eb744d562a97
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  이 항목에서는 페이지를 매긴 보고서를 Excel로 내보낼 때 Excel 2003 행 제한을 해결하는 방법을 설명합니다. 테이블만 포함하는 보고서에 대한 해결 방법입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003(.xls) 렌더링 확장 프로그램은 더 이상 사용되지 않습니다. 자세한 내용은 [SQL Server 2016의 SQL Server Reporting Services에서 지원되지 않는 기능](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)을 참조하세요.  
  
 Excel 2003은 워크시트당 최대 65,536개 행을 지원합니다. 특정 행 수 이후 명시적 페이지 나누기를 강제로 수행하여 이 제한을 해결할 수 있습니다. Excel 렌더러는 각 명시적 페이지 나누기에 대해 새 워크시트를 만듭니다.  
  
### <a name="to-create-an-explicit-page-break"></a>명시적 페이지 나누기를 만들려면  
  
1.  [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 엽니다.  
  
2.  테이블에서 데이터 행을 마우스 오른쪽 단추로 클릭한 다음 **그룹 추가** > **상위 그룹** 을 클릭하여 외부 테이블 그룹을 추가합니다.  
  
     ![부모 그룹 선택](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "부모 그룹 선택")  
  
3.  **그룹화 방법** 식 상자에 다음 수식을 입력한 다음 **확인** 을 클릭하여 상위 그룹을 추가합니다.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     수식은 숫자를 데이터 집합의 65000개 행 집합 각각에 할당합니다. 그룹에 페이지 나누기가 정의되어 있는 경우 식을 사용하면 65000개 행마다 페이지가 나눠집니다.  
  
     외부 테이블 그룹을 추가하면 그룹 열이 보고서에 추가됩니다.  
  
4.  열 머리글을 마우스 오른쪽 단추로 클릭하고 **열 삭제**를 클릭한 다음 **열만 삭제**를 선택하여 그룹 열을 삭제하고 **확인**을 클릭합니다.  
  
     ![그룹 열 삭제](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "그룹 열 삭제")  
  
5.  **행 그룹** 섹션에서 **그룹 1** 을 마우스 오른쪽 단추로 클릭한 다음 **그룹 속성**을 클릭합니다.  
  
     ![그룹 속성 보기](../../reporting-services/report-builder/media/groupproperties-updated.png "그룹 속성 보기")  
  
6.  **그룹 속성** 대화 상자의 **정렬** 페이지에서 기본 정렬 옵션을 선택하고 **삭제**를 클릭합니다.  
  
     ![기본 정렬 삭제](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "기본 정렬 삭제")  
  
7.  **페이지 나누기** 페이지에서 **각 그룹 인스턴스 사이** 를 클릭한 다음 **확인**을 클릭합니다.  
  
     ![페이지 나누기를 설정할](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "페이지 나누기를 설정 합니다.")  
  
8.  보고서를 저장합니다. 보고서를 Excel로 내보내는 경우 여러 워크시트로 내보내고 각 워크시트에는 최대 65000개 행이 포함됩니다.  
  
  
