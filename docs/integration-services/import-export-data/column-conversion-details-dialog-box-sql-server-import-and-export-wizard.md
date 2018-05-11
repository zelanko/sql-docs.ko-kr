---
title: 열 변환 정보 대화 상자(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b14be85bc739a13790f51e887175dcdf77a166a9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>열 변환 정보 대화 상자(SQL Server 가져오기 및 내보내기 마법사)
  **데이터 형식 매핑 검토** 페이지의 개별 열에 대한 행을 두 번 클릭하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **열 변환 정보** 대화 상자가 표시됩니다. 이 페이지에서 개별 열에 대한 자세한 변환 정보를 검토할 수 있습니다. 이 정보에는 다음 항목이 포함됩니다.
-   원본 및 대상의 열 데이터 형식입니다.
-   변환이 필요한 경우 마법사에서 수행하는 데이터 형식 변환입니다.
-   마법사에서 필요한 데이터 형식 변환을 결정하는 데 사용하는 데이터 형식 매핑 파일입니다. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>열 변환 정보 페이지의 스크린샷 
 다음 스크린샷은 사용자가 **데이터 형식 매핑 검토** 페이지에서 행을 두 번 클릭하면 나타나는 마법사의 **열 변환 정보** 대화 상자를 보여 줍니다. **데이터 형식 매핑 검토** 페이지를 다시 보려면 [데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)를 참조하세요.
 
이 예에서는 다음과 같은 항목을 볼 수 있습니다.
-   원본 SQL Server 테이블의 `PersonID` 열은 `int` 형식입니다. 마법사는 데이터 형식 매핑 파일 MSSQLToSSIS10.xml을 참조하여 이 형식을 4바이트 부호 있는 정수인 SSIS(SQL Server Integration Services) `DT_I4` 데이터 형식에 매핑합니다.
-   대상 SQL Server 테이블의 `PersonID` 열은 `int` 형식이기도 합니다. 마법사는 이 형식을 동일한 SSIS 데이터 형식으로 매핑합니다.
-   마법사는 *이 열은 변환할 필요가 없다*고 결론을 내립니다.
 
  
 ![가져오기 및 내보내기 마법사의 열 변환 페이지](../../integration-services/import-export-data/media/column-conversion.png "가져오기 및 내보내기 마법사의 열 변환 페이지") 
  
## <a name="whats-next"></a>다음 단계  
 열 변환 정보를 검토하고 **확인**을 클릭하면 **열 변환 정보** 대화 상자에서 **데이터 형식 매핑 검토** 페이지를 표시합니다. 자세한 내용은 [데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)를 참조하세요.  

## <a name="see-also"></a>관련 항목:
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
