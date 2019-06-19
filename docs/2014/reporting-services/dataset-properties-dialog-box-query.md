---
title: 데이터 집합 속성 대화 상자, 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10160"
- sql12.rtp.rptdesigner.datasetproperties.query.f1
ms.assetid: 1fa34a4b-7de0-4e92-99fa-bc28a206773f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aead5d8e5c85b67333f10bee4e73e2bb1a8633ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109368"
---
# <a name="dataset-properties-dialog-box-query"></a>데이터 세트 속성 대화 상자, 쿼리
  선택 **쿼리** 에 **데이터 집합 속성** 대화 상자의 데이터 원본을 선택 하 고 쿼리를 만듭니다.  
  
 **데이터 집합 속성** 대화 상자에는 다음과 같은 항목이 있습니다.  
  
-   [데이터 집합 속성 대화 상자, 매개 변수](report-data/dataset-properties-dialog-box-parameters.md)  
  
-   [데이터 집합 속성 대화 상자, 필드](../../2014/reporting-services/dataset-properties-dialog-box-fields.md)  
  
-   [데이터 집합 속성 대화 상자, 옵션](../../2014/reporting-services/dataset-properties-dialog-box-options.md)  
  
-   [데이터 집합 속성 대화 상자, 필터](report-data/dataset-properties-dialog-box-filters.md)  
  
## <a name="options"></a>변수  
 **이름**  
 데이터 세트의 이름을 입력합니다. 이 이름이 보고서의 다른 데이터 영역이나 그룹의 이름과 같아서는 안 됩니다.  
  
 **데이터 원본**  
 데이터 세트의 기준이 되는 데이터 원본을 선택합니다. 새 데이터 원본을 만들려면 **새로 만들기**를 클릭합니다.  
  
 **쿼리 유형**  
 데이터 세트에 사용할 명령 또는 쿼리의 유형을 선택합니다. 쿼리를 실행하여 데이터베이스에서 데이터를 검색하려면 **텍스트** 를 선택합니다. **의** TableDirect **기능을 사용하여 테이블 내의 모든 필드를 선택하려면** 테이블 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 을 선택합니다. 저장 프로시저를 이름으로 실행하려면 **저장 프로시저** 를 선택합니다. 기본값은**텍스트** 이며 대부분의 쿼리에 사용됩니다. 선택한 데이터 원본 쿼리를 편집하려면 **쿼리 디자이너**를 클릭합니다.  
  
> [!NOTE]  
>  모든 데이터 원본에서 모든 쿼리 유형을 지원하는 것은 아닙니다. 예를 들어 **테이블** 은 데이터 원본 유형 **OLE DB** 와 **ODBC**에서만 지원됩니다.  
  
 **데이터 집합 속성**  
 이 옵션은 **텍스트** 명령 유형 옵션을 선택하면 표시됩니다. 쿼리를 입력하거나 **가져오기**를 클릭하여 이미 존재하는 쿼리를 가져옵니다. 식을 편집하려면 **식** 단추(*fx*)를 클릭합니다.  
  
> [!NOTE]  
>  쿼리 디자이너를 사용하여 쿼리를 작성한 경우 쿼리의 텍스트가 이 상자에 표시됩니다.  
  
 **테이블 이름**  
 데이터 세트로 사용할 테이블의 이름을 입력합니다. 이 옵션은 **테이블**을 선택하면 표시됩니다.  
  
 **저장 프로시저 이름 선택 또는 입력**  
 사용할 저장 프로시저의 이름을 입력하거나 선택합니다. 식을 편집하려면 **식** 단추(*fx*)를 클릭합니다. 이 옵션은 저장 프로시저 명령 유형 옵션을 선택하면 표시됩니다.  
  
 **제한 시간(초)**  
 쿼리 제한 시간이 초과되기까지의 시간(초)을 입력합니다. 기본값은 30초입니다. **제한 시간** 값은 비워 두거나 0보다 커야 합니다. 값을 비워 두면 쿼리 시간이 제한되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [쿼리 디자이너&#40;보고서 작성기&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Reporting Services 쿼리 디자이너](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
