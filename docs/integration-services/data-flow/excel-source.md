---
title: "Excel 원본 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: e8b5878513b74faa8df5e7766762f2f7287ec7af
ms.contentlocale: ko-kr
ms.lasthandoff: 08/17/2017

---
# <a name="excel-source"></a>Excel 원본
  Excel 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서의 워크시트 또는 범위에서 데이터를 추출합니다.  
  
 Excel 원본은 데이터 추출을 위한 4가지 데이터 액세스 모델을 제공합니다.  
  
-   테이블 또는 뷰  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과 쿼리는 매개 변수가 있는 쿼리일 수 있습니다.  
  
-   변수에 저장된 SQL 문의 결과  
  
> [!IMPORTANT]  
>  Excel에서 워크시트나 범위는 테이블 또는 뷰에 해당합니다. Excel 원본 및 대상 편집기의 사용 가능한 테이블 목록은 기존 워크시트(Sheet1$와 같이 워크시트 이름에 $ 기호가 붙음)와 명명된 범위(MyRange와 같이 $ 기호가 없음)를 표시합니다. 자세한 내용은 "사용 시 고려 사항" 섹션을 참조하십시오.  
  
 Excel 원본은 Excel 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 통합 문서 파일을 지정합니다. 자세한 내용은 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)를 참조하세요.  
  
 Excel 원본에는 하나의 일반 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="usage-considerations"></a>사용 시 고려 사항  
 Excel 연결 관리자는 Jet 4.0용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider와 공급자에서 지원하는 Excel ISAM(Indexed Sequential Access Method) 드라이버를 사용하여 Excel 데이터 원본에 연결하고 데이터를 읽고 씁니다.  
  
 이 공급자와 드라이버의 동작에 대해 다루는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 문서가 많이 있습니다. 이러한 문서가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 이전 기능인 데이터 변환 서비스와 반드시 관련된 것은 아니지만 예기치 않은 결과를 발생시킬 수 있는 특정 동작에 대해 살펴보는 것이 좋습니다. Excel 드라이버의 사용 방법과 동작에 대한 일반 정보는 [Visual Basic 또는 VBA에서 Excel 데이터에 ADO를 사용하는 방법](http://support.microsoft.com/kb/257819)을 참조하십시오.  
  
 Excel 드라이버를 사용하는 Jet 공급자의 다음 동작은 Excel 데이터 원본에서 데이터를 읽을 때 예기치 않은 결과를 발생시킬 수 있습니다.  
  
-   **데이터 원본**. Excel 통합 문서의 데이터 원본은 $ 기호가 붙은 워크시트(예: Sheet1$) 또는 명명된 범위(예: MyRange)일 수 있습니다. SQL 문에서 $ 기호로 인한 구문 오류가 없도록 워크시트의 이름을 구분해야 합니다(예: [Sheet1$]). 쿼리 작성기는 자동으로 이러한 구분 기호를 추가합니다. 워크시트 또는 범위를 지정하면 드라이버는 워크시트 또는 범위의 가장 왼쪽에서 비어 있지 않은 첫 번째 셀부터 인접한 블록의 셀을 읽습니다. 따라서 원본 데이터나 제목 또는 머리글 행과 데이터 행 사이에 빈 행이 있을 수 없습니다.  
  
-   **누락된 값**. Excel 드라이버는 지정한 원본에서 특정 개수의 행(기본값: 8행)을 읽어 각 열의 데이터 형식을 추측합니다. 열에 혼합된 데이터 형식, 특히 숫자 데이터와 텍스트 데이터가 혼합되어 있으면 드라이버는 주로 사용된 데이터 형식을 지정하고 다른 형식의 데이터가 포함된 셀에 Null 값을 반환합니다. 사용된 횟수가 같은 경우에는 숫자 유형이 적용됩니다. Excel 워크시트에서 대부분의 셀 서식 옵션은 이러한 데이터 형식 결정에 영향을 주지 않습니다. 가져오기 모드를 지정하여 Excel 드라이버의 이러한 동작을 수정할 수 있습니다. 가져오기 모드를 지정하려면 **속성** 창에서 Excel 연결 관리자의 연결 문자열에 있는 확장 속성 값에 **IMEX=1** 을 추가합니다. 자세한 내용은 [PRB: DAO OpenRecordset를 사용할 때 Excel 값이 NULL로 반환된다](http://support.microsoft.com/kb/194124)를 참조하십시오.  
  
-   **잘린 텍스트**. Excel 열에 텍스트 데이터가 포함되어 있음이 확인되면 드라이버는 샘플링하는 값 중 가장 긴 값을 기준으로 데이터 형식(문자열 또는 메모)을 선택합니다. 샘플링하는 행에서 255자보다 긴 값이 검색되지 않으면 이 드라이버는 해당 열을 메모 열이 아닌 255자 문자열 열로 처리합니다. 따라서 255자보다 긴 값은 잘릴 수 있습니다. 메모 열에서 데이터를 가져올 때 데이터가 잘리지 않도록 하려면 샘플링된 행 중 하나 이상의 행에 있는 메모 열에 255자보다 긴 값을 포함시키거나 드라이버가 샘플링하는 행 수를 늘려 이러한 행을 포함하도록 합니다. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** 레지스트리 키 아래 **TypeGuessRows** 값을 늘려 샘플링된 행 수를 늘릴 수 있습니다. 자세한 내용은 [PRB: Transfer of Data from Jet 4.0 OLEDB Source Fails w/ Error](http://support.microsoft.com/kb/281517)(PRB: Jet 4.0 OLEDB 원본에서 데이터를 전송하면 버퍼 오버플로 오류가 발생하면서 실패)를 참조하세요.  
  
-   **데이터 형식**. Excel 드라이버는 제한된 데이터 형식 집합만 인식합니다. 예를 들어 모든 숫자 열은 double(DT_R8)로 해석되고 모든 문자열 열(메모 열 제외)은 255자 유니코드 문자열(DT_WSTR)로 해석됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 Excel 데이터 형식을 다음과 같이 매핑합니다.  
  
    -   숫자 - 배정밀도 부동 소수점 수(DT_R8)  
  
    -   통화 - currency(DT_CY)  
  
    -   부울 - Boolean(DT_BOOL)  
  
    -   날짜/시간 - **datetime** (DT_DATE)  
  
    -   문자열 - 길이가 255인 유니코드 문자열(DT_WSTR)  
  
    -   메모 - 유니코드 텍스트 스트림(DT_NTEXT)  
  
-   **데이터 형식 및 길이 변환**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 데이터 형식을 암시적으로 변환하지 않습니다. 따라서 파생 열 변환이나 데이터 변환을 사용하여 Excel 데이터를 비 Excel 대상으로 로드하기 전에 명시적으로 변환하거나 비 Excel 데이터를 Excel 대상으로 로드하기 전에 변환해야 할 수 있습니다. 이 경우 필요한 변환을 구성해 주는 가져오기 및 내보내기 마법사를 사용하여 초기 패키지를 만들면 유용할 수 있습니다. 필요할 수 있는 일부 변환 예는 다음과 같습니다.  
  
    -   유니코드 Excel 문자열 열과 특정 코드 페이지가 있는 비유니코드 문자열 열 간 변환  
  
    -   255자 Excel 문자열 열과 길이가 다른 문자열 열 간 변환  
  
    -   배정밀도 Excel 숫자 열과 다른 유형의 숫자 열 간 변환  
  
## <a name="excel-source-configuration"></a>Excel 원본 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 모든 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 사용자 지정 속성](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Excel 파일 그룹을 통한 루핑 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Excel 통해 루프 파일 및 Foreach 루프 컨테이너를 사용 하 여 테이블](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
## <a name="excel-source-editor-connection-manager-page"></a>Excel 원본 편집기(연결 관리자 페이지)
  **Excel 원본 편집기** 대화 상자의 **연결 관리자** 노드를 사용하여 원본으로 사용할 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 통합 문서를 선택할 수 있습니다. Excel 원본에서는 워크시트 또는 기존 통합 문서의 명명된 범위에서 데이터를 읽습니다.  
  
> [!NOTE]  
>  Excel 원본의 **CommandTimeout** 속성은 **Excel 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이 속성에 대한 자세한 내용은 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)의 Excel 원본 섹션을 참조하십시오.  
  
### <a name="static-options"></a>정적 옵션  
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
|SQL 명령|SQL 쿼리를 사용하여 Excel 파일에서 데이터를 가져옵니다. |  
|변수를 사용한 SQL 명령|변수에 SQL 쿼리 텍스트를 지정합니다.|  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
### <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
#### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **Excel 시트의 이름**  
 Excel 통합 문서에서 사용할 수 있는 워크시트 또는 명명된 범위 목록에서 이름을 선택합니다.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 워크시트 또는 명명된 범위 이름이 포함된 변수를 선택합니다.  
  
#### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
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
  
#### <a name="data-access-mode--sql-command-from-variable"></a>데이터 액세스 모드 = 변수를 사용한 SQL 명령  
 **변수 이름**  
 SQL 쿼리 텍스트가 포함된 변수를 선택합니다.  
  
## <a name="excel-source-editor-columns-page"></a>Excel 원본 편집기(열 페이지)
  **Excel 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록을 표시합니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다.  
  
 **외부 열**  
 태스크에서 읽는 순서대로 외부(원본) 열을 표시합니다. 이 순서는 먼저 위에 설명된 테이블에서 선택된 열을 지운 다음 목록에서 다른 순서로 외부 열을 선택하여 변경할 수 있습니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
## <a name="excel-source-editor-error-output-page"></a>Excel 원본 편집기(오류 출력 페이지)
  **Excel 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택하고 오류 출력 열에 속성을 설정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **입력 또는 출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **Excel 원본 편집기** 대화 상자의 **연결 관리자**페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
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
  
## <a name="related-content"></a>관련 내용  
  
-   hrvoje.piasevoli.com의 블로그 항목 - [SSIS의 64비트 Excel에서 데이터 가져오기](http://go.microsoft.com/fwlink/?LinkId=217673)  
  
-   dougbert.com의 블로그 항목 - [Integration Services의 Excel, 3부 중 1부: 연결 및 구성 요소](http://go.microsoft.com/fwlink/?LinkId=217674)  
  
-   dougbert.com의 블로그 항목 - [Integration Services의 Excel, 3부 중 2부: 표 및 데이터 형식](http://go.microsoft.com/fwlink/?LinkId=217675)  
  
-   dougbert.com의 블로그 항목 - [Integration Services의 Excel, 3부 중 3부: 문제 및 대안](http://go.microsoft.com/fwlink/?LinkId=217676)  
  
  

