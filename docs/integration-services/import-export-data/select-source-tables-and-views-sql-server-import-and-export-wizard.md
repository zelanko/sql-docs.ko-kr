---
title: 원본 테이블 및 뷰 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3d3019419538c05efc28ceabc5324d373500f65c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285132"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>원본 테이블 및 뷰 선택(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.

### <a name="excel-source-tables"></a>Excel 원본 테이블
Excel 데이터 원본에 대한 원본 테이블 및 뷰 목록에는 두 가지 유형의 Excel 개체가 포함됩니다.
-   **워크시트**. 워크시트 이름 뒤에는 달러 기호($)가 옵니다(예: **'Sheet1$ '** ).
-   **명명된 범위.** 명명된 범위(있는 경우)는 이름별으로 나열됩니다.

명명되지 않는 특정 셀 범위(예: **[Sheet1$A1:B4]** )에서 또는 해당 범위로 데이터를 로드하려면 쿼리를 작성해야 합니다. **테이블 복사 또는 쿼리 지정** 페이지로 돌아가서 **전송 데이터를 지정할 쿼리 작성**을 선택합니다.

### <a name="excel-destination-tables"></a>Excel 대상 테이블
Excel로 데이터를 내보내는 경우에 다음 세 가지 방법 중 하나로 대상을 지정할 수 있습니다.
-   **워크시트.** 워크시트를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$]** ).
-   **명명된 범위.** 명명된 범위를 지정하려면 범위 이름을 사용하면 됩니다(예: **MyDataRange**).
-   **명명되지 않은 범위.** 명명하지 않은 셀의 범위를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$A1:B4]** ).

> [!TIP]
> Excel을 원본 또는 대상으로 사용하는 경우 **매핑 편집** 을 클릭하고 **열 매핑** 페이지에서 데이터 형식 매핑을 검토하는 것이 좋습니다. 

## <a name="whats-next"></a>다음 단계  
 대상에 복사 및 매핑할 기존 테이블 및 뷰를 선택한 후 다음 페이지는 **패키지 저장 및 실행**입니다. 이 페이지에서는 복사 작업을 즉시 실행할지 여부를 지정합니다. 구성에 따라 마법사에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 저장하여 사용자 지정하고 나중에 다시 사용할 수도 있습니다. 자세한 내용은 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.
 
 ## <a name="see-also"></a>관련 항목:
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)



