---
title: ODBC 원본 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b928b54236929238c404597f4ba1eeeddb427ccc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790645"
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
  
 오류 동작 설정에 따라 ODBC 원본은 추출 프로세스 중 발생하는 오류(데이터 변환, 잘림)를 오류 출력에 반환하는 작업을 지원합니다. 자세한 내용은 [ODBC 대상 편집기&#40;연결 관리자 페이지&#41;](../odbc-destination-editor-connection-manager-page.md)를 참조하세요.  
  
## <a name="data-type-support"></a>데이터 형식 지원  
 ODBC 원본이 지원하는 데이터 형식에 대한 자세한 내용은 Connector for ODBC(Open Database Connectivity) by Attunity를 참조하십시오.  
  
## <a name="extract-options"></a>추출 옵션  
 ODBC 원본은 **일괄 처리** 또는 **행 단위** 모드에서 작동합니다. 사용되는 모드는 **FetchMethod** 속성으로 결정됩니다. 다음 목록에서는 이러한 모드를 설명합니다.  
  
-   **일괄 처리**: 구성 요소가 인식된 ODBC 공급자 기능을 기반으로 가장 효율적인 인출 메서드를 사용하려고 합니다. 대부분의 최신 ODBC 공급자에게 이는 배열 바인딩을 사용한 SQLFetchScroll입니다(배열 크기는 **BatchSize** 속성으로 결정됨). **일괄 처리** 를 선택했는데 공급자가 이 메서드를 지원하지 않으면 ODBC 대상이 **행 단위** 모드로 자동 전환됩니다.  
  
-   **행 단위**: 구성 요소가 SQLFetch를 사용하여 한 번에 하나씩 행을 검색합니다.  
  
 **FetchMethod** 속성에 대한 자세한 내용은 [ODBC Source Custom Properties](odbc-source-custom-properties.md)을 참조하십시오.  
  
## <a name="parallelism"></a>Parallelism  
 동일한 컴퓨터 또는 서로 다른 컴퓨터에서 동일한 테이블 또는 서로 다른 테이블에 대해 병렬로 실행될 수 있는 ODBC 원본 구성 요소의 수에는 제한이 없습니다(일반적인 전역 세션 제한 제외).  
  
 그러나 이용 중인 ODBC 공급자의 제한으로 인해 공급자를 통한 동시 연결 수가 제한될 수 있습니다. 이러한 제한으로 인해 ODBC 원본에 대해 지원 가능한 병렬 인스턴스 수가 제한됩니다. SSIS 개발자는 이용 중인 모든 ODBC 공급자의 제한을 이해하고 SSIS 패키지를 작성할 때 해당 제한을 고려해야 합니다.  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 원본 문제 해결  
 ODBC 원본이 외부 데이터 공급자에 대해 수행하는 호출을 기록할 수 있습니다. 이 로깅 기능을 사용하면 ODBC 원본이 외부 데이터 원본에서 데이터를 로드할 때 발생하는 문제를 해결할 수 있습니다. ODBC 원본이 외부 데이터 공급자에 대해 수행하는 호출을 기록하려면 ODBC 드라이버 관리자 추적을 사용해야 합니다. 자세한 내용은 *ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법*에 대한 Microsoft 설명서를 참조하십시오.  
  
## <a name="configuring-the-odbc-source"></a>ODBC 원본 구성  
 SSIS 디자이너를 사용하거나 프로그래밍 방식으로 ODBC 원본을 구성할 수 있습니다.  
  
 자세한 내용은 다음 항목 중 하나를 참조하십시오.  
  
-   [ODBC 원본 편집기&#40;연결 관리자 페이지&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [ODBC 원본 편집기&#40;열 페이지&#41;](../odbc-source-editor-columns-page.md)  
  
-   [ODBC 원본 편집기&#40;오류 출력 페이지&#41;](../odbc-source-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
 **고급 편집기** 대화 상자를 열려면  
  
-   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 ODBC 원본을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
 고급 편집기 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [ODBC Source Custom Properties](odbc-source-custom-properties.md)을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC 원본 편집기&#40;오류 출력 페이지&#41;](../odbc-source-editor-error-output-page.md)  
  
-   [ODBC 원본 편집기&#40;열 페이지&#41;](../odbc-source-editor-columns-page.md)  
  
-   [ODBC 원본 편집기&#40;연결 관리자 페이지&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [ODBC 원본을 사용하여 데이터 추출](odbc-source.md)  
  
-   [ODBC Source Custom Properties](odbc-source-custom-properties.md)  
  
  
