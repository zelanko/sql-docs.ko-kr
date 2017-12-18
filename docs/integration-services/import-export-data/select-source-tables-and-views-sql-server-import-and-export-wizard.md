---
title: "원본 테이블 및 뷰 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: "96"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 407e1b75ca60bb8a36040883c472dce8e059188e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>원본 테이블 및 뷰 선택(SQL Server 가져오기 및 내보내기 마법사)
  전체 테이블을 복사할지 여부를 지정한 후나 쿼리를 입력하고 나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사가 **원본 테이블 및 뷰 선택**을 표시합니다. 이 페이지에서는 복사할 기존 테이블 및 뷰를 선택합니다. 그런 다음 원본 테이블을 새 대상 테이블 또는 기존 대상 테이블에 매핑합니다. 필요에 따라 개별 열의 매핑을 검토하고 샘플 데이터를 미리 봅니다.

> [!TIP]
> 둘 이상의 SQL Server 데이터베이스 또는 테이블과 뷰 이외의 다른 SQL Server 데이터베이스 개체를 복사해야 하는 경우 가져오기 및 내보내기 마법사 대신 데이터베이스 복사 마법사를 사용합니다. 자세한 내용은 [데이터베이스 복사 마법사 사용](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>스크린샷 - 테이블을 복사하려는 경우  
 다음 스크린샷은 이전에 **테이블 복사 또는 쿼리 지정** 페이지에서 **하나 이상의 테이블 또는 뷰에서 데이터 복사** 옵션을 선택했을 때 표시되는 마법사의 **원본 테이블 및 뷰 선택** 페이지의 예입니다. 데이터 원본에서 사용할 수 있는 모든 테이블 및 뷰가 목록에 표시됩니다.
 
이 예에서 **원본** 목록에는 AdventureWorks 샘플 데이터베이스의 모든 테이블이 포함되어 있습니다. 선택한 행은 사용자가 **Sales.Customer** 테이블을 원본에서 대상의 새 **Sales.CustomerNew** 테이블로 복사하려고 함을 보여 줍니다. 
   
 ![가져오기 및 내보내기 마법사의 테이블 선택 페이지](../../integration-services/import-export-data/media/select-tables1.png "가져오기 및 내보내기 마법사의 테이블 선택 페이지")
  
## <a name="screen-shot---if-you-provided-a-query"></a>스크린샷 - 쿼리를 제공한 경우  
 다음 스크린샷은 이전에 **테이블 복사 또는 쿼리 지정** 페이지에서 **전송 데이터를 지정할 쿼리 작성** 옵션을 선택했을 때 표시되는 마법사의 **원본 테이블 및 뷰 선택** 페이지의 예입니다. **원본** 목록에는 단일 행만 포함됩니다. 여기서 `[Query]`라는 항목은 **원본 쿼리 제공** 페이지에서 제공한 쿼리를 나타냅니다.
 
이 예제에서 사용자는 쿼리 결과를 원본에서 대상의 **Sales.CustomerNew** 테이블로 복사하려고 합니다.  
    
 ![가져오기 및 내보내기 마법사의 테이블 선택 페이지](../../integration-services/import-export-data/media/select-tables2.png "가져오기 및 내보내기 마법사의 테이블 선택 페이지")  

## <a name="select-source-and-destination-tables"></a>원본 및 대상 테이블 선택 
**원본**  
사용 가능한 목록에서 확인란을 사용하여 대상으로 복사할 테이블 및 뷰를 선택합니다. 기본적으로 데이터 원본의 데이터를 변경하지 않고 복사합니다. 새 대상 테이블을 만드는 경우 새 테이블에 대한 스키마(즉, 열 목록 및 해당 속성)도 데이터 원본에서 변경하지 않고 복사됩니다.

쿼리를 제공한 경우 목록에는 이름이 `[Query]`인 항목 하나만 포함됩니다. 

**대상**  
 목록에서 각 원본 테이블 또는 쿼리에 대한 대상 테이블을 선택하거나 마법사에서 만들려는 새 테이블의 이름을 입력합니다. 기존 대상 테이블을 선택할 경우 테이블의 열 데이터 형식이 원본 데이터와 호환되어야 합니다.  

> [!NOTE]
> 외부 도구(예:  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])를 사용하여 대상 데이터베이스에서 새 테이블을 만들기 위해 마법사의 이 지점에서 일시 중지할 경우 사용 가능한 대상 테이블의 목록에 새 테이블이 즉시 표시되지는 않습니다. 대상 테이블 목록을 새로 고치려면 **대상 선택** 페이지로 돌아가 대상 데이터베이스를 다시 선택하여 사용 가능한 테이블 및 뷰 목록을 새로 고친 다음 다시 **원본 테이블 및 뷰 선택** 페이지로 이동합니다.  

