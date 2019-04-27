---
title: CDC 원본 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0e421d6ba1aaf69c04a450d8d93ff1ddf385935
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771779"
---
# <a name="cdc-source-editor-connection-manager-page"></a>CDC 원본 편집기(연결 관리자 페이지)
  **CDC 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 CDC 원본이 변경 행을 읽어오는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 데이터베이스(CDC 데이터베이스)에 대한 ADO.NET 연결 관리자를 선택할 수 있습니다. CDC 데이터베이스를 선택한 후 데이터베이스에서 캡처된 테이블을 선택해야 합니다.  
  
 CDC 원본에 대한 자세한 내용은 [CDC Source](data-flow/cdc-source.md)을 참조하십시오.  
  
## <a name="task-list"></a>작업 목록  
 **CDC 원본 편집기의 연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 CDC 원본이 있는 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 CDC 원본을 두 번 클릭합니다.  
  
3.  **CDC 원본 편집기**에서 **연결 관리자**를 클릭합니다.  
  
## <a name="options"></a>변수  
 **ADO.NET 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다. CDC에 사용할 수 있고 선택한 변경 테이블이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 연결해야 합니다.  
  
 **새로 만들기**  
 **새로 만들기**를 클릭합니다. 새 연결 관리자를 만들 수 있는 **ADO.NET 연결 관리자 편집기 구성** 대화 상자가 열립니다.  
  
 **CDC 테이블**  
 처리하기 위해 읽고 다운스트림 SSIS 구성 요소에 제공하려는 캡처된 변경 내용이 포함된 CDC 원본 테이블을 선택합니다.  
  
 **캡처 인스턴스**  
 읽을 CDC 테이블이 있는 CDC 캡처 인스턴스의 이름을 선택하거나 입력합니다.  
  
 캡처된 원본 테이블에는 스키마 변경을 통해 테이블 정의의 원활한 전환을 처리하도록 하나 또는 두 개의 캡처된 인스턴스가 포함되어 있을 수 있습니다. 캡처할 원본 테이블에 대해 두 개 이상의 캡처 인스턴스가 정의되어 있으면 여기에서 사용할 캡처 인스턴스를 선택합니다. [schema].[table] 테이블의 기본 캡처 인스턴스 이름은 \<schema>_\<table>이지만 실제로 사용 중인 캡처 인스턴스 이름은 다를 수 있습니다. 실제로 읽어 올 테이블은 CDC 테이블 **cdc .\<capture-instance>_CT**입니다.  
  
 **CDC 처리 모드**  
 처리 요구를 처리할 최적의 처리 모드를 선택합니다. 가능한 옵션은 아래와 같습니다.  
  
-   **모두**: **업데이트 전** 값이 없는 현재 CDC 범위의 변경 내용을 반환합니다.  
  
-   **이전 값이 포함된 모두**: 이전 값(**업데이트 전**)을 포함한 현재 CDC 처리 범위의 변경 내용을 반환합니다. 각 업데이트 작업에 대해 두 행이 있습니다. 이 중 한 행에는 업데이트 전 값이 포함되어 있고 다른 한 행에는 업데이트 후 값이 포함되어 있습니다.  
  
-   **Net**: 현재 CDC 처리 범위에서 수정 된 원본 행당 하나의 변경 행을 반환 합니다. 원본 행이 여러 번 업데이트된 경우에는 결합된 변경 내용이 생성됩니다. 예를 들어 삽입+업데이트는 단일 업데이트로 생성되고 업데이트+삭제는 단일 삭제로 생성됩니다. 순 변경 내용 처리 모드에서 작업할 경우 단일 원본 행이 두 개 이상의 출력에 나타나므로 변경 내용을 삭제, 삽입 및 업데이트 출력으로 분할하고 해당 출력을 병렬로 처리할 수 있습니다.  
  
-   **업데이트 마스크를 사용한 순 변경 내용**: 이 모드는 일반적인 순 변경 내용 모드와 비슷하지만 현재 변경 행에서 변경된 열을 나타내고 이름 패턴이 **__$\<column-name>\__Changed**인 부울 열도 추가합니다.  
  
-   **병합을 사용한 순 변경 내용**: 이 모드는 일반적인 유사한 순 변경 내용 모드 삽입 및 업데이트 작업으로 병합 경우 단일 병합 작업 (UPSERT).  
  
> [!NOTE]  
>  모든 순 변경 내용 옵션의 경우 원본 테이블에 기본 키 또는 고유 인덱스가 있어야 합니다. 기본 키 또는 고유 인덱스가 없는 테이블의 경우에는 **모두** 옵션을 사용해야 합니다.  
  
 **CDC 상태를 포함하는 변수**  
 현재 CDC 컨텍스트에 대한 CDC 상태를 유지 관리하는 SSIS 문자열 패키지 변수를 선택합니다. CDC 상태 변수에 대한 자세한 내용은 [상태 변수 정의](data-flow/define-a-state-variable.md)를 참조하세요.  
  
 **재처리 표시기 열 포함**  
 **__$reprocessing**이라는 특수 출력 열을 만들려면 이 확인란을 선택합니다.  
  
 CDC 처리 범위가 초기 처리 범위(초기 로드 기간에 해당하는 LSN의 범위)와 겹치거나 이전 실행의 오류 발생 후 CDC 처리 범위가 다시 처리되는 경우 이 열 값은 **true** 입니다. 이 표시기 열을 사용하면 변경 내용을 다시 처리할 때 SSIS 개발자가 오류를 다르게 처리할 수 있습니다. 예를 들어 존재하지 않는 행의 삭제와 중복 키에 대해 실패한 삽입과 같은 동작은 무시할 수 있습니다.  
  
 자세한 내용은 [CDC Source Custom Properties](data-flow/cdc-source-custom-properties.md)을(를) 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CDC 원본 편집기&#40;열 페이지&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)   
 [CDC 원본 편집기&#40;오류 출력 페이지&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  
