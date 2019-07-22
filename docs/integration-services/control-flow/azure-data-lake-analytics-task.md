---
title: Azure Data Lake Analytics 태스크 | Microsoft Docs
description: Azure Data Lake Analytics 태스크를 사용하여 U-SQL 작업을 Azure Data Lake Analytics 서비스에 제출할 수 있습니다.
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
ms.openlocfilehash: ab9a357e8215310b21fa2e401067f49176aeefd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947353"
---
# <a name="azure-data-lake-analytics-task"></a>Azure Data Lake Analytics 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Azure Data Lake Analytics 태스크를 사용하여 U-SQL 작업을 Azure Data Lake Analytics 서비스에 제출할 수 있습니다. 이 태스크는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

일반적인 백그라운드는 [Azure Data Lake Analytics](https://azure.microsoft.com/services/data-lake-analytics/)를 참조하세요.

## <a name="configure-the-task"></a>태스크 구성

패키지에 Data Lake Analytics 태스크를 추가하려면 SSIS 도구 상자에서 디자이너 캔버스로 태스크를 끕니다. 그런 후 태스크를 두 번 클릭하거나 태스크를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다. **Azure Data Lake Analytics 태스크 편집기** 대화 상자가 열립니다. SSIS 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.

## <a name="general-page-configuration"></a>일반 페이지 구성

**일반** 페이지를 사용하여 태스크를 구성하고 태스크가 제출하는 U-SQL 스크립트를 제공합니다. U-SQL 언어에 대한 자세한 내용은 [U-SQL Language Reference](/u-sql/)(U-SQL 언어 참조)를 참조하세요.

### <a name="basic-configuration"></a>기본 구성

태스크의 이름 및 설명을 지정할 수 있습니다.

### <a name="u-sql-configuration"></a>U-SQL 구성

U-SQL 구성에는 다음 두 가지 설정이 있습니다. **SourceType** 및 **SourceType** 값을 기반으로 하는 동적 옵션. 

**SourceType**은 U-SQL 스크립트의 원본을 지정합니다. SSIS 패키지 실행 중에 Data Lake Analytics 계정에 스크립트가 제출됩니다. 이 속성의 옵션은 다음과 같습니다.

|값|설명|  
|-----------|-----------------|  
|**DirectInput**|인라인 편집기를 통해 U-SQL 스크립트를 지정합니다. 이 값을 선택하면 동적 옵션 **USQLStatement**가 표시됩니다.|  
|**FileConnection**|U-SQL 스크립트를 포함하는 로컬 .usql 파일을 지정합니다. 이 옵션을 설정하면 동적 옵션 **FileConnection**이 표시됩니다.|  
|**변수**|U-SQL 스크립트를 포함하는 SSIS 변수를 지정합니다. 이 값을 선택하면 동적 옵션 **SourceVariable**이 표시됩니다.|

**SourceType 동적 옵션**은 U-SQL 쿼리의 스크립트 콘텐츠를 지정합니다. 

|SourceType|동적 옵션|  
|-----------|-----------------|  
|**SourceType = DirectInput**|옵션 상자에서 직접 제출할 U-SQL 쿼리를 입력하거나 [찾아보기] 단추(...)를 선택하여 **U-SQL 쿼리 입력** 대화 상자에 U-SQL 쿼리를 입력합니다.|  
|**SourceType = FileConnection**|기존 파일 연결 관리자를 선택하거나 <**새 연결...** >을 선택하여 새 파일 연결을 만듭니다. 관련 내용은 [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md) 및 [파일 연결 관리자 편집기](../../integration-services/connection-manager/file-connection-manager-editor.md)를 참조하세요.|  
|**SourceType = Variable**|기존 변수를 선택하거나 \<**새 변수...** >를 선택하여 새 변수를 만듭니다. 관련 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [변수 추가](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)를 참조하세요.|


### <a name="job-configuration"></a>작업 구성
작업 구성은 U-SQL 작업 제출 속성을 지정합니다.

- **AzureDataLakeAnalyticsConnection:** U-SQL 스크립트가 제출되는 Data Lake Analytics 계정을 지정합니다. 정의된 연결 관리자 목록에서 연결을 선택합니다. 새 연결을 만들려면 <**새 연결...** >을 선택합니다. 관련 내용은 [Azure Data Lake Analytics 연결 관리자](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)를 참조하세요.

- **JobName:** U-SQL 작업의 이름을 지정합니다. 
- **AnalyticsUnits:** U-SQL 작업의 분석 단위 수를 지정합니다.
- **Priority:** U-SQL 작업의 우선순위를 지정합니다. 이 항목은 0~1000 사이의 값으로 설정할 수 있습니다. 숫자가 작을수록 우선 순위가 높습니다.
- **RuntimeVersion:** U-SQL 작업의 Data Lake Analytics 런타임 버전을 지정합니다. 기본적으로 “default”로 설정됩니다. 일반적으로 이 속성을 변경할 필요가 없습니다.
- **Synchronous:** 작업 실행이 완료될 때까지 태스크가 기다릴지 여부를 지정하는 부울 값입니다. 값이 true로 설정되면 작업이 완료된 후 태스크가 **성공**으로 표시됩니다. 값이 false로 설정되면 작업이 준비 단계를 통과한 후 태스크가 **성공**으로 표시됩니다.

  |값|설명|
  |-----------|-----------------|
  |True|태스크 결과는 U-SQL 작업 실행 결과를 기반으로 합니다. 작업 성공 > 태스크 성공. 작업 실패 > 태스크 실패. 태스크 성공 또는 실패 > 태스크 완료.|
  |False|태스크 결과는 U-SQL 작업 제출 및 준비 결과를 기반으로 합니다. 작업 제출 성공 및 준비 단계 통과 > 태스크 성공. 작업 제출 실패 또는 준비 단계에서 작업 실패 > 태스크 실패. 태스크 성공 또는 실패 > 태스크 완료.|

- **TimeOut:** 작업 실행을 위한 시간 제한 시간(초)을 지정합니다. 작업 시간이 초과되면 작업이 취소되고 실패로 표시됩니다. **Synchronous**가 false로 설정되면 이 속성을 사용할 수 없습니다.

## <a name="parameter-mapping-page-configuration"></a>매개 변수 매핑 페이지 구성

**Azure Data Lake Analytics 태스크 편집기** 대화 상자의 **매개 변수 매핑** 페이지를 사용하여 변수를 U-SQL 스크립트의 매개 변수(U-SQL 변수)에 매핑합니다.

- **변수 이름:** **추가**를 선택하여 매개 변수 매핑을 추가한 후 목록에서 시스템 또는 사용자 정의 변수를 선택합니다. 또는 <**새 변수...** >를 선택하여 **변수 추가** 대화 상자에서 새 변수를 추가할 수 있습니다. 관련 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)를 참조하세요.  

- **매개 변수 이름:** U-SQL 스크립트에 매개 변수/변수 이름을 제공합니다. 매개 변수 이름이 \@Param1과 같이 \@ 기호로 시작하는지 확인합니다. 

다음은 U-SQL 스크립트에 매개 변수를 전달하는 방법의 예제입니다.

**샘플 U-SQL 스크립트**
```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

입력 및 출력 경로는 **\@in** 및 **\@out** 매개 변수에 정의됩니다. U-SQL 스크립트에서 **\@in** 및 **\@out** 매개 변수의 값은 매개 변수 매핑 구성을 통해 동적으로 전달됩니다.

|변수 이름|매개 변수 이름|
|-------------|--------------|
|사용자: Variable1|\@in|
|사용자: Variable2|\@out| 

## <a name="expression-page-configuration"></a>식 페이지 구성

일반 페이지 구성의 모든 속성을 속성 식으로 할당하여 런타임에 속성의 동적 업데이트를 사용할 수 있습니다. 자세한 내용은 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.

## <a name="see-also"></a>관련 항목:
- [Azure Data Lake Analytics 연결 관리자](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Azure Data Lake Store 파일 시스템 태스크](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Azure Data Lake Store 연결 관리자](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

