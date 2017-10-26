---
title: "Excel 대상 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 69a0a8b907fcb45cf6ecd0576fb6fba04775d237
ms.contentlocale: ko-kr
ms.lasthandoff: 08/17/2017

---
# <a name="excel-destination"></a>Excel 대상
  Excel 대상은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서의 워크시트 또는 범위로 데이터를 로드합니다.  
  
## <a name="access-modes"></a>액세스 모드  
 Excel 대상은 데이터 로드를 위한 3가지 데이터 액세스 모델을 제공합니다.  
  
-   테이블 또는 뷰  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과 쿼리는 매개 변수가 있는 쿼리일 수 있습니다.  
  
> [!IMPORTANT]  
>  Excel에서 워크시트나 범위는 테이블 또는 뷰에 해당합니다. Excel 원본 및 대상 편집기의 사용 가능한 테이블 목록은 기존 워크시트(Sheet1$와 같이 워크시트 이름에 $ 기호가 붙음)와 명명된 범위(MyRange와 같이 $ 기호가 없음)만 표시합니다.  
  
## <a name="usage-considerations"></a>사용 시 고려 사항  
 Excel 연결 관리자는 Jet 4.0용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider와 공급자에서 지원하는 Excel ISAM(Indexed Sequential Access Method) 드라이버를 사용하여 Excel 데이터 원본에 연결하고 데이터를 읽고 씁니다.  
  
 이 공급자와 드라이버의 동작에 대해 다루는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 문서가 많이 있습니다. 이러한 문서가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 이전 기능인 데이터 변환 서비스와 반드시 관련된 것은 아니지만 예기치 않은 결과를 발생시킬 수 있는 특정 동작에 대해 살펴보는 것이 좋습니다. Excel 드라이버의 사용 방법과 동작에 대한 일반 정보는 [Visual Basic 또는 VBA에서 Excel 데이터에 ADO를 사용하는 방법](http://support.microsoft.com/kb/257819)을 참조하십시오.  
  
 Excel 드라이버에 포함된 Jet 공급자의 다음 동작은 데이터를 Excel 대상에 저장할 때 예기치 않은 결과를 초래할 수 있습니다.  
  
-   **텍스트 데이터 저장**. Excel 드라이버가 텍스트 데이터 값을 Excel 대상에 저장하면 드라이버는 각 셀에서 작은따옴표(')가 있는 텍스트 앞에 오므로 저장된 값이 텍스트 값으로 해석됩니다. 저장된 데이터를 읽거나 처리하는 다른 응용 프로그램을 갖고 있거나 개발한 경우 각 텍스트 값을 처리하는 작은따옴표에 대한 특별한 처리 방식을 포함해야 합니다.  
  
     작은따옴표가 포함되지 않도록 하는 방법에 대한 내용은 msdn.com의 블로그 게시물 중 [SSIS 패키지에서 Excel 대상 데이터 흐름 구성 요소를 사용하여 Excel로 데이터를 변환할 때 모든 문자열에 추가되는 작은따옴표](http://go.microsoft.com/fwlink/?LinkId=400876)(영문)를 참조하세요.  
  
-   **메모(ntext) 데이터 저장**. 255자보다 긴 문자열을 Excel 열에 저장하려면 드라이버에서 대상 열의 데이터 형식을 **string** 이 아닌 **memo**로 인식해야 합니다. 대상 테이블에 이미 데이터 행이 포함된 경우 드라이버에서 샘플링하는 처음 몇 개 행의 메모 열에 값이 255자보다 긴 인스턴스가 하나 이상 들어 있어야 합니다. 패키지 디자인 타임 또는 런타임에 대상 테이블을 만드는 경우 CREATE TABLE 문은 메모 열의 데이터 형식으로 LONGTEXT(또는 해당 동의어 중 하나)를 사용해야 합니다.  
  
-   **데이터 형식**. Excel 드라이버는 제한된 데이터 형식 집합만 인식합니다. 예를 들어 모든 숫자 열은 double(DT_R8)로 해석되고 모든 문자열 열(메모 열 제외)은 255자 유니코드 문자열(DT_WSTR)로 해석됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 Excel 데이터 형식을 다음과 같이 매핑합니다.  
  
    -   숫자    배정밀도 부동 소수점 수(DT_R8)  
  
    -   통화    currency(DT_CY)  
  
    -   부울    Boolean(DT_BOOL)  
  
    -   날짜/시간     **datetime** (DT_DATE)  
  
    -   문자열    길이가 255인 유니코드 문자열(DT_WSTR)  
  
    -   메모    유니코드 텍스트 스트림(DT_NTEXT)  
  
-   **데이터 형식 및 길이 변환**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 데이터 형식을 암시적으로 변환하지 않습니다. 따라서 파생 열 변환이나 데이터 변환을 사용하여 Excel 데이터를 비 Excel 대상으로 로드하기 전에 명시적으로 변환하거나 비 Excel 데이터를 Excel 대상으로 로드하기 전에 변환해야 할 수 있습니다. 이 경우 필요한 변환을 구성해 주는 가져오기 및 내보내기 마법사를 사용하여 초기 패키지를 만들면 유용할 수 있습니다. 필요할 수 있는 일부 변환 예는 다음과 같습니다.  
  
    -   유니코드 Excel 문자열 열과 특정 코드 페이지가 있는 비유니코드 문자열 열 간 변환  
  
    -   255자 Excel 문자열 열과 길이가 다른 문자열 열 간 변환  
  
    -   배정밀도 Excel 숫자 열과 다른 유형의 숫자 열 간 변환  
  
## <a name="configuration-of-the-excel-destination"></a>Excel 집합 대상 구성  
 Excel 대상은 Excel 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 통합 문서 파일을 지정합니다. 자세한 내용은 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)를 참조하세요.  
  
 Excel 대상에는 하나의 일반 입력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 모든 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 사용자 지정 속성](../../integration-services/data-flow/excel-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   dougbert.com의 블로그 항목 - [Integration Services의 Excel, 3부 중 1부: 연결 및 구성 요소](http://go.microsoft.com/fwlink/?LinkId=217674)  
  
-   dougbert.com의 블로그 항목 - [Integration Services의 Excel, 3부 중 2부: 표 및 데이터 형식](http://go.microsoft.com/fwlink/?LinkId=217675)  
  
-   dougbert.com의 블로그 항목 - [Integration Services의 Excel, 3부 중 3부: 문제 및 대안](http://go.microsoft.com/fwlink/?LinkId=217676)  
  
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
  
|옵션|Description|  
|------------|-----------------|  
|테이블 또는 뷰|데이터를 워크시트 또는 Excel 데이터 원본의 명명된 범위로 로드합니다.|  
|테이블 이름 또는 뷰 이름 변수|변수에 워크시트 또는 범위 이름을 지정합니다.<br /><br /> **관련 정보**: [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 명령|SQL 쿼리를 사용하여 Excel 대상으로 데이터를 로드합니다.|  
  
 **Excel 시트의 이름**  
 드롭다운 목록에서 Excel 대상을 선택합니다. 목록이 비어 있는 경우 **새로 만들기**를 클릭합니다.  
  
 **새로 만들기**  
 **새로 만들기** 를 클릭하여 **테이블 만들기** 대화 상자를 시작합니다. **확인**을 클릭하면 대화 상자에서 **Excel 연결 관리자** 가 가리키는 Excel 파일이 만들어집니다.  
  
 **기존 데이터 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
> [!WARNING]  
>  선택한 **Excel 연결 관리자** 가 존재하지 않는 Excel 파일을 가리키는 경우 이 단추를 클릭하면 오류 메시지가 표시됩니다.  
  
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
  
 **Description**  
 오류에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Excel 원본](../../integration-services/data-flow/excel-source.md)   
 [Integration Services &#40; Ssis&#41; 변수](../../integration-services/integration-services-ssis-variables.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)   
 [스크립트 태스크와 Excel 파일 작업](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  

