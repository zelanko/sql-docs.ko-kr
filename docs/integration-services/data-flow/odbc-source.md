---
title: "ODBC 원본 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c8def299d18a8c7d64cd581fdf7934f366ce5dc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="odbc-source"></a>ODBC 원본
  ODBC 원본은 데이터베이스 테이블, 뷰 또는 SQL 문을 사용하여 ODBC 지원 데이터베이스에서 데이터를 추출합니다.  
  
 ODBC 원본은 데이터 추출을 위한 다음 데이터 액세스 모드를 제공합니다.  
  
-   테이블 또는 뷰  
  
-   SQL 문의 결과  
  
 원본은 이용할 공급자를 지정하는 ODBC 연결 관리자를 사용합니다.  
  
 ODBC 원본에는 원본 데이터 출력 열이 포함됩니다. 출력 열이 ODBC 대상에서 대상 열에 매핑될 경우 대상 열에 매핑된 출력 열이 없으면 오류가 발생할 수 있습니다. 유형이 다른 열을 매핑할 수 있지만 출력 데이터가 대상과 호환되지 않으면 런타임에 오류가 발생합니다. 오류 동작 설정에 따라 오류가 무시되거나, 오류가 발생하거나, 오류 출력에 행이 전송됩니다.  
  
 ODBC 원본에는 하나의 일반 출력과 하나의 오류 출력이 있습니다.  
  
## <a name="error-handling"></a>오류 처리  
 ODBC 원본에는 하나의 오류 출력이 있습니다. 구성 요소 오류 출력에 다음과 같은 출력 열이 포함됩니다.  
  
-   **오류 코드**: 현재 오류에 해당하는 숫자입니다. 오류 목록은 현재 사용하고 있는 ODBC 지원 데이터베이스에 대한 설명서를 참조하십시오. SSIS 오류 코드 목록은 SSIS 오류 코드 및 메시지 참조를 참조하십시오.  
  
-   **오류 열**: 오류의 원인이 되는 원본 열입니다(변환 오류의 경우).  
  
-   표준 출력 데이터 열입니다.  
  
 오류 동작 설정에 따라 ODBC 원본은 추출 프로세스 중 발생하는 오류(데이터 변환, 잘림)를 오류 출력에 반환하는 작업을 지원합니다. 자세한 내용은 [ODBC 대상 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)를 참조하세요.  
  
## <a name="data-type-support"></a>데이터 형식 지원  
 ODBC 원본이 지원하는 데이터 형식에 대한 자세한 내용은 Connector for ODBC(Open Database Connectivity)를 참조하세요.  
  
## <a name="extract-options"></a>추출 옵션  
 ODBC 원본은 **일괄 처리** 또는 **행 단위** 모드에서 작동합니다. 사용되는 모드는 **FetchMethod** 속성으로 결정됩니다. 다음 목록에서는 이러한 모드를 설명합니다.  
  
-   **일괄 처리**: 구성 요소가 인식된 ODBC 공급자 기능을 기반으로 가장 효율적인 인출 메서드를 사용하려고 합니다. 대부분의 최신 ODBC 공급자에게 이는 배열 바인딩을 사용한 SQLFetchScroll입니다(배열 크기는 **BatchSize** 속성으로 결정됨). **일괄 처리** 를 선택했는데 공급자가 이 메서드를 지원하지 않으면 ODBC 대상이 **행 단위** 모드로 자동 전환됩니다.  
  
-   **행 단위**: 구성 요소가 SQLFetch를 사용하여 한 번에 하나씩 행을 검색합니다.  
  
 **FetchMethod** 속성에 대한 자세한 내용은 [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md)을 참조하십시오.  
  
## <a name="parallelism"></a>Parallelism  
 동일한 컴퓨터 또는 서로 다른 컴퓨터에서 동일한 테이블 또는 서로 다른 테이블에 대해 병렬로 실행될 수 있는 ODBC 원본 구성 요소의 수에는 제한이 없습니다(일반적인 전역 세션 제한 제외).  
  
 그러나 이용 중인 ODBC 공급자의 제한으로 인해 공급자를 통한 동시 연결 수가 제한될 수 있습니다. 이러한 제한으로 인해 ODBC 원본에 대해 지원 가능한 병렬 인스턴스 수가 제한됩니다. SSIS 개발자는 이용 중인 모든 ODBC 공급자의 제한을 이해하고 SSIS 패키지를 작성할 때 해당 제한을 고려해야 합니다.  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 원본 문제 해결  
 ODBC 원본이 외부 데이터 공급자에 대해 수행하는 호출을 기록할 수 있습니다. 이 로깅 기능을 사용하면 ODBC 원본이 외부 데이터 원본에서 데이터를 로드할 때 발생하는 문제를 해결할 수 있습니다. ODBC 원본이 외부 데이터 공급자에 대해 수행하는 호출을 기록하려면 ODBC 드라이버 관리자 추적을 사용해야 합니다. 자세한 내용은 *ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법*에 대한 Microsoft 설명서를 참조하십시오.  
  
## <a name="configuring-the-odbc-source"></a>ODBC 원본 구성  
 SSIS 디자이너를 사용하거나 프로그래밍 방식으로 ODBC 원본을 구성할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
 **고급 편집기** 대화 상자를 열려면  
  
