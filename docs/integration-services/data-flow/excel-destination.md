---
title: Excel 대상 | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 418d3c214f667807df997902f97bfa271c8c4742
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292815"
---
# <a name="excel-destination"></a>Excel 대상

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Excel 대상은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서의 워크시트 또는 범위로 데이터를 로드합니다.  

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.
  
## <a name="access-modes"></a>액세스 모드  
 Excel 대상은 데이터 로드를 위한 3가지 데이터 액세스 모델을 제공합니다.  
  
-   테이블 또는 뷰  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과 쿼리는 매개 변수가 있는 쿼리일 수 있습니다.  
  
## <a name="configure-the-excel-destination"></a>Excel 대상 구성  
 Excel 대상은 Excel 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 통합 문서 파일을 지정합니다. 자세한 내용은 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)를 참조하세요.  
  
 Excel 대상에는 하나의 일반 입력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 모든 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 사용자 지정 속성](../../integration-services/data-flow/excel-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Excel 대상 편집기(연결 관리자 페이지)
  **Excel 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 데이터 원본 정보를 지정하고 그 결과를 미리 볼 수 있습니다. Excel 대상은 데이터를 워크시트 또는 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] Excel 통합 문서의 명명된 범위로 로드합니다.  
  
> [!NOTE]  
>  Excel 대상의 **CommandTimeout** 속성은 **Excel 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 또한 특정 빠른 로드 옵션은 **고급 편집기**에서만 사용할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)의 Excel 대상 섹션을 참조하십시오.  
  
### <a name="static-options"></a>정적 옵션  
 **Excel 연결 관리자**  
 목록에서 기존 Excel 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **Excel 연결 관리자** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|테이블 또는 뷰|데이터를 워크시트 또는 Excel 데이터 원본의 명명된 범위로 로드합니다.|  
|테이블 이름 또는 뷰 이름 변수|변수에 워크시트 또는 범위 이름을 지정합니다.<br /><br /> **관련 정보**: [패키지에서 변수 사용](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 명령|SQL 쿼리를 사용하여 Excel 대상으로 데이터를 로드합니다.|  
  
 **Excel 시트의 이름**  
 드롭다운 목록에서 Excel 대상을 선택합니다. 목록이 비어 있는 경우 **새로 만들기**를 클릭합니다.  
  
 **새로 만들기**  
 **새로 만들기** 를 클릭하여 **테이블 만들기** 대화 상자를 시작합니다. **확인**을 클릭하면 대화 상자에서 **Excel 연결 관리자** 가 가리키는 Excel 파일이 만들어집니다.  
  
 **기존 데이터 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
### <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
#### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **Excel 시트의 이름**  
 데이터 원본에서 사용할 수 있는 워크시트 또는 명명된 범위 목록에서 이름을 선택합니다.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 워크시트 또는 명명된 범위 이름이 포함된 변수를 선택합니다.  
  
#### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
 **쿼리 작성**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
 **쿼리 구문 분석**  
 쿼리 텍스트의 구문을 확인합니다.  
  
## <a name="excel-destination-editor-mappings-page"></a>Excel 대상 편집기(매핑 페이지)
  **Excel 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 입력 열을 대상 열에 매핑합니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 대상 열을 입력 열에 매핑합니다.  
  
 **입력 열**  
 위 테이블에서 선택한 입력 열을 표시합니다. **사용 가능한 입력 열**의 목록을 사용하여 매핑을 변경할 수 있습니다.  
  
 **대상 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="excel-destination-editor-error-output-page"></a>Excel 대상 편집기(오류 출력 페이지)
  **Excel 대상 편집기** 대화 상자의 **고급** 페이지를 사용하여 오류 처리 옵션을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **입력 또는 출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **Excel 원본 편집기** 대화 상자의 **연결 관리자**노드에서 선택한 외부(원본) 열을 표시합니다.  
  
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
 [SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)  
 [Excel 원본](../../integration-services/data-flow/excel-source.md)   
[Excel 연결 관리자](../connection-manager/excel-connection-manager.md)
