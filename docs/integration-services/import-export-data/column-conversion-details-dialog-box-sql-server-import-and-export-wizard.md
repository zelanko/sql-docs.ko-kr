---
title: "열 변환 정보 대화 상자 (SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 985ba8a478999a153b3bb32649b98c3e809fc5e8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>열 변환 정보 대화 상자(SQL Server 가져오기 및 내보내기 마법사)
  **데이터 형식 매핑 검토** 페이지의 개별 열에 대한 행을 두 번 클릭하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **열 변환 정보** 대화 상자가 표시됩니다. 이 페이지에서 개별 열에 대한 자세한 변환 정보를 검토할 수 있습니다. 이 정보에는 다음 항목이 포함됩니다.
-   원본과 대상에 있는 열의 데이터 형식입니다.
-   데이터 형식으로 변환 하는 경우 마법사를 수행 하는 변환입니다.
-   마법사에서 필요한 데이터 형식 변환을 결정하는 데 사용하는 데이터 형식 매핑 파일입니다. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>열 변환 정보 페이지의 스크린샷 
 다음 스크린샷은 사용자가 **데이터 형식 매핑 검토** 페이지에서 행을 두 번 클릭하면 나타나는 마법사의 **열 변환 정보** 대화 상자를 보여 줍니다. **데이터 형식 매핑 검토** 페이지를 다시 보려면 [데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)를 참조하세요.
 
이 예제에서는 다음 사항을 확인할 수 있습니다.
-   `PersonID` 형식의 원본 SQL Server 테이블의 열은 `int`합니다. 마법사가 SQL Server Integration Services (SSIS)에이 형식을 매핑합니다 `DT_I4` MSSQLToSSIS10.xml 데이터 형식 매핑 파일을 참조 하 여 있는 4 바이트 부호 있는 정수 데이터 형식입니다.
-   `PersonID` 대상 SQL Server 테이블의 열 형식 이기도 한 `int`합니다. 마법사에이 형식을 매핑하는 동일한 SSIS 데이터 형식입니다.
-   마법사 완료 *이 열에서 변환 하지 않아도*합니다.
 
  
 ![열 변환 페이지 가져오기 및 내보내기 마법사의](../../integration-services/import-export-data/media/column-conversion.png "열 변환 페이지 가져오기 및 내보내기 마법사") 
  
## <a name="whats-next"></a>다음 단계  
 열 변환 정보를 검토하고 **확인**을 클릭하면 **열 변환 정보** 대화 상자에서 **데이터 형식 매핑 검토** 페이지를 표시합니다. 자세한 내용은 [데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)를 참조하세요.  

## <a name="see-also"></a>참고 항목
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

