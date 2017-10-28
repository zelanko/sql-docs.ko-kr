---
title: "Reporting Services 보고서의 처리 문제 해결 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
caps.latest.revision: 4
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8df3dd891b236ca295a4cc0deebdc5768d06dffa
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>Reporting Services 보고서의 처리 문제 해결
보고서 데이터가 검색되면 보고서 처리기는 데이터와 레이아웃 정보를 조합합니다. 식이 포함된 각 보고서 항목 속성은 조합된 데이터와 레이아웃의 컨텍스트에서 계산됩니다. 이 항목에서는 이러한 문제를 해결하는 데 유용한 정보를 제공합니다.   
  
## <a name="my-report-definition-is-not-valid"></a>보고서 정의가 유효하지 않은 경우  
런타임에 보고서 처리기는 보고서 정의에 있는 데이터와 레이아웃 요소를 조합하고 보고서 항목 속성의 식을 계산합니다.   
  
보고서 처리기는 보고서 정의(.rdl 파일)가 .rdl 파일의 시작 부분에 있는 네임스페이스 선언에 정의된 스키마를 따르는지 확인합니다. RDL 스키마에 대한 자세한 내용은 [보고서 정의 스키마 버전(SSRS) 찾기](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)를 참조하세요.  
  
또한 런타임에 계산되는 보고서 식은 보고서 데이터 및 레이아웃이 올바르게 조합될 수 있도록 보장하는 일련의 규칙을 따라야 합니다. 보고서 처리기가 문제를 발견하면 ' `<report name>` 보고서의 정의가 잘못되었습니다'라는 메시지가 표시될 수 있습니다.  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>보고서 항목 식은 현재 데이터 집합 범위 내의 필드만 참조하거나, 집계 함수 내에 있는 경우 지정한 데이터 집합 범위만 참조할 수 있음  
  
다음 목록을 사용하여 오류 원인을 확인할 수 있습니다.  
* 보고서에 두 개 이상의 데이터 집합이 포함된 경우 보고서 본문의 입력란에 있는 집계 식이 범위 매개 변수를 지정해야 합니다. `=First(Fields!FieldName.Value, "DataSet1")`)을 입력합니다.  
  
범위 매개 변수를 지정하려면 보고서 항목에 대한 범위에 포함되는 데이터 집합, 데이터 영역 또는 그룹의 이름을 제공합니다. 자세한 내용은 [합계, 집계 및 기본 제공 컬렉션에 대한 식 범위 이해(보고서 작성기 3.0 및 SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 및 [식 참조(보고서 작성기 3.0 및 SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>개체 이름은 0보다 크고 256자 이하여야 함  
보고서 정의의 개체 식별자 길이는 256자로 제한됩니다. 식별자는 대/소문자를 구분하고 CLS 규격이어야 합니다. 이름은 문자로 시작해야 하고 문자, 숫자 또는 밑줄(_)로 구성되어야 하며 공백은 포함할 수 없습니다. 예를 들어 입력란 이름 또는 데이터 영역 이름은 이러한 지침을 따라야 합니다.   
  
개체 이름을 변경하려면 속성 창의 도구 모음에 있는 드롭다운 목록에서 항목을 선택한 후 **이름** 으로 스크롤하고 올바른 개체 이름을 입력합니다.   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>입력란에 표시된 "#오류" 관련 문제 해결 방법  
보고서 처리기가 런타임에 보고서 항목 속성에서 식을 평가할 때 데이터 형식 변환, 범위 또는 기타 오류가 발견될 경우 "#오류" 메시지가 발생합니다.   
  
데이터 형식 오류는 일반적으로 기본 또는 지정된 데이터 형식이 지원되지 않음을 의미하고, 범위 오류는 식을 평가할 당시에 지정된 범위를 사용할 수 없었음을 의미합니다.   
  
#오류 메시지를 제거하려면 이 오류의 원인이 되는 식을 다시 작성해야 합니다. 이 문제에 대한 자세한 내용을 확인하려면 자세한 오류 메시지를 검토하십시오.   
  
[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)]의 미리 보기에서 출력 창을 봅니다. 보고서 서버에서 호출 스택을 봅니다. 
  
  
## <a name="see-also"></a>관련 항목:  
[오류 및 이벤트(Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


