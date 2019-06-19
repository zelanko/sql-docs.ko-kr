---
title: OLE DB 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f666a224c2e41fb50a1a62748e7d8f1666d0beb9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726640"
---
# <a name="ole-db-source"></a>OLE DB 원본

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 원본은 데이터베이스 테이블, 뷰 또는 SQL 명령을 사용하여 다양한 OLE DB 호환 관계형 데이터베이스에서 데이터를 추출합니다. 예를 들어 OLE DB 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블에서 데이터를 추출할 수 있습니다.  
  
> [!NOTE]  
>  데이터 원본이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007인 경우 이 데이터 원본에는 이전 버전의 Excel과 다른 연결 관리자가 필요합니다. 자세한 내용은 [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)을 참조하세요.  
  
 OLE DB 원본은 데이터 추출을 위한 4가지 데이터 액세스 모델을 제공합니다.  
  
-   테이블 또는 뷰  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과 쿼리는 매개 변수가 있는 쿼리일 수 있습니다.  
  
-   변수에 저장된 SQL 문의 결과  
  
> [!NOTE]  
>  SQL 문을 사용하여 임시 테이블의 결과를 반환하는 저장 프로시저를 호출하는 경우 WITH RESULT SETS 옵션을 사용하여 결과 집합의 메타데이터를 정의합니다.  
  
 매개 변수가 있는 쿼리를 사용하는 경우 변수를 매개 변수에 매핑하여 SQL 문의 개별 매개 변수에 값을 지정할 수 있습니다.  
  
 이 원본은 OLE DB 연결 관리자를 사용하여 데이터 원본에 연결하며 이 연결 관리자는 사용할 OLE DB Provider를 지정합니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 또한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 OLE DB 연결 관리자를 만들 수 있는 데이터 원본 개체를 제공하여 OLE DB 원본에서 데이터 원본과 데이터 원본 뷰를 사용할 수 있게 합니다.  
  
 OLE DB Provider에 따라 OLE DB 원본에는 다음 몇 가지 제한이 적용됩니다.  
  
-   Oracle용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider는 Oracle 데이터 형식 BLOB, CLOB, NCLOB, BFILE 또는 UROWID를 지원하지 않으며 OLE DB 원본은 이러한 데이터 형식의 열이 포함된 테이블에서 데이터를 추출할 수 없습니다.  
  
