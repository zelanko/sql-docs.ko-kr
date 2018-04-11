---
title: CDC 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.designer.cdcsource.f1
- sql13.ssis.designer.cdcsource.connection.f1
- sql13.ssis.designer.cdcsource.columns.f1
- sql13.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 632174b48536a4111125b24cfc85503ed6868a20
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="cdc-source"></a>CDC 원본
  CDC 원본은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 변경 테이블에서 특정 범위의 변경 데이터를 읽고 변경 내용을 다른 SSIS 다운스트림 구성 요소로 배달합니다.  
  
 CDC 원본이 읽는 변경 데이터의 범위를 CDC 처리 범위라고 합니다. 이 범위는 현재 데이터 흐름이 시작되기 전에 실행되는 CDC 제어 태스크에 의해 결정됩니다. CDC 처리 범위는 테이블 그룹의 CDC 처리 상태를 유지 관리하는 패키지 변수의 값에서 파생됩니다.  
  
 CDC 원본은 데이터베이스 테이블, 뷰 또는 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 추출합니다.  
  
 CDC 원본은 다음과 같은 구성을 사용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 데이터베이스에 액세스하기 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 연결 관리자 CDC 원본 연결 구성에 대한 자세한 내용은 [CDC 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)를 참조하세요.  
  
-   CDC용으로 설정된 테이블  
  
-   선택한 테이블에 대한 캡처 인스턴스의 이름(둘 이상이 있는 경우)  
  
-   변경 처리 모드  
  
-   CDC 처리 범위 결정의 기준이 되는 CDC 상태 패키지 변수의 이름. CDC 원본은 해당 변수를 수정하지 않습니다.  
  
 CDC 원본에 의해 반환되는 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 함수인 **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** 또는 **cdc.fn_cdc_get_net_changes_\<capture-instance-name>**(사용 가능한 경우)에 의해 반환되는 데이터와 같습니다. 현재 처리 범위가 테이블의 초기 로드와 겹칠 수 있는지 여부를 나타내는 **__$initial_processing** 열만 선택적으로 추가될 수 있습니다. 초기 처리에 대한 자세한 내용은 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)를 참조하십시오.  
  
 CDC 원본에는 하나의 일반 출력과 하나의 오류 출력이 있습니다.  
  
## <a name="error-handling"></a>오류 처리  
 CDC 원본에는 하나의 오류 출력이 있습니다. 구성 요소 오류 출력에 다음과 같은 출력 열이 포함됩니다.  
  
-   **오류 코드**: 값은 항상 -1입니다.  
  
-   **오류 열**: 오류의 원인이 되는 원본 열입니다(변환 오류의 경우).  
  
-   **오류 행 열**: 오류의 원인이 되는 레코드 데이터입니다.  
  
 오류 동작 설정에 따라 CDC 원본은 추출 프로세스 중 발생하는 오류(데이터 변환, 잘림)를 오류 출력에 반환하는 작업을 지원합니다.  
  
## <a name="data-type-support"></a>데이터 형식 지원  
 Microsoft용 CDC 원본 구성 요소는 올바른 SSIS 데이터 형식에 매핑되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC 원본 문제 해결  
 다음에는 CDC 원본 문제 해결에 대한 정보가 들어 있습니다.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>이 스크립트를 사용하여 문제를 격리하고 SQL Server Management Studio에서 해당 문제를 재현할 수 있습니다.  
 CDC 원본 작업은 CDC 원본을 호출하기 전에 실행되는 CDC 제어 태스크의 작업으로 제어됩니다. CDC 제어 태스크는 시작 및 끝 LSN을 포함하기 위해 CDC 상태 패키지 변수의 값을 준비합니다. 이 태스크는 다음 스크립트에 해당하는 함수를 실행합니다.  
  