## <a name="optionally-review-column-mappings-and-preview-data"></a>필요에 따라 열 매핑 검토 및 데이터 미리 보기
**매핑 편집**   
필요에 따라 **매핑 편집**을 클릭하여 선택한 테이블에 대한 **열 매핑** 대화 상자를 표시합니다. **열 매핑** 대화 상자를 사용하여 다음을 수행합니다.
-   원본과 대상 간의 개별 열 매핑을 검토합니다.
-   복사하지 않을 열에 **무시** 를 선택하여 일부 열만 복사합니다.

자세한 내용은 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.  

**미리 보기**  
필요에 따라 **미리 보기**를 클릭하여 **데이터 미리 보기** 대화 상자에서 최대 200개의 샘플 데이터 행을 미리 봅니다. 이를 통해 원하는 데이터를 마법사가 복사하는지 확인할 수 있습니다. 자세한 내용은 [데이터 미리 보기](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
데이터를 미리 본 후 마법사의 이전 페이지에서 선택한 옵션을 변경할 수도 있습니다. 이렇게 변경하려면 **원본 테이블 및 뷰 선택** 페이지로 돌아간 다음 **뒤로** 를 클릭하여 선택 내용을 변경할 수 있는 이전 페이지로 돌아갑니다.  

## <a name="select-source-and-destination-tables-for-excel"></a>Excel에 대한 원본 및 대상 테이블 선택

### <a name="excel-source-tables"></a>Excel 원본 테이블
Excel 데이터 원본에 대한 원본 테이블 및 뷰 목록에는 두 가지 유형의 Excel 개체가 포함됩니다.
-   **워크시트**. 워크시트 이름 뒤에는 달러 기호($)가 옵니다(예: **'Sheet1$ '**).
-   **명명된 범위.** 명명된 범위(있는 경우)는 이름별으로 나열됩니다.

명명되지 않는 특정 셀 범위(예: **[Sheet1$A1:B4]**)에서 또는 해당 범위로 데이터를 로드하려면 쿼리를 작성해야 합니다. **테이블 복사 또는 쿼리 지정** 페이지로 돌아가서 **전송 데이터를 지정할 쿼리 작성**을 선택합니다.

#### <a name="prepare-the-excel-source-data"></a>Excel 원본 데이터 준비
워크시트 또는 범위를 원본 테이블로 지정하면 드라이버는 워크시트 또는 범위의 가장 왼쪽에서 비어 있지 않은 첫 번째 셀부터 *인접한* 블록의 셀을 읽습니다. 따라서 원본 데이터에 빈 행이 있으면 안 됩니다. 예를 들어 열 머리글과 데이터 행 사이에 빈 행이 있으면 안 됩니다. 워크시트 맨 위에서 데이터 위에 제목 다음에 빈 행이 있으면 워크시트를 쿼리할 수 없습니다. Excel에서 데이터의 범위에 이름을 할당하고 워크시트 대신 명명된 범위를 쿼리해야 합니다.

### <a name="excel-destination-tables"></a>Excel 대상 테이블
Excel로 데이터를 내보내는 경우에 다음 세 가지 방법 중 하나로 대상을 지정할 수 있습니다.
-   **워크시트.** 워크시트를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$]**).
-   **명명된 범위.** 명명된 범위를 지정하려면 범위 이름을 사용하면 됩니다(예: **MyDataRange**).
-   **명명되지 않은 범위.** 명명하지 않은 셀의 범위를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$A1:B4]**).

## <a name="special-considerations-for-excel-sources-and-destinations"></a>Excel 원본 및 대상에 대한 특별 고려 사항
Excel을 원본 또는 대상으로 사용하는 경우 **매핑 편집** 을 클릭하고 **열 매핑** 페이지에서 데이터 형식 매핑을 검토하는 것이 좋습니다. 

