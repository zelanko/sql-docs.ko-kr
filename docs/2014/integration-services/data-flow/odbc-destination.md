---
title: ODBC 대상 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e398766c827f7611432f5ecd94353f1168e136b4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431900"
---
# <a name="odbc-destination"></a>ODBC 대상
  ODBC 대상은 ODBC 지원 데이터베이스 테이블로 데이터를 대량 로드합니다. ODBC 대상은 ODBC 연결 관리자를 사용하여 데이터 원본에 연결합니다.  
  
 ODBC 대상에는 입력 열과 대상 데이터 원본 열 사이의 매핑이 포함됩니다. 입력 열을 모든 대상 열에 매핑할 필요는 없지만 대상 열에 매핑된 입력 열이 없으면 대상 열의 속성에 따라 오류가 발생할 수 있습니다. 예를 들어 대상 열에 Null 값이 허용되지 않는 경우에는 입력 열을 해당 열에 매핑해야 합니다. 유형이 다른 열을 매핑할 수도 있지만 입력 데이터가 대상 열 유형과 호환되지 않으면 런타임에 오류가 발생합니다. 오류 동작 설정에 따라 오류가 무시되거나, 오류가 발생하거나, 오류 출력에 행이 전송됩니다.  
  
 ODBC 대상에는 하나의 일반 출력과 하나의 오류 출력이 있습니다.  
  
##  <a name="load-options"></a><a name="BKMK_odbcdestination_loadoptions"></a> 로드 옵션  
 ODBC 대상은 두 액세스 로드 모듈 중 하나를 사용할 수 있습니다. [ODBC 원본 편집기&#40;연결 관리자 페이지&#41;](../odbc-source-editor-connection-manager-page.md)에서 모드를 설정합니다. 두 모드는 다음과 같습니다.  
  
-   **일괄 처리**: 이 모드에서는 ODBC 대상이 인식된 ODBC 공급자 기능을 기반으로 가장 효율적인 삽입 메서드를 사용하려고 합니다. 대부분의 요즘 ODBC 공급자에게 이는 매개 변수가 포함된 INSERT 문을 준비한 다음 행 단위 배열 매개 변수 바인딩을 사용해야 함을 의미할 수 있습니다(배열 크기는 **BatchSize** 속성으로 제어됨). **일괄 처리** 를 선택했는데 공급자가 이 메서드를 지원하지 않으면 ODBC 대상이 **행 단위** 모드로 자동 전환됩니다.  
  
-   **행 단위**: 이 모드에서는 ODBC 대상이 매개 변수가 포함된 INSERT 문을 준비하고 **SQL 실행** 을 사용하여 한 번에 하나씩 행을 삽입합니다.  
  
## <a name="error-handling"></a>오류 처리  
 ODBC 대상에는 하나의 오류 출력이 있습니다. 구성 요소 오류 출력에 다음과 같은 출력 열이 포함됩니다.  
  
-   **오류 코드**: 현재 오류에 해당하는 숫자입니다. 오류 목록은 원본 데이터베이스에 대한 설명서를 참조하십시오. SSIS 오류 코드 목록은 SSIS 오류 코드 및 메시지 참조를 참조하십시오.  
  
-   **오류 열**: 오류의 원인이 되는 원본 열입니다(변환 오류의 경우).  
  
-   표준 출력 데이터 열입니다.  
  
 오류 동작 설정에 따라 ODBC 대상은 추출 프로세스 중 발생하는 오류(데이터 변환, 잘림)를 오류 출력에 반환하는 작업을 지원합니다. 자세한 내용은 [ODBC 원본 편집기&#40;오류 출력 페이지&#41;](../odbc-source-editor-error-output-page.md)를 참조하세요.  
  
## <a name="parallelism"></a>병렬 처리  
 동일한 컴퓨터 또는 서로 다른 컴퓨터에서 동일한 테이블 또는 서로 다른 테이블에 대해 병렬로 실행될 수 있는 ODBC 대상 구성 요소의 수에는 제한이 없습니다(일반적인 전역 세션 제한 제외).  
  
 그러나 이용 중인 ODBC 공급자의 제한으로 인해 공급자를 통한 동시 연결 수가 제한될 수 있습니다. 이러한 제한으로 인해 ODBC 대상에 대해 지원 가능한 병렬 인스턴스 수가 제한됩니다. SSIS 개발자는 이용 중인 모든 ODBC 공급자의 제한을 이해하고 SSIS 패키지를 작성할 때 해당 제한을 고려해야 합니다.  
  
 또한 동일한 테이블로 동시에 로드할 경우 표준 레코드 잠금 때문에 성능이 저하될 수 있다는 사실을 알고 있어야 합니다. 이는 로드되는 데이터와 테이블 구성에 따라 달라집니다.  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 대상 문제 해결  
 ODBC 원본이 외부 데이터 공급자에 대해 수행하는 호출을 기록할 수 있습니다. 이 로깅 기능을 사용하면 ODBC 대상이 외부 데이터 원본에 데이터를 저장할 때 발생하는 문제를 해결할 수 있습니다. ODBC 대상이 외부 데이터 공급자에 대해 수행하는 호출을 기록하려면 ODBC 드라이버 관리자 추적을 사용해야 합니다. 자세한 내용은 *ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법*에 대한 Microsoft 설명서를 참조하십시오.  
  
## <a name="configuring-the-odbc-destination"></a>ODBC 대상 구성  
 SSIS 디자이너를 사용하거나 프로그래밍 방식으로 ODBC 대상을 구성할 수 있습니다.  
  
 자세한 내용은 다음 항목 중 하나를 참조하십시오.  
  
-   [ODBC 대상 편집기&#40;연결 관리자 페이지&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 대상 편집기&#40;매핑 페이지&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 대상 편집기&#40;오류 출력 페이지&#41;](../odbc-destination-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
 **고급 편집기** 대화 상자를 열려면  
  
-   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 ODBC 대상을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
 고급 편집기 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [ODBC Destination Custom Properties](odbc-destination-custom-properties.md)을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC 대상 편집기&#40;오류 출력 페이지&#41;](../odbc-destination-editor-error-output-page.md)  
  
-   [ODBC 대상 편집기&#40;매핑 페이지&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 대상 편집기&#40;연결 관리자 페이지&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 대상을 사용하여 데이터 로드](odbc-destination.md)  
  
-   [ODBC Destination Custom Properties](odbc-destination-custom-properties.md)  
  
  
