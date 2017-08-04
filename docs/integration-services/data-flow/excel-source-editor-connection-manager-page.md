---
title: "Excel 원본 편집기 (연결 관리자 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsourceadapter.connection.f1
helpviewer_keywords:
- Excel Source Editor
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1f01be71a5093945a49c43a3a2aec334db7584b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="excel-source-editor-connection-manager-page"></a>Excel 원본 편집기(연결 관리자 페이지)
  **Excel 원본 편집기** 대화 상자의 **연결 관리자** 노드를 사용하여 원본으로 사용할 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 통합 문서를 선택할 수 있습니다. Excel 원본에서는 워크시트 또는 기존 통합 문서의 명명된 범위에서 데이터를 읽습니다.  
  
> [!NOTE]  
>  Excel 원본의 **CommandTimeout** 속성은 **Excel 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이 속성에 대한 자세한 내용은 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)의 Excel 원본 섹션을 참조하십시오.  
  
 Excel 원본에 대한 자세한 내용은 [Excel Source](../../integration-services/data-flow/excel-source.md)을 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **OLE DB 연결 관리자**  
 목록에서 기존 Excel 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **Excel 연결 관리자** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|테이블 또는 뷰|Excel 파일의 워크시트나 명명된 범위에서 데이터를 가져옵니다.|  
|테이블 이름 또는 뷰 이름 변수|변수에 워크시트 또는 범위 이름을 지정합니다.<br /><br /> **관련 정보:** [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 명령|SQL 쿼리를 사용하여 Excel 파일에서 데이터를 가져옵니다. 쿼리 구문에 대한 자세한 내용은 [Excel Source](../../integration-services/data-flow/excel-source.md)을 참조하십시오.|  
|변수를 사용한 SQL 명령|변수에 SQL 쿼리 텍스트를 지정합니다.|  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **Excel 시트의 이름**  
 Excel 통합 문서에서 사용할 수 있는 워크시트 또는 명명된 범위 목록에서 이름을 선택합니다.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 워크시트 또는 명명된 범위 이름이 포함된 변수를 선택합니다.  
  
### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
 **매개 변수**  
 쿼리 텍스트에 ?를 매개 변수 자리 표시자로 사용하여 매개 변수가 있는 쿼리를 입력한 경우 **쿼리 매개 변수 설정** 대화 상자를 사용하여 쿼리 입력 매개 변수를 패키지 변수에 매핑합니다.  
  
 **Build query**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
 **쿼리 구문 분석**  
 쿼리 텍스트의 구문을 확인합니다.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>데이터 액세스 모드 = 변수를 사용한 SQL 명령  
 **변수 이름**  
 SQL 쿼리 텍스트가 포함된 변수를 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [Excel 원본 편집기 &#40; 열 페이지 &#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Excel 원본 편집기 &#40; 오류 출력 페이지 &#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Excel 통해 루프 파일 및 Foreach 루프 컨테이너를 사용 하 여 테이블](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
