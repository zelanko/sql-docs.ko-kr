---
title: "데이터 형식 매핑 검토(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8f9c2ddd8834d5ff3dbef2d0aff725343fae4f41
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>데이터 형식 매핑 검토(SQL Server 가져오기 및 내보내기 마법사)
**열 매핑** 대화 상자의 **매핑** 목록에서 성공하지 않을 수 있는 데이터 형식 매핑을 지정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **데이터 형식 매핑 검토** 페이지를 표시합니다. 이 페이지에서는 원본 데이터가 대상과 호환되도록 하기 위해 마법사에서 수행해야 하는 데이터 형식 변환에 대한 세부 정보를 검토합니다. 이 정보에는 오류 또는 잘림이 발생할 수 있는 변환에서 성공할 것으로 예상되는 데이터 형식 변환을 구별하는 시각적 표시가 포함됩니다. 각 변환에 대해 마법사에서 제안하는 변환을 적용할지 여부를 결정하고 발생할 수 있는 오류를 처리하는 방법을 지정합니다.   
  
> [!TIP]
> **데이터 형식 매핑 검토** 페이지에서는 데이터 형식 매핑을 변경할 수 없습니다. 그러나 **뒤로** 를 클릭하여 **원본 테이블 및 뷰 선택** 페이지로 돌아간 다음 **매핑 편집** 을 클릭하여 **열 매핑** 대화 상자를 다시 열 수 있습니다. **열 매핑** 대화 상자에서 성공할 가능성이 더 높은 데이터 형식 매핑을 지정할 수 있습니다. **열 매핑** 대화 상자를 다시 살펴보려면 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>데이터 형식 매핑 검토 페이지의 스크린샷
 다음 스크린샷에서는 마법사의 **데이터 형식 매핑 검토** 페이지의 예를 보여 줍니다.
 
 이 예에서는 다음과 같습니다.
 -   사용자가 **열 매핑** 대화 상자에서 성공하지 못할 수 있는 매핑을 지정했습니다.
 -   **테이블** 목록의 행에 있는 경고 아이콘은 쿼리 결과의 하나 이상 데이터 열을 대상 테이블의 호환되는 데이터 형식으로 변환하는 중 문제가 발생했음을 나타냅니다.
 -   **데이터 형식 매핑** 목록의 첫 번째 행에 있는 경고 아이콘은 원본 열의 **int** 데이터 형식을 대상 열의 **smalldatetime** 데이터 형식에 매핑하면 데이터가 손실될 수 있음을 나타냅니다.
 
 ![가져오기 및 내보내기 마법사의 데이터 형식 매핑 검토 페이지](../../integration-services/import-export-data/media/review-mapping.png "가져오기 및 내보내기 마법사의 데이터 형식 매핑 검토 페이지") 
 
## <a name="review-the-source-and-destination-tables"></a>원본 및 대상 테이블 검토  
 **데이터 형식 매핑 검토** 페이지의 위쪽 섹션은 원본에서 대상으로 복사할 테이블을 나열하는 **테이블** 목록입니다. 개별 테이블에 대한 변환 정보를 확인하려면 **테이블** 목록에서 테이블을 선택합니다. 선택한 테이블의 개별 열에 대한 변환 정보가 **페이지 아래쪽의 데이터 형식 매핑** 표에 표시됩니다.

이 예에서는 사용자가 제공한 쿼리의 결과가 대상의 Sales.CustomerNew2 테이블에 복사됩니다. 경고 아이콘은 쿼리 결과에서 하나 이상의 데이터 열을 대상 테이블의 호환되는 데이터 형식으로 변환하는 데 문제가 있음을 나타냅니다.

