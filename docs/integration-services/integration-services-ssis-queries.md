---
title: Integration Services(SSIS) 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e3603e4eb3f446518562eec82cf33d02d0ff1fa
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411665"
---
# <a name="integration-services-ssis-queries"></a>Integration Services(SSIS) 쿼리
  SQL 쿼리는 SQL 실행 태스크, OLE DB 원본, OLE DB 대상 및 조회 변환에서 사용될 수 있습니다. SQL 실행 태스크에서 SQL 문은 데이터베이스 개체 및 데이터를 생성, 업데이트 및 삭제할 수 있으며 저장 프로시저를 실행하고 SELECT 문을 수행할 수 있습니다. OLE DB 원본 및 조회 변환에서 일반적으로 SQL 문은 SELECT 문 또는 EXEC 문입니다. 후자는 결과 집합을 반환하는 저장 프로시저를 가장 자주 실행합니다.  
  
 쿼리 유효성 여부를 확인하기 위해 구문 분석을 수행할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 연결을 사용하는 쿼리를 구문 분석하는 경우 쿼리를 구문 분석하고 실행한 다음 구문 분석 결과에 실행 결과(성공 또는 실패)를 할당합니다. 쿼리가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]이외의 데이터로의 연결을 사용하는 경우 문은 구문 분석만 됩니다.  
  
다음과 같은 방법으로 SQL 문을 제공할 수 있습니다.
1.   디자이너에서 직접 입력합니다.
2.   명령문이 포함된 파일에 대한 연결을 지정합니다.
3.   명령문이 포함된 변수를 지정합니다.  
  
## <a name="direct-input-sql"></a>SQL 직접 입력  
 쿼리 작성기는 SQL 실행 태스크, OLE DB 원본, OLE DB 대상 및 조회 변환의 사용자 인터페이스에서 사용할 수 있습니다. 쿼리 작성기를 사용하면 다음과 같은 이점이 있습니다.  
  
-   시각적으로 또는 SQL 명령으로 작업합니다.  
  
     쿼리 작성기는 쿼리를 시각적으로 구성하는 그래픽 창과 쿼리의 SQL 텍스트를 표시하는 텍스트 창을 포함합니다. 그래픽 또는 텍스트 창에서 작업할 수 있습니다. 쿼리 작성기는 뷰를 동기화하므로 쿼리 텍스트와 그래픽 표현이 항상 일치합니다.  
  
-   관련 테이블을 조인합니다.  
  
     둘 이상의 테이블을 쿼리에 추가하면 쿼리 작성기는 테이블이 관련되는 방법과 적절한 조인 명령을 생성하는 방법을 자동으로 결정합니다.  
  
-   데이터베이스를 쿼리 또는 업데이트할 수 있습니다.  
  
     쿼리 작성기에서 Transact-SQL SELECT 문을 사용하여 데이터를 반환하거나 데이터베이스에서 레코드를 업데이트, 추가 또는 삭제하는 쿼리를 작성할 수 있습니다.  
  
