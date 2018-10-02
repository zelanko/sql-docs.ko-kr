---
title: 테이블 편집 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 108b3bf1ccd37b92144bcf0aa21d60546dc68979
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613001"
---
# <a name="edit-tables"></a>테이블 편집
  **테이블** 탭을 사용하여 Oracle 원본 데이터베이스에서 선택한 테이블과 열을 변경할 수 있습니다. 이 탭은 다음과 같은 요소로 구성되어 있습니다.  
  
 **테이블 목록**  
 테이블 목록은 다음과 같은 세 개의 열이 있습니다.  
  
-   **Oracle 테이블 이름**: 테이블의 이름(테이블 스키마 포함)입니다.  
  
-   **캡처 인스턴스**: 인스턴스별 변경 데이터 캡처 개체의 이름 지정에 사용되는 캡처 인스턴스의 이름입니다. 캡처 인스턴스는 NULL일 수 없습니다. 지정하지 않으면 이름은 원본 스키마 이름에 원본 테이블 이름을 붙인 `<schema-name>_<table-name>.` 형식으로 파생됩니다. 캡처 인스턴스 이름은 100자를 초과할 수 없으며 데이터베이스 내에서 고유해야 합니다. 이 열에서 셀을 클릭하여 **capture_instance**를 수동으로 편집할 수 있습니다.  
  
-   **보안 역할**: 변경 데이터에 대한 액세스 권한을 얻는 데 사용되는 데이터베이스 역할의 이름입니다. 이 열에서 셀을 클릭하여 **security_role**을 수동으로 편집할 수 있습니다.  
  
 **테이블 추가**  
 **테이블 추가** 를 클릭하면 테이블 선택 대화 상자가 열립니다. 이 대화 상자에서 [CDC 인스턴스에 테이블을 추가](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)할 수 있습니다. 이 세션에서 Oracle 데이터베이스에 처음으로 액세스하는 경우 [Connect to Oracle](../../integration-services/change-data-capture/connect-to-oracle.md)해야 합니다.  
  
 **편집**  
 목록에서 테이블을 선택하고 **편집** 을 선택하여 해당 테이블에 대한 **속성** 대화 상자를 엽니다. 이 대화 상자에서 [테이블 속성을 편집](../../integration-services/change-data-capture/edit-the-table-properties.md)할 수 있습니다.  
  
> [!NOTE]  
>  미러 테이블이 이미 있는 테이블에 대한 형식 매핑을 편집할 수 없습니다. 이 작업은 새 테이블에 대해서만 수행할 수 있습니다.  
  
 **제거**  
 목록에서 테이블을 선택하고 **제거** 를 클릭하여 CDC 인스턴스에서 테이블을 제거할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC 인스턴스 속성을 편집하는 방법](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Oracle 테이블 및 열 선택](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