-   IBM OLE DB DB2 공급자와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 공급자는 저장 프로시저를 호출하는 SQL 명령의 사용을 지원하지 않습니다. 이러한 종류의 명령을 사용하면 OLE DB 원본에서 열 메타데이터를 만들 수 없으므로 데이터 흐름에서 OLE DB 원본을 따르는 데이터 흐름 구성 요소가 열 데이터를 사용할 수 없으며 데이터 흐름의 실행이 실패합니다.  
  
 OLE DB 원본에는 하나의 일반 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="using-parameterized-sql-statements"></a>매개 변수가 있는 SQL 문 사용  
 OLE DB 원본은 SQL 문을 사용하여 데이터를 추출할 수 있습니다. 이 문은 SELECT 또는 EXEC 문일 수 있습니다.  
  
 OLE DB 원본은 OLE DB 연결 관리자를 사용하여 데이터를 추출할 데이터 원본에 연결합니다. OLE DB 연결 관리자가 사용하는 공급자 및 연결하는 RDBMS(관계형 데이터베이스 관리 시스템)에 따라 매개 변수 명명 및 나열 작업에 적용되는 규칙이 달라집니다. RDBMS에서 매개 변수 이름을 반환하는 경우 매개 변수 이름을 사용하여 매개 변수 목록의 매개 변수를 SQL 문의 매개 변수에 매핑할 수 있습니다. 그렇지 않으면 매개 변수가 매개 변수 목록에서의 서수 위치별로 SQL 문의 매개 변수에 매핑됩니다. 지원되는 매개 변수 이름 유형은 공급자에 따라 달라집니다. 예를 들어 일부 공급자의 경우 변수 또는 열 이름을 사용해야 하지만 0 또는 Param0과 같은 심볼 이름을 사용해야 하는 공급자도 있습니다. SQL 문에서 사용할 매개 변수 이름에 대한 자세한 내용은 공급자별 설명서를 참조하십시오.  
  
 OLE DB 연결 관리자를 사용하는 경우에는 OLE DB 원본이 OLE DB Provider를 통해 매개 변수 정보를 파생할 수 없으므로 매개 변수가 있는 하위 쿼리를 사용할 수 없습니다. 하지만 식을 사용하여 매개 변수 값을 쿼리 문자열에 연결하고 원본의 SqlCommand 속성을 설정할 수 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **OLE DB 원본 편집기** 대화 상자를 사용하여 OLE DB 원본을 구성하고 **쿼리 매개 변수 설정** 대화 상자에서 매개 변수를 변수에 매핑합니다.  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>서수 위치를 사용하여 매개 변수 지정  
 매개 변수 이름이 반환되지 않는 경우 매개 변수가 **쿼리 매개 변수 설정** 대화 상자의 **매개 변수** 목록에 나열되는 순서에 따라 런타임에 매핑되는 대상 매개 변수 표식이 결정됩니다. 목록의 첫 번째 매개 변수는 SQL 문의 첫 번째 ?에 매핑되고 두 번째 매개 변수는 두 번째 ?에 매핑되는 식입니다.  
  
 다음 SQL 문은 **데이터베이스의** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 테이블에서 행을 선택합니다. **매핑** 목록의 첫 번째 매개 변수는 **Color** 열의 첫 번째 매개 변수에 매핑되고 두 번째 매개 변수는 **Size** 열에 매핑됩니다.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 매개 변수 이름은 영향을 받지 않습니다. 예를 들어 매개 변수의 이름이 적용될 열의 이름과 같지만 해당 매개 변수가 **매개 변수** 목록의 올바른 서수 위치에 배치되어 있지 않은 경우 런타임에 매개 변수 매핑이 수행될 때는 매개 변수의 이름이 아니라 매개 변수의 서수 위치가 사용됩니다.  
  
 EXEC 명령을 사용하려면 일반적으로 프로시저의 매개 변수 값을 매개 변수 이름으로 제공하는 변수의 이름을 사용해야 합니다.  
  
### <a name="specifying-parameters-by-using-names"></a>이름을 사용하여 매개 변수 지정  
 RDBMS에서 실제 매개 변수 이름을 반환하는 경우 SELECT 및 EXEC 문에서 사용하는 매개 변수가 이름별로 매핑됩니다. 매개 변수 이름은 SELECT 문이나 EXEC 문으로 실행되는 저장 프로시저에 필요한 이름과 일치해야 합니다.  
  
 다음 SQL 문은 **데이터베이스에서 사용할 수 있는** uspGetWhereUsedProductID [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 저장 프로시저를 실행합니다.  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 이 저장 프로시저에는 매개 변수 값을 제공할 변수 `@StartProductID` 및 `@CheckDate`가 필요합니다. **매핑** 목록에 매개 변수가 나타나는 순서는 상관없으며 \@ 기호를 포함한 매개 변수 이름이 저장 프로시저의 변수 이름과 일치하기만 하면 됩니다.  
  
### <a name="mapping-parameters-to-variables"></a>변수에 매개 변수 매핑  
 매개 변수는 런타임에 매개 변수 값을 제공하는 변수에 매핑됩니다. 변수는 일반적으로 사용자 정의 변수이지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 시스템 변수를 사용할 수도 있습니다. 사용자 정의 변수를 사용하는 경우에는 매핑된 매개 변수가 참조하는 열의 데이터 형식과 호환되는 형식으로 데이터 형식을 설정합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)을 참조하세요.  
  