-   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 ODBC 원본을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
 고급 편집기 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md)을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC 원본을 사용하여 데이터 추출](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [ODBC 원본 사용자 지정 속성](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>ODBC 원본 편집기(연결 관리자 페이지)
  **ODBC 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 원본의 ODBC 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
### <a name="task-list"></a>작업 목록  
 **ODBC 원본 편집기의 연결 관리자 페이지를 열려면**  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 ODBC 원본이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
-   **데이터 흐름** 탭에서 ODBC 원본을 두 번 클릭합니다.  
  
### <a name="options"></a>변수  
  
#### <a name="connection-manager"></a>ODBC 원본 편집기  
 목록에서 기존 ODBC 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다. 어느 ODBC 지원 데이터베이스에나 연결할 수 있습니다.  
  
#### <a name="new"></a>단추를 사용하여 새  
 **새로 만들기**를 클릭합니다. 새 ODBC 연결 관리자를 만들 수 있는 **ODBC 연결 관리자 편집기 구성** 대화 상자가 열립니다.  
  
#### <a name="data-access-mode"></a>데이터 액세스 모드  
 원본에서 데이터를 선택하는 방법을 선택합니다. 옵션은 다음 표에 표시되어 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|테이블 이름|ODBC 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다. 이 옵션을 선택할 경우 다음 목록에서 값을 선택합니다.|  
||**테이블 또는 뷰 이름**: 목록에서 사용 가능한 테이블 또는 뷰를 선택하거나 테이블을 식별할 수 있는 정규식을 입력합니다.|  
||이 목록에는 처음 1000개의 테이블만 포함되어 있습니다. 데이터베이스에 포함되어 있는 테이블이 1000개를 넘는 경우 테이블 이름의 시작 부분을 입력하거나 와일드카드(*)를 통해 이름의 일부를 입력하여 사용할 테이블을 표시합니다.|  
|SQL 명령|SQL 쿼리를 사용하여 ODBC 데이터 원본에서 데이터를 검색합니다. 사용할 원본 데이터베이스의 구문으로 쿼리를 작성해야 합니다. 이 옵션을 선택할 경우 다음 중 한 가지 방법으로 쿼리를 입력합니다.|  
||**SQL 명령 텍스트** 필드에 SQL 쿼리 텍스트를 입력합니다.|  
||**찾아보기** 를 클릭하여 텍스트 파일에서 SQL 쿼리를 로드합니다.|  
||**쿼리 구문 분석** 을 클릭하여 쿼리 텍스트의 구문을 확인합니다.|  
  
#### <a name="preview"></a>미리 보기  
 **미리 보기** 를 클릭하면 선택한 테이블 또는 뷰에서 추출된 최대 200개의 데이터 행을 볼 수 있습니다.  
  
## <a name="odbc-source-editor-columns-page"></a>ODBC 원본 편집기(열 페이지)
  **ODBC 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
### <a name="task-list"></a>작업 목록  
 **ODBC 원본 편집기의 열 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 ODBC 원본이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ODBC 원본을 두 번 클릭합니다.  
  
3.  **ODBC 원본 편집기**에서 **열**을 클릭합니다.  
  
### <a name="options"></a>변수  
  
#### <a name="available-external-columns"></a>사용 가능한 외부 열  
 데이터 원본에서 사용 가능한 외부 열의 목록입니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다. 원본에서 사용할 열을 선택합니다. 선택한 열이 선택 순서대로 **외부 열** 목록에 추가됩니다.  
  
 모든 열을 선택하려면 **모두 선택** 확인란을 선택합니다.  
  
#### <a name="external-column"></a>외부 열  
 ODBC 원본의 데이터를 사용하는 구성 요소를 구성할 때 표시되는 순서로 된 외부(원본) 열의 뷰입니다.  
  
#### <a name="output-column"></a>출력 열  
 각 출력 열의 고유 이름을 입력합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 입력한 이름은 SSIS 디자이너에 표시됩니다.  
  
## <a name="odbc-source-editor-error-output-page"></a>ODBC 원본 편집기(오류 출력 페이지)
  **ODBC 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택할 수 있습니다.  
  
### <a name="task-list"></a>작업 목록  
 **ODBC 원본 편집기 오류 출력 페이지를 열려면**  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 ODBC 원본이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
-   **데이터 흐름** 탭에서 ODBC 원본을 두 번 클릭합니다.  
  
-   **ODBC 원본 편집기**에서 **오류 출력**을 클릭합니다.  
  
### <a name="options"></a>변수  
  
#### <a name="inputoutput"></a>입/출력  
 데이터 원본의 이름을 표시합니다.  
  
#### <a name="column"></a>Column  
 사용되지 않습니다.  
  
#### <a name="error"></a>Error  
 ODBC 원본에서 흐름의 오류를 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
#### <a name="truncation"></a>잘림  
 ODBC 원본에서 흐름의 잘림을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
#### <a name="description"></a>Description  
 사용되지 않습니다.  
  
#### <a name="set-this-value-to-selected-cells"></a>이 값을 선택한 셀에 설정  
 오류나 잘림 발생 시 ODBC 원본에서 선택한 모든 셀을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
#### <a name="apply"></a>적용  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
### <a name="error-handling-options"></a>오류 처리 옵션  
 다음 옵션을 사용하여 ODBC 원본에서 오류 및 잘림을 처리하는 방법을 구성할 수 있습니다.  
  
#### <a name="fail-component"></a>구성 요소 실패  
 오류 또는 잘림이 발생하면 데이터 흐름 태스크가 실패합니다. 이것이 기본 동작입니다.  
  
#### <a name="ignore-failure"></a>오류 무시  
 오류 또는 잘림이 무시됩니다.  
  
#### <a name="redirect-flow"></a>흐름 리디렉션  
 오류 또는 잘림을 발생시키는 행이 ODBC 원본의 오류 출력으로 전송됩니다.  
  
  