-   결과를 보고 즉시 편집합니다.  
  
     쿼리를 실행하고 레코드 집합을 표 형태로 사용하여 데이터베이스의 레코드를 스크롤하고 편집할 수 있습니다.  
  
 쿼리 작성기의 시각적 기능은 SELECT 문 작성으로 제한되지만 텍스트 창에 DELETE 및 UPDATE 문과 같은 다른 유형의 문을 위한 SQL을 입력할 수 있습니다. 이때 입력한 SQL 문을 반영하도록 그래픽 창이 자동으로 업데이트됩니다.  
  
 태스크 또는 데이터 흐름 구성 요소 대화 상자나 속성 창에 쿼리를 입력하여 직접 입력을 제공할 수 있습니다.  
  
 자세한 내용은 [Query Builder](http://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)을 참조하세요.  
  
## <a name="sql-in-files"></a>파일 내의 SQL  
 SQL 실행 태스크의 SQL 문을 별도의 파일에 보관할 수 있습니다. 예를 들어 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 작성기와 같은 도구를 사용하여 쿼리를 작성하고 파일로 저장한 다음 패키지를 실행할 때 파일에서 쿼리를 읽을 수 있습니다. 이 파일에는 실행할 SQL 문과 주석만 포함될 수 있습니다. 파일에 저장된 SQL 문을 사용하려면 파일 이름 및 위치를 지정하는 파일 연결을 제공해야 합니다. 자세한 내용은 [File Connection Manager](../integration-services/connection-manager/file-connection-manager.md)을 참조하세요.  
  
## <a name="sql-in-variables"></a>변수 내의 SQL  
 SQL 실행 태스크의 SQL 문 원본이 변수인 경우 쿼리를 포함하는 변수의 이름을 지정하십시오. 쿼리 텍스트는 변수의 Value 속성에 포함됩니다. 변수의 ValueType 속성을 문자열 데이터 형식으로 설정한 다음 Value 속성에 SQL 문을 입력하거나 복사합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  

## <a name="query-builder-dialog-box"></a>쿼리 작성기 대화 상자
**쿼리 작성기** 대화 상자를 사용하여 SQL 실행 태스크, OLE DB 원본 및 대상, 조회 변환에서 사용할 쿼리를 만들 수 있습니다.  
  
 쿼리 작성기를 사용하여 다음 태스크를 수행할 수 있습니다.  
  
-   **쿼리의 그래픽 표시 또는 SQL 명령 작업** 쿼리 작성기에는 쿼리를 그래픽으로 표시하는 창과 쿼리의 SQL 텍스트를 표시하는 텍스트 창이 있습니다. 그래픽 창이나 텍스트 창에서 작업할 수 있습니다. 쿼리 작성기는 항상 최신 상태를 유지하도록 뷰를 동기화합니다.  
  
-   **관련 테이블 조인** 둘 이상의 테이블을 쿼리에 추가하면 쿼리 작성기는 테이블이 관련되는 방법과 적절한 조인 명령을 생성하는 방법을 자동으로 결정합니다.  
  
-   **데이터베이스 쿼리 또는 업데이트** 쿼리 작성기에서 Transact-SQL SELECT 문을 사용하여 데이터를 반환하고 데이터베이스에서 레코드를 업데이트, 추가 또는 삭제하는 쿼리를 만들 수 있습니다.  
  
-   **즉시 결과를 보고 편집** 쿼리를 실행하고 레코드 집합을 표 형태로 처리하여 데이터베이스의 레코드를 스크롤하고 편집할 수 있습니다.  
  
 **쿼리 작성기** 대화 상자의 그래픽 도구를 사용하면 끌어서 놓기 작업을 통해 쿼리를 만들 수 있습니다. 기본적으로 쿼리 작성기 대화 상자에서 SELECT 쿼리를 생성하지만 사용자가 INSERT, UPDATE 또는 DELETE 쿼리를 작성할 수도 있습니다. 모든 유형의 SQL 문은 **쿼리 작성기** 대화 상자에서 구문을 분석하고 실행할 수 있습니다. 패키지의 SQL 문에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 쿼리](../integration-services/integration-services-ssis-queries.md)를 참조하세요.  
  
 Transact-SQL 언어와 해당 구문에 대한 자세한 내용은 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](../t-sql/transact-sql-reference-database-engine.md)를 참조하세요.  
  
 쿼리에 변수를 사용하여 입력 매개 변수에 값을 제공하고 출력 매개 변수의 값을 캡처하며 반환 코드를 저장할 수도 있습니다. 패키지에서 사용하는 쿼리에서 변수를 사용하는 방법에 대한 자세한 내용은 [SQL 실행 태스크](../integration-services/control-flow/execute-sql-task.md), [OLE DB 원본](../integration-services/data-flow/ole-db-source.md) 및 [Integration Services&#40;SSIS&#41; 쿼리](../integration-services/integration-services-ssis-queries.md)를 참조하세요. SQL 실행 태스크에서 변수를 사용하는 방법에 대한 자세한 내용은 [SQL 실행 태스크의 매개 변수 및 반환 코드](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663) 및 [SQL 실행 태스크의 결과 집합](http://msdn.microsoft.com/library/62605b63-d43b-49e8-a863-e154011e6109)을 참조하세요.  
  
 조회 및 유사 항목 조회 변환에서도 매개 변수와 반환 코드에 변수를 사용할 수 있습니다. OLE DB 원본에 대한 정보는 이러한 두 변환에도 적용됩니다.  
  
### <a name="options"></a>변수  
 **도구 모음**  
 도구 모음을 사용하여 데이터 집합을 관리하고, 표시할 창을 선택하고, 쿼리 함수를 제어할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**다이어그램 창 표시/숨기기**|**다이어그램** 창을 표시하거나 숨깁니다.|  
|**표 형태 창 표시/숨기기**|**표 형태** 창을 표시하거나 숨깁니다.|  
|**SQL 창 표시/숨기기**|**SQL** 창을 표시하거나 숨깁니다.|  
|**결과 창 표시/숨기기**|**결과** 창을 표시하거나 숨깁니다.|  
|**실행**|쿼리를 실행합니다. 결과는 결과 창에 표시됩니다.|  
|**SQL 검증**|SQL 문이 유효한지 여부를 확인합니다.|  
|**오름차순 정렬**|표 형태 창에서 선택한 열의 출력 행을 오름차순으로 정렬합니다.|  
|**내림차순 정렬**|표 형태 창에서 선택한 열의 출력 행을 내림차순으로 정렬합니다.|  
|**필터 제거**|표 형태 창에서 열 이름을 선택한 다음 **필터 제거** 를 클릭하여 해당 열에 대한 정렬 조건을 제거합니다.|  
|**Group By 사용**|쿼리에 GROUP BY 기능을 추가합니다.|  
|**테이블 추가**|쿼리에 새 테이블을 추가합니다.|  
  
 **쿼리 정의**  
 쿼리 정의에서는 쿼리를 정의 및 테스트할 수 있는 도구 모음 및 창을 사용할 수 있습니다.  
  
|창|설명|  
|----------|-----------------|  
|**다이어그램** 창|쿼리를 다이어그램에 표시합니다. 다이어그램은 쿼리에 포함된 테이블과 이러한 테이블의 조인 방법을 보여 줍니다. 쿼리 출력에 열을 추가하거나 제거하려면 테이블에서 해당 열의 옆에 있는 확인란을 선택하거나 선택을 취소합니다.<br /><br /> 쿼리에 테이블을 추가하면 쿼리 작성기에서 테이블의 키에 따라 테이블을 기반으로 테이블 간의 조인을 만듭니다. 조인을 추가하려면 한 테이블의 필드를 다른 테이블의 필드로 끌어 놓습니다. 조인을 관리하려면 해당 조인을 마우스 오른쪽 단추로 클릭한 다음 메뉴 옵션을 선택합니다.<br /><br /> **다이어그램** 창을 마우스 오른쪽 단추로 클릭하여 테이블을 추가 또는 제거하고, 모든 테이블을 선택하고, 창을 표시하거나 숨길 수 있습니다.|  
|**표 형태** 창|쿼리를 표에 표시합니다. 이 창을 사용하여 쿼리에서 열을 추가 및 제거하고 각 열의 설정을 변경할 수 있습니다.|  
|**SQL** |쿼리를 SQL 텍스트로 표시합니다. **다이어그램** 창 및 **표 형태** 창에서 변경한 내용은 이 창에 나타나고 여기에서 변경한 내용은 **다이어그램** 창 및 **표 형태** 창에 나타납니다.|  
|**결과** 창|도구 모음에서 **실행** 을 클릭하면 쿼리 결과가 표시됩니다.| 

  