## <a name="troubleshooting-the-ole-db-source"></a>OLE DB 원본 문제 해결  
 OLE DB 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하면 OLE DB 원본이 외부 데이터 원본에서 데이터를 로드할 때 발생하는 문제를 해결할 수 있습니다. OLE DB 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-ole-db-source"></a>OLE DB 원본 구성  
 프로그래밍 방식을 통해 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB 사용자 지정 속성](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [OLE DB 원본을 사용하여 데이터 추출](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>관련 내용  
 social.technet.microsoft.com의 Wiki 문서 - [Oracle 커넥터가 있는 SSIS](https://go.microsoft.com/fwlink/?LinkId=220670)  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>OLE DB 원본 편집기(연결 관리자 페이지)
  **OLE DB 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 원본의 OLE DB 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007을 사용하는 데이터 원본에서 데이터를 로드하려면 OLE DB 원본을 사용하십시오. Excel 원본을 사용하여 Excel 2007 데이터 원본에서 데이터를 로드할 수 없습니다. 자세한 내용은 [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)을(를) 참조하세요.  
>   
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 이전 버전을 사용하는 데이터 원본에서 데이터를 로드하려면 Excel 원본을 사용하십시오. 자세한 내용은 [Excel 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md)를 참조하세요.  
  
> [!NOTE]  
>  OLE DB 원본의 **CommandTimeout** 속성은 **OLE DB 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이 속성에 대한 자세한 내용은 [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)의 Excel 원본 섹션을 참조하십시오.  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>OLE DB 원본 편집기 열기(연결 관리자 페이지)  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 OLE DB 원본을 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 추가합니다.  
  
2.  원본 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **연결 관리자**를 클릭합니다.  
  
### <a name="static-options"></a>정적 옵션  
 **캐시 없음**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|테이블 또는 뷰|OLE DB 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다.|  
|테이블 이름 또는 뷰 이름 변수|변수에 테이블 또는 뷰 이름을 지정합니다.<br /><br /> **관련 정보:** [패키지에서 변수 사용](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 명령|SQL 쿼리를 사용하여 OLE DB 데이터 원본에서 데이터를 검색합니다.|  
|변수를 사용한 SQL 명령|변수에 SQL 쿼리 텍스트를 지정합니다.|  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. **미리 보기** 에는 최대 200개의 행이 표시될 수 있습니다.  
  
> [!NOTE]  
>  데이터를 미리 보면 CLR 사용자 정의 형식의 열에 데이터가 포함되지 않습니다. 대신 \<값이 너무 커서 표시할 수 없습니다> 또는 System.Byte[] 값이 표시됩니다. 전자는 SQL OLE DB 공급자를 사용하여 데이터 원본에 액세스하는 경우 표시되고 후자는 &lt; [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자를 사용하는 경우 표시됩니다.  
  
### <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
#### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **테이블 또는 뷰 이름**  
 데이터 원본의 사용 가능한 테이블 또는 뷰 목록에서 테이블 또는 뷰 이름을 선택합니다.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 테이블 또는 뷰 이름이 포함된 변수를 선택합니다.  
  
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
  
## <a name="ole-db-source-editor-columns-page"></a>OLE DB 원본 편집기(열 페이지)
  **OLE DB 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록을 표시합니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다.  
  
 **외부 열**  
 이 원본의 데이터를 사용하는 구성 요소를 구성할 때 표시되는 순서로 외부(원본) 열을 표시합니다. 이 순서는 먼저 테이블에서 선택된 열을 지운 다음 목록에서 다른 순서로 외부 열을 선택하여 변경할 수 있습니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 제공한 이름은 SSIS 디자이너에 표시됩니다.  
  
## <a name="ole-db-source-editor-error-output-page"></a>OLE DB 원본 편집기(오류 출력 페이지)
  **OLE DB 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택하고 오류 출력 열에 속성을 설정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **입/출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **OLE DB 원본 편집기** 대화 상자의 **연결 관리자**페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
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
 [OLE DB 대상](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
