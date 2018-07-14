---
title: CDC 원본 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff8eccaf0e1c13c63d73eff20e7415c6872c967b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269519"
---
# <a name="cdc-source"></a>CDC 원본
  CDC 원본은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 변경 테이블에서 특정 범위의 변경 데이터를 읽고 변경 내용을 다른 SSIS 다운스트림 구성 요소로 배달합니다.  
  
 CDC 원본이 읽는 변경 데이터의 범위를 CDC 처리 범위라고 합니다. 이 범위는 현재 데이터 흐름이 시작되기 전에 실행되는 CDC 제어 태스크에 의해 결정됩니다. CDC 처리 범위는 테이블 그룹의 CDC 처리 상태를 유지 관리하는 패키지 변수의 값에서 파생됩니다.  
  
 CDC 원본은 데이터베이스 테이블, 뷰 또는 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 추출합니다.  
  
 CDC 원본은 다음과 같은 구성을 사용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 데이터베이스에 액세스하기 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 연결 관리자 CDC 원본 연결을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [CDC 원본 편집기 &#40;연결 관리자 페이지&#41;](../cdc-source-editor-connection-manager-page.md)합니다.  
  
-   CDC용으로 설정된 테이블  
  
-   선택한 테이블에 대한 캡처 인스턴스의 이름(둘 이상이 있는 경우)  
  
-   변경 처리 모드  
  
-   CDC 처리 범위 결정의 기준이 되는 CDC 상태 패키지 변수의 이름. CDC 원본은 해당 변수를 수정하지 않습니다.  
  
 CDC 원본에 의해 반환되는 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 함수인 **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** 또는 **cdc.fn_cdc_get_net_changes_\<capture-instance-name>**(사용 가능한 경우)에 의해 반환되는 데이터와 같습니다. 현재 처리 범위가 테이블의 초기 로드와 겹칠 수 있는지 여부를 나타내는 **__$initial_processing** 열만 선택적으로 추가될 수 있습니다. 초기 처리에 대한 자세한 내용은 [CDC Control Task](../control-flow/cdc-control-task.md)를 참조하십시오.  
  
 CDC 원본에는 하나의 일반 출력과 하나의 오류 출력이 있습니다.  
  
## <a name="error-handling"></a>오류 처리  
 CDC 원본에는 하나의 오류 출력이 있습니다. 구성 요소 오류 출력에 다음과 같은 출력 열이 포함됩니다.  
  
-   **오류 코드**: 값은 항상 -1입니다.  
  
-   **오류 열**: 오류의 원인이 되는 원본 열입니다(변환 오류의 경우).  
  
-   **오류 행 열**: 오류의 원인이 되는 레코드 데이터입니다.  
  
 오류 동작 설정에 따라 CDC 원본은 추출 프로세스 중 발생하는 오류(데이터 변환, 잘림)를 오류 출력에 반환하는 작업을 지원합니다. 자세한 내용은 [CDC 원본 편집기 &#40;오류 출력 페이지&#41;](../cdc-source-editor-error-output-page.md)합니다.  
  
## <a name="data-type-support"></a>데이터 형식 지원  
 Microsoft용 CDC 원본 구성 요소는 올바른 SSIS 데이터 형식에 매핑되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC 원본 문제 해결  
 다음에는 CDC 원본 문제 해결에 대한 정보가 들어 있습니다.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>이 스크립트를 사용하여 문제를 격리하고 SQL Server Management Studio에서 해당 문제를 재현할 수 있습니다.  
 CDC 원본 작업은 CDC 원본을 호출하기 전에 실행되는 CDC 제어 태스크의 작업으로 제어됩니다. CDC 제어 태스크는 시작 및 끝 LSN을 포함하기 위해 CDC 상태 패키지 변수의 값을 준비합니다. 이 태스크는 다음 스크립트에 해당하는 함수를 실행합니다.  
  
```  
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
  
 **프로시저 또는 함수 cdc.fn_cdc_get_net_changes_\<..>** 에 제공된 인수 개수가 부족합니다.  
  
 이 오류는 인수가 누락되었음을 나타내지 않습니다. 대신 CDC 상태 변수의 시작 또는 끝 LSN 값이 잘못되었음을 의미합니다.  
  
## <a name="configuring-the-cdc-source"></a>CDC 원본 구성  
 SSIS 디자이너를 사용하거나 프로그래밍 방식으로 CDC 원본을 구성할 수 있습니다.  
  
 자세한 내용은 다음 항목 중 하나를 참조하십시오.  
  
-   [CDC 원본 편집기 &#40;연결 관리자 페이지&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 원본 편집기 &#40;열 페이지&#41;](../cdc-source-editor-columns-page.md)  
  
-   [CDC 원본 편집기 &#40;오류 출력 페이지&#41;](../cdc-source-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
 **고급 편집기** 대화 상자를 열려면  
  
-   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 CDC 원본을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
 **고급 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [CDC Source Custom Properties](cdc-source-custom-properties.md)을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [CDC 원본 편집기 &#40;연결 관리자 페이지&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 원본 편집기 &#40;열 페이지&#41;](../cdc-source-editor-columns-page.md)  
  
-   [CDC 원본 편집기 &#40;오류 출력 페이지&#41;](../cdc-source-editor-error-output-page.md)  
  
-   [CDC 원본 사용자 지정 속성](cdc-source-custom-properties.md)  
  
-   [CDC 원본을 사용하여 변경 데이터 추출](cdc-source.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   mattmasson.com의 블로그 항목 - [CDC 원본 처리 모드](http://go.microsoft.com/fwlink/?LinkId=242541)  
  
  
