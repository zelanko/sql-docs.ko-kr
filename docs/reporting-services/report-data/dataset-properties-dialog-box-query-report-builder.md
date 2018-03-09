---
title: "데이터 집합 속성 대화 상자, 쿼리(보고서 작성기) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10024"
- sql13.rtp.rptdesigner.datasetproperties.query.f1
- "10160"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
caps.latest.revision: "12"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f733d1c6013bb6f8110a52007e1a3cfa682bfecd
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>데이터 집합 속성 대화 상자, 쿼리(보고서 작성기)
  **데이터 집합 속성** 대화 상자에서 **쿼리** 를 선택하여 보고서 서버에서 공유 데이터 집합을 선택하거나 포함된 데이터 집합을 만들 수 있습니다. 포함된 데이터 집합의 경우 데이터 원본을 선택하고 쿼리를 작성해야 합니다.  
  
 **데이터 집합 속성** 대화 상자에는 다음과 같은 항목이 있습니다.  
  
-   [데이터 집합 속성 대화 상자, 매개 변수&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/3a0672ad-c969-455b-b952-585164ce1dda)  
  
-   [데이터 집합 속성 대화 상자, 필드&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)  
  
-   [데이터 집합 속성 대화 상자, 옵션&#40;보고서 작성기&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-options-report-builder.md)  
  
-   [데이터 집합 속성 대화 상자, 필터&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/933a6f44-4eb7-4e73-9c40-ac0fd17b23d3)  
  
 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 데이터 집합의 이름을 입력합니다. 이 이름이 보고서의 다른 데이터 영역이나 그룹의 이름과 같아서는 안 됩니다.  
  
 **공유 데이터 집합 사용**  
 보고서 서버에서 미리 정의된 데이터 집합을 사용하려면 이 옵션을 선택합니다.  
  
 **찾아보기**  
 보고서 서버나 SharePoint 사이트에서 폴더로 이동하고 공유 데이터 집합(.rsd)을 선택합니다.  
  
 **내 보고서에 포함된 데이터 집합 사용**  
 이 보고서 전용의 데이터 집합을 만들려면 이 옵션을 선택합니다.  
  
 **데이터 원본**  
 데이터 집합의 기준이 되는 데이터 원본을 선택합니다. 새 데이터 원본을 만들려면 **새로 만들기**를 클릭합니다.  
  
 **쿼리 유형**  
 데이터 집합에 사용할 명령 또는 쿼리의 유형을 선택합니다. 쿼리를 실행하여 데이터베이스에서 데이터를 검색하려면 **텍스트** 를 선택합니다. **의** TableDirect **기능을 사용하여 테이블 내의 모든 필드를 선택하려면** 테이블 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 선택합니다. 저장 프로시저를 이름으로 실행하려면 **저장 프로시저** 를 선택합니다. 기본값은**텍스트** 이며 대부분의 쿼리에 사용됩니다. 선택한 데이터 원본 쿼리를 편집하려면 **쿼리 디자이너**를 클릭합니다.  
  
> [!NOTE]  
>  모든 데이터 원본에서 모든 쿼리 유형을 지원하는 것은 아닙니다. 예를 들어 **테이블** 은 데이터 원본 유형 **OLE DB** 와 **ODBC**에서만 지원됩니다.  
  
 **데이터 집합 속성**  
 이 옵션은 **텍스트** 명령 유형 옵션을 선택하면 표시됩니다. 쿼리를 입력하거나 **가져오기**를 클릭하여 이미 존재하는 쿼리를 가져옵니다. 식을 편집하려면 **식** 단추(*fx*)를 클릭합니다.  
  
> [!NOTE]  
>  쿼리 디자이너를 사용하여 쿼리를 작성한 경우 쿼리의 텍스트가 이 상자에 표시됩니다.  
  
 **테이블 이름**  
 데이터 집합으로 사용할 테이블 이름을 입력합니다. 이 옵션은 **테이블**을 선택하면 표시됩니다.  
  
 **저장 프로시저 이름 선택 또는 입력**  
 사용할 저장 프로시저의 이름을 입력하거나 선택합니다. 식을 편집하려면 **식** 단추(*fx*)를 클릭합니다. 이 옵션은 저장 프로시저 명령 유형 옵션을 선택하면 표시됩니다.  
  
 **제한 시간(초)**  
 쿼리 제한 시간이 초과되기까지의 시간(초)을 입력합니다. 기본값은 30초입니다. **제한 시간** 값은 비워 두거나 0보다 커야 합니다. 값을 비워 두면 쿼리 시간이 제한되지 않습니다.  
  
 **필드 새로 고침**  
 쿼리 명령을 실행하여 [데이터 집합 속성 대화 상자, 필드](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42) 페이지에서 필드의 목록을 업데이트합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [쿼리 디자이너&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