```sql
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
-   \<cdc-enabled-database-name>은 변경 테이블을 포함하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 이름입니다.  
  
-   \<value-from-state-cs>는 CDC 상태 변수에 CS/\<value-from-state-cs>/로 나타나는 값입니다. CS는 현재 처리 범위 시작을 의미합니다.  
  
-   \<value-from-state-ce>는 CDC 상태 변수에 CE/\<value-from-state-cs>/로 나타나는 값입니다. CE는 현재 처리 범위 끝을 의미합니다.  
  
-   \<mode>는 CDC 처리 모드입니다. 처리 모드에는 **모두**, **이전 값이 포함된 모두**, **순**, **업데이트 마스크를 사용한 순 변경 내용**, **병합을 사용한 순 변경 내용**중 하나의 값이 지정됩니다.  
  
 이 스크립트는 오류를 식별하고 재현하기가 쉬운 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 문제를 재현하여 문제를 격리하는 데 도움이 됩니다.  
  
#### <a name="sql-server-error-message"></a>SQL Server 오류 메시지  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다음 메시지가 반환될 수 있습니다.  
  
 **프로시저 또는 함수 cdc.fn_cdc_get_net_changes_\<..>**에 제공된 인수 개수가 부족합니다.  
  
 이 오류는 인수가 누락되었음을 나타내지 않습니다. 대신 CDC 상태 변수의 시작 또는 끝 LSN 값이 잘못되었음을 의미합니다.  
  
## <a name="configuring-the-cdc-source"></a>CDC 원본 구성  
 SSIS 디자이너를 사용하거나 프로그래밍 방식으로 CDC 원본을 구성할 수 있습니다.  
  
 자세한 내용은 다음 항목 중 하나를 참조하십시오.  
  
-   [CDC 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 원본 편집기 & #40; 열 페이지 & #41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [CDC 원본 편집기 & #40; 오류 출력 페이지 & #41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
 **고급 편집기** 대화 상자를 열려면  
  
-   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 CDC 원본을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
 **고급 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md)을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [CDC 원본 사용자 지정 속성](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [CDC 원본을 사용하여 변경 데이터 추출](../../integration-services/data-flow/extract-change-data-using-the-cdc-source.md)  
  
## <a name="cdc-source-editor-connection-manager-page"></a>CDC 원본 편집기(연결 관리자 페이지)
  **CDC 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 CDC 원본이 변경 행을 읽어오는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스(CDC 데이터베이스)에 대한 ADO.NET 연결 관리자를 선택할 수 있습니다. CDC 데이터베이스를 선택한 후 데이터베이스에서 캡처된 테이블을 선택해야 합니다.  
  
 CDC 원본에 대한 자세한 내용은 [CDC Source](../../integration-services/data-flow/cdc-source.md)을 참조하십시오.  
  
### <a name="task-list"></a>작업 목록  
 **CDC 원본 편집기의 연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 CDC 원본이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 CDC 원본을 두 번 클릭합니다.  
  
3.  **CDC 원본 편집기**에서 **연결 관리자**를 클릭합니다.  
  
### <a name="options"></a>옵션  
 **ADO.NET 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다. CDC에 사용할 수 있고 선택한 변경 테이블이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결해야 합니다.  
  
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
  
-   **순 변경 내용**: 현재 CDC 처리 범위에서 수정된 원본 행당 하나의 변경 행만 반환합니다. 원본 행이 여러 번 업데이트된 경우에는 결합된 변경 내용이 생성됩니다. 예를 들어 삽입+업데이트는 단일 업데이트로 생성되고 업데이트+삭제는 단일 삭제로 생성됩니다. 순 변경 내용 처리 모드에서 작업할 경우 단일 원본 행이 두 개 이상의 출력에 나타나므로 변경 내용을 삭제, 삽입 및 업데이트 출력으로 분할하고 해당 출력을 병렬로 처리할 수 있습니다.  
  
-   **업데이트 마스크를 사용한 순 변경 내용**: 이 모드는 일반적인 순 변경 내용 모드와 비슷하지만 현재 변경 행에서 변경된 열을 나타내고 이름 패턴이 **__$\<column-name>\__Changed**인 부울 열도 추가합니다.  
  
-   **병합을 사용한 순 변경 내용**: 이 모드는 일반적인 순 변경 내용 모드와 비슷하지만 삽입 및 업데이트 작업을 사용할 경우 단일 병합 작업으로 병합됩니다(UPSERT).  
  
> [!NOTE]  
>  모든 순 변경 내용 옵션의 경우 원본 테이블에 기본 키 또는 고유 인덱스가 있어야 합니다. 기본 키 또는 고유 인덱스가 없는 테이블의 경우에는 **모두** 옵션을 사용해야 합니다.  
  
 **CDC 상태를 포함하는 변수**  
 현재 CDC 컨텍스트에 대한 CDC 상태를 유지 관리하는 SSIS 문자열 패키지 변수를 선택합니다. CDC 상태 변수에 대한 자세한 내용은 [상태 변수 정의](../../integration-services/data-flow/define-a-state-variable.md)를 참조하세요.  
  
 **재처리 표시기 열 포함**  
 **__$reprocessing**이라는 특수 출력 열을 만들려면 이 확인란을 선택합니다.  
  
 CDC 처리 범위가 초기 처리 범위(초기 로드 기간에 해당하는 LSN의 범위)와 겹치거나 이전 실행의 오류 발생 후 CDC 처리 범위가 다시 처리되는 경우 이 열 값은 **true** 입니다. 이 표시기 열을 사용하면 변경 내용을 다시 처리할 때 SSIS 개발자가 오류를 다르게 처리할 수 있습니다. 예를 들어 존재하지 않는 행의 삭제와 중복 키에 대해 실패한 삽입과 같은 동작은 무시할 수 있습니다.  
  
 자세한 내용은 [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md)을(를) 참조하세요.  
  
## <a name="cdc-source-editor-columns-page"></a>CDC 원본 편집기(열 페이지)
  **CDC 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
### <a name="task-list"></a>작업 목록  
 **CDC 원본 편집기의 열 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 CDC 원본이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 CDC 원본을 두 번 클릭합니다.  
  
3.  **CDC 원본 편집기**에서 **열**을 클릭합니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록입니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다. 원본에서 사용할 열을 선택합니다. 선택한 열이 선택 순서대로 **외부 열** 목록에 추가됩니다.  
  
 **외부 열**  
 CDC 원본의 데이터를 사용하는 구성 요소를 구성할 때 표시되는 순서로 된 외부(원본) 열의 뷰입니다. 순서를 변경하려면 먼저 **사용 가능한 열** 목록에서 선택한 열을 지운 다음 목록에서 외부 열을 다른 순서로 선택합니다. 선택한 열이 선택 순서대로 **외부 열** 목록에 추가됩니다.  
  
 **출력 열**  
 각 출력 열의 고유 이름을 입력합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 입력한 이름은 SSIS 디자이너에 표시됩니다.  
  
## <a name="cdc-source-editor-error-output-page"></a>CDC 원본 편집기(오류 출력 페이지)
  **CDC 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택할 수 있습니다.  
  
### <a name="task-list"></a>작업 목록  
 **CDC 원본 편집기 오류 출력 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 CDC 원본이 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 CDC 원본을 두 번 클릭합니다.  
  
3.  **CDC 원본 편집기**에서 **오류 출력**을 클릭합니다.  
  
### <a name="options"></a>옵션  
 **입/출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **CDC 원본 편집기** 대화 상자의 **연결 관리자** 페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
 **오류**  
 CDC 원본에서 흐름의 오류를 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **잘림**  
 CDC 원본에서 흐름의 잘림을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **Description**  
 사용되지 않습니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 CDC 원본에서 선택한 모든 셀을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
### <a name="error-handling-options"></a>오류 처리 옵션  
 다음 옵션을 사용하여 CDC 원본에서 오류 및 잘림을 처리하는 방법을 구성할 수 있습니다.  
  
 **구성 요소 실패**  
 오류 또는 잘림이 발생하면 데이터 흐름 태스크가 실패합니다. 이것이 기본 동작입니다.  
  
 **오류 무시**  
 오류 또는 잘림이 무시되고 데이터 행이 CDC 원본 출력으로 전달됩니다.  
  
 **흐름 리디렉션**  
 오류 또는 잘림 데이터 행이 CDC 원본의 오류 출력으로 전달됩니다. 이 경우에는 CDC 원본 오류 처리가 사용됩니다. 자세한 내용은 [CDC Source](../../integration-services/data-flow/cdc-source.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
  
-   mattmasson.com의 블로그 항목 - [CDC 원본 처리 모드](http://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/)  
  
  