![매핑 검토 - 테이블](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 다음 표에서는 **테이블** 목록의 열에 대해 설명합니다.  
  
|Column|Description|  
|------------|-----------------|  
|(원본 아이콘)|데이터 형식 변환에 대한 성공 확률을 나타냅니다.<br /> - **녹색** 확인 표시 아이콘은 마법사에서 이 테이블에 대한 모든 데이터 형식 변환이 성공할 것으로 예상함을 나타냅니다.<br />- **노란색** 경고 아이콘은 마법사에서 수행할 개별 변환을 검토해야 함을 나타냅니다. 이러한 변환을 검토하려면 테이블을 선택한 다음 **데이터 형식 매핑** 목록의 개별 열에 대해 변환을 검토합니다.<br />- **빨간색** 오류 아이콘은 마법사에서 이 테이블에 대한 일부 변환을 안정적으로 수행할 수 없음을 나타냅니다.|  
|**원본**|원본 테이블의 이름입니다.|  
|(대상 아이콘)|대상이 이미 존재하는지, 아니면 마법사에 의해 만들어지는지를 나타냅니다.<br /> -   테이블 아이콘은 대상이 기존 테이블임을 나타냅니다.<br />-   해 모양이 있는 테이블 아이콘은 대상이 마법사에서 만드는 새 테이블임을 나타냅니다.|  
|**대상**|대상 테이블의 이름입니다.|  
  
## <a name="review-the-data-type-mappings"></a>데이터 형식 매핑 검토  
 **데이터 형식 매핑 검토** 페이지의 가운데 섹션은 **데이터 형식 매핑** 목록입니다. 이 그리드는 페이지 위쪽의 **테이블** 목록에서 선택된 원본 테이블의 열에 대한 자세한 변환 정보를 제공합니다.

이 예에서는 원본의 각 열이 동일한 이름과 데이터 형식이 있는 대상 열에 복사됩니다. **데이터 형식 매핑** 목록의 첫 번째 행에 있는 경고 아이콘은 원본 열의 **int** 데이터 형식을 대상 열의 **smalldatetime** 데이터 형식에 매핑하면 데이터가 손실될 수 있음을 나타냅니다.
 
![매핑 검토 - 매핑](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

다음 표에서는 **데이터 형식 매핑** 목록의 열에 대해 설명합니다. 

|Column|Description|  
|------------|-----------------|  
|(변환 아이콘)|데이터 형식 변환에 대한 성공 확률을 나타냅니다.<br /> - **녹색** 확인 표시 아이콘은 마법사에서 이 열에 대한 데이터 형식 변환이 성공할 것으로 예상함을 나타냅니다.<br />- **노란색** 경고 아이콘은 마법사에서 수행할 변환을 검토해야 함을 나타냅니다. 변환을 검토하려면 열을 두 번 클릭하여 **열 변환 정보** 대화 상자를 표시합니다. 자세한 내용은 [열 변환 정보 대화 상자](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)를 참조하세요.<br />- **빨간색** 오류 아이콘은 마법사에서 변환을 안정적으로 수행할 수 없음을 나타냅니다.|  
|**원본 열**|원본 열의 이름입니다.|  
|**원본 형식**|원본 열의 데이터 형식입니다.|  
|**대상 열**|대상 열의 이름입니다.|  
|**대상 형식**|대상 열의 데이터 형식입니다.|  
|**변환**|계획된 변환을 계속할지 여부를 지정합니다.<br /> -   마법사에서 계획된 변환을 계속하도록 하려면 확인란을 선택합니다.<br />-   데이터 형식 변환을 취소하려면 확인란의 선택을 취소합니다.|  
|**오류 발생 시**|마법사에서 오류를 처리하는 방법을 지정합니다.<br /> -   이 페이지의 맨 아래에서 지정할 수 있는 **오류 발생 시(전역)** 설정을 사용합니다.<br />-   오류가 발생하면 실패하고 가져오기 또는 내보내기 프로세스가 중지됩니다.<br />-   오류를 무시합니다.|  
|**잘림 발생 시**|마법사에서 잘림을 처리하는 방법을 지정합니다.<br /> -   이 페이지의 맨 아래에서 지정할 수 있는 **잘림 발생 시(전역)** 설정을 사용합니다.<br />-   오류가 발생하면 실패하고 가져오기 또는 내보내기 프로세스가 중지됩니다.<br />-   잘림을 무시합니다.|  

> [!TIP]
> 특정 데이터 열의 변환에 대한 세부 정보를 확인하려면 목록에서 임의의 행을 두 번 클릭합니다. **열 변환 정보** 대화 상자가 열리고 해당 열에 대한 보다 자세한 변환 정보가 표시됩니다. 자세한 내용은 [열 변환 정보 대화 상자](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)를 참조하세요.
 
## <a name="specify-global-error-handling-options"></a>전역 오류 처리 옵션 지정  
 **데이터 형식 매핑 검토** 페이지의 아래쪽 섹션에서는 기본적으로 모든 열에 적용되는 오류 처리 옵션을 지정할 수 있습니다. 이러한 설정은 **데이터 형식 매핑** 목록의 **오류 발생 시** 또는 **잘림 발생 시** 열에서 **전역 사용** 을 선택한 모든 변환에 적용됩니다.   

이 예에서는 두 가지 전역 오류 처리 옵션의 기본값을 보여 줍니다.

![매핑 검토 - 오류](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **오류 발생 시(전역)**  
 마법사에서 오류를 처리하는 방법을 지정합니다.  
 -   오류가 발생하면 실패하고 가져오기 또는 내보내기 프로세스가 중지됩니다. 이것은 기본값입니다.
 -   오류를 무시하고 가져오기 또는 내보내기 프로세스를 계속합니다.  
  
 **잘림 발생 시(전역)**  
 마법사에서 데이터 잘림을 처리하는 방법을 지정합니다.  
 -   오류가 발생하면 실패하고 가져오기 또는 내보내기 프로세스가 중지됩니다. 이것은 기본값입니다.
 -   잘림을 무시하고 가져오기 또는 내보내기 프로세스를 계속합니다.  
   
## <a name="whats-next"></a>다음 단계  
 경고를 검토하고 변환 옵션과 오류 처리 방법을 지정하면 **데이터 형식 매핑 검토** 페이지에서 **열 매핑** 대화 상자로 다시 이동됩니다. 자세한 내용은 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.  
 
 ## <a name="see-also"></a>관련 항목:
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

