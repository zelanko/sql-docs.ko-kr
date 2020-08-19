---
description: OData 원본
title: OData 원본 | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f74fa8478953c4c1353d35f49250896ab2a7ab8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425825"
---
# <a name="odata-source"></a>OData 원본

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


SSIS 패키지의 OData 원본 구성 요소를 사용하여 Open Data Protocol(OData) 서비스에서 데이터를 사용할 수 있습니다.

## <a name="supported-protocols-and-data-formats"></a>지원되는 프로토콜 및 데이터 형식

구성 요소는 OData v3 및 v4 프로토콜을 지원합니다.  
  
-   OData V3 프로토콜의 경우 구성 요소는 ATOM 및 JSON 데이터 형식을 지원합니다.  
  
-   OData V4 프로토콜의 경우 구성 요소는 JSON 데이터 형식을 지원합니다.  

## <a name="supported-data-sources"></a>지원되는 데이터 원본

OData 원본에는 다음 데이터 원본에 대한 지원이 포함됩니다.
-   Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online
-   SharePoint 목록 SharePoint 서버의 모든 목록을 보려면 URL `https://<server>/_vti_bin/ListData.svc`를 사용합니다. SharePoint URL 규칙에 대한 자세한 내용은 [SharePoint Foundation REST 인터페이스](https://msdn.microsoft.com/library/ff521587.aspx)를 참조하십시오.

## <a name="supported-data-types"></a>지원되는 데이터 형식

OData 원본은 단순 데이터 형식 int, byte[], bool, byte, DateTime, DateTimeOffset, decimal, double, Guid, Int16, Int32, Int64, sbyte, float, string 및 TimeSpan을 지원합니다.

데이터 원본에 있는 열의 데이터 형식을 검색하려면 `https://<OData feed endpoint>/$metadata` 페이지를 확인입니다.

**Decimal** 데이터 형식의 전체 자릿수와 소수 자릿수는 원본 메타데이터에서 결정됩니다. 원본 메타데이터에서 **전체 자릿수** 및 **소수 자릿수** 속성을 지정하지 않는 경우 데이터가 잘릴 수 있습니다.

> [!IMPORTANT]
> OData 원본 구성 요소는 SharePoint 목록에서 다중 선택 항목과 같은 복합 형식을 지원하지 않습니다.

## <a name="odata-format-and-performance"></a>OData 형식 및 성능
 대부분의 OData 서비스는 여러 형식으로 결과를 반환할 수 있습니다. `$format` 쿼리 옵션을 사용하여 결과 집합의 형식을 지정할 수 있습니다. JSON 및 JSON Light와 같은 형식은 ATOM 또는 XML보다 효율적이며 많은 양의 데이터를 전송하는 경우 더 나은 성능을 제공할 수 있습니다. 다음 표에서는 샘플 테스트의 결과를 제공합니다. 표에 나와 있듯이 ATOM에서 JSON으로 전환하는 경우 성능이 30-53% 향상되었고, ATOM에서 새로운 JSON Light 형식(WCF Data Services 5.1에서 사용 가능)으로 전환하는 경우에는 성능이 67% 향상되었습니다.  
  
|행|ATOM|JSON|JSON(Light)|  
|-|-|-|-|  
|10000|113초|74초|68초|  
|1000000|1110초|853초|665초|  
  
## <a name="related-topics-in-this-section"></a>이 섹션의 관련 항목  
  
-   [자습서: OData 원본 사용](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [런타임에 OData 원본 쿼리 수정](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData 원본 속성](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>OData 원본 편집기(연결 페이지)
  **OData 원본 편집기** 대화 상자의 **연결** 페이지를 사용하여 OData 원본의 OData 연결 관리자를 선택할 수 있습니다. 또한 이 페이지에서 컬렉션 또는 리소스 경로와 쿼리 옵션을 지정하여 OData 원본에서 검색해야 하는 데이터를 나타낼 수 있습니다. 
  
### <a name="static-options"></a>정적 옵션  
 **OData 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 연결 관리자를 선택하거나 만든 후 대화 상자는 연결 관리자가 사용하는 OData 프로토콜 버전을 표시합니다.  
  
 **새로 만들기**  
 **OData 연결 관리자 편집기** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **컬렉션 또는 리소스 경로 사용**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|컬렉션|컬렉션 이름을 사용하여 OData 원본에서 데이터를 검색합니다.|  
|리소스 경로|리소스 경로를 사용하여 OData 원본에서 데이터를 검색합니다.|  
  
 **쿼리 옵션**  
 쿼리에 대한 옵션을 지정합니다. 예: `$top=5` 
  
 **피드 URL**  
 이 대화 상자에서 선택한 옵션에 따라 읽기 전용 피드 URL을 표시합니다.  
  
 **미리 보기**  
 **미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. **미리 보기** 에는 최대 20개의 행이 표시될 수 있습니다.  
  
### <a name="dynamic-options"></a>동적 옵션  
  
#### <a name="use-collection-or-resource-path--collection"></a>컬렉션 또는 리소스 경로 사용 = 컬렉션  
 **컬렉션**  
 드롭다운 목록에서 컬렉션을 선택합니다.  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>컬렉션 또는 리소스 경로 사용 = 리소스 경로  
 **Resource path**  
 리소스 경로를 입력합니다. 예: Employees  
  
## <a name="odata-source-editor-columns-page"></a>OData 원본 편집기(열 페이지)
  **OData 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력에 포함될 외부(원본) 열을 선택하고 출력 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 원본 열의 목록을 표시합니다. 목록의 확인란을 사용하여 페이지의 아래쪽에 있는 테이블에 열을 추가하거나 제거할 수 있습니다. 선택한 열이 출력에 추가됩니다.  
  
 **외부 열**  
 출력에 포함되도록 선택한 원본 열을 표시합니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
## <a name="odata-source-editor-error-output-page"></a>OData 원본 편집기(오류 출력 페이지)
  **OData 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택하고 오류 출력 열에 속성을 설정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **입/출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **OData 원본 편집기** 대화 상자의 **연결 관리자** 페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
 **오류**  
 오류가 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **관련 항목:** [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **잘림**  
 잘림이 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **설명**  
 오류에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [OData 연결 관리자](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
