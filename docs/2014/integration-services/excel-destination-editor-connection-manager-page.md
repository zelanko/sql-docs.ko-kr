---
title: Excel 대상 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3538e768fafbf310850fecf9899e70409b7b2758
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157823"
---
# <a name="excel-destination-editor-connection-manager-page"></a>Excel 대상 편집기(연결 관리자 페이지)
  **Excel 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 데이터 원본 정보를 지정하고 그 결과를 미리 볼 수 있습니다. Excel 대상은 데이터를 워크시트 또는 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] Excel 통합 문서의 명명된 범위로 로드합니다.  
  
> [!NOTE]  
>  `CommandTimeout` Excel 대상의 속성을 사용할 수 없습니다는 **Excel 대상 편집기**를 사용 하 여 설정할 수 있습니다 합니다 **고급 편집기**합니다. 또한 특정 빠른 로드 옵션은 **고급 편집기**에서만 사용할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Excel Custom Properties](data-flow/excel-custom-properties.md)의 Excel 대상 섹션을 참조하십시오.  
  
 Excel 대상에 대한 자세한 내용은 [Excel Destination](data-flow/excel-destination.md)을 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **Excel 연결 관리자**  
 목록에서 기존 Excel 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **Excel 연결 관리자** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|테이블 또는 뷰|데이터를 워크시트 또는 Excel 데이터 원본의 명명된 범위로 로드합니다.|  
|테이블 이름 또는 뷰 이름 변수|변수에 워크시트 또는 범위 이름을 지정합니다.<br /><br /> **관련 정보**: [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)|  
|SQL 명령|SQL 쿼리를 사용하여 Excel 대상으로 데이터를 로드합니다.|  
  
 **Excel 시트의 이름**  
 드롭다운 목록에서 Excel 대상을 선택합니다. 목록이 비어 있는 경우 **새로 만들기**를 클릭합니다.  
  
 **새로 만들기**  
 **새로 만들기** 를 클릭하여 **테이블 만들기** 대화 상자를 시작합니다. **확인**을 클릭하면 대화 상자에서 **Excel 연결 관리자** 가 가리키는 Excel 파일이 만들어집니다.  
  
 **기존 데이터 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
> [!WARNING]  
>  선택한 **Excel 연결 관리자** 가 존재하지 않는 Excel 파일을 가리키는 경우 이 단추를 클릭하면 오류 메시지가 표시됩니다.  
  
## <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **Excel 시트의 이름**  
 데이터 원본에서 사용할 수 있는 워크시트 또는 명명된 범위 목록에서 이름을 선택합니다.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 워크시트 또는 명명된 범위 이름이 포함된 변수를 선택합니다.  
  
### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
 **쿼리 작성**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
 **쿼리 구문 분석**  
 쿼리 텍스트의 구문을 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Excel 대상 편집기 &#40;매핑 페이지&#41;](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [Excel 대상 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](control-flow/foreach-loop-container.md)  
  
  