**Excel 통합 문서의 데이터 형식**. Excel 일반적인 데이터베이스가 아닙니다. 열의 데이터 형식이 고정되어 있지 않습니다. 마법사는 Excel에서 제한된 데이터 형식 집합(숫자, 통화, 부울, 날짜/시간, 문자열(255자 미만), 메모(255자 이상))만 인식합니다. 마법사는 Excel 데이터 원본에서 특정 개수의 행(기본값: 처음 8개 행)을 샘플링하여 각 열의 데이터 형식을 추측합니다.

마법사가 Excel에서 또는 Excel로 데이터를 로드하기 위해 명시적 데이터 형식 변환을 수행해야 하는 경우 일반적으로 이러한 변환을 검토할 수 있는 **데이터 형식 매핑 검토** 페이지가 표시됩니다. 이러한 변환에는 다음이 포함될 수 있습니다.
-   배정밀도 Excel 숫자 열과 다른 유형의 숫자 열 간 변환
-   255자 Excel 문자열 열과 길이가 다른 문자열 열 간 변환
-   유니코드 Excel 문자열 열과 특정 코드 페이지를 사용하는 비유니코드 문자열 열 간 변환

### <a name="special-considerations-for-excel-sources"></a>Excel 원본에 대한 특별 고려 사항
**가져온 데이터의 null 값 또는 누락된 값**. 마법사에서 샘플링한 처음 8개 행의 Excel 열에 혼합된 데이터 형식(예: 숫자 값과 텍스트 값의 혼합)이 있는 것으로 나타나는 경우, 마법사는 대다수의 데이터 형식을 열의 데이터 형식으로 선택하고 다른 형식의 데이터를 포함하는 셀에 대해서는 null 값을 반환합니다. 마법사의 이 동작은 변경할 수 없습니다.

**가져온 데이터의 잘린 문자열**. Excel 열에 텍스트 데이터가 포함된 경우 마법사는 첫 번째 8개 행에서 샘플링하는 가장 긴 값을 기준으로 열의 데이터 형식(string 또는 memo)를 선택합니다. 마법사가 샘플링하는 행에서 255자보다 긴 값을 찾지 못하는 경우 열을 메모 열이 아니라 255자 문자열 열로 간주하고 255자보다 긴 값을 자릅니다. 메모 열에서 잘림 없이 데이터를 가져오려면 메모 열에 마법사에서 샘플링한 처음 8개 행에 255자보다 긴 값이 하나 이상 포함되어 있는지 확인해야 합니다.

### <a name="special-considerations-for-excel-destinations"></a>Excel 대상에 대한 특별 고려 사항
**기존 범위 지정**. 기존 범위를 대상으로 지정하는 경우 범위가 원본 데이터의 *열 수*보다 적으면 오류가 발생합니다. 그러나 지정하는 범위가 원본 데이터의 *행 수*보다 적으면 마법사에서 행 쓰기를 계속하고 범위 정의를 새 행 수와 일치하도록 확장합니다.

**메모(ntext) 데이터 저장**. 255자보다 긴 문자열을 Excel 열에 저장하려면 마법사에서 대상 열의 데이터 형식을 **string** 이 아닌 **memo**로 인식해야 합니다.
-   대상 테이블에 이미 데이터 행이 포함되어 있는 경우 마법사에서 샘플링한 처음 8개 행의 메모 열에 255자보다 긴 값이 있는 행이 하나 이상 포함되어 있어야 합니다.
-   마법사에서 대상 테이블을 만드는 경우 **CREATE TABLE** 문은 메모 열의 데이터 형식으로 **LONGTEXT**(또는 해당 동의어 중 하나)를 사용해야 합니다. 필요한 경우 **열 매핑** 페이지의 **대상 테이블 만들기** 옵션 옆에 있는 **SQL 편집**을 클릭하여 **CREATE TABLE** 문을 확인하고 수정합니다.

## <a name="whats-next"></a>다음 단계  
 대상에 복사 및 매핑할 기존 테이블 및 뷰를 선택한 후 다음 페이지는 **패키지 저장 및 실행**입니다. 이 페이지에서는 복사 작업을 즉시 실행할지 여부를 지정합니다. 구성에 따라 마법사에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 저장하여 사용자 지정하고 나중에 다시 사용할 수도 있습니다. 자세한 내용은 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.
 
 ## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


