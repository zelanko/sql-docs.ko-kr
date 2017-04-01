---
title: "Oracle 테이블 및 열 선택 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "selTabCol"
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Oracle 테이블 및 열 선택
  Oracle 테이블 및 열 선택 페이지를 사용하여 변경이 캡처되는 Oracle 원본 데이터베이스에서 테이블을 선택할 수 있습니다. 이 페이지는 다음과 같은 요소로 구성되어 있습니다.  
  
## 옵션  
 **테이블 목록**  
 테이블 목록은 다음과 같은 세 개의 열이 있습니다.  
  
-   **Oracle 테이블 이름**: 테이블의 이름(테이블 스키마 포함)입니다.  
  
-   **캡처 인스턴스**: 인스턴스별 변경 데이터 캡처 개체의 이름 지정에 사용되는 캡처 인스턴스의 이름입니다. 캡처 인스턴스는 NULL일 수 없습니다.  
  
     지정하지 않으면 이름은 원본 스키마 이름에 원본 테이블 이름을 붙인 `<schema-name>_<table-name>`형식으로 파생됩니다. 캡처 인스턴스 이름은 100자를 초과할 수 없으며 데이터베이스 내에서 고유해야 합니다.  
  
     이 열에서 셀을 클릭하여 **capture_instance**를 수동으로 편집할 수 있습니다.  
  
-   **보안 역할**: 변경 데이터에 대한 액세스를 제어하는 데 사용되는 데이터베이스 제어 역할의 이름입니다.  
  
     이 열에서 셀을 클릭하여 **security_role**을 수동으로 편집할 수 있습니다.  
  
 **테이블 추가**  
 **테이블 추가**를 클릭하면 테이블 선택 대화 상자가 열립니다. 이 대화 상자에서 [변경 내용을 캡처할 Oracle 테이블을 선택](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)할 수 있습니다.  
  
 **편집**  
 목록에서 테이블을 선택하고 **편집**을 선택하여 해당 테이블에 대한 **속성** 대화 상자를 엽니다. 이 대화 상자에서 [변경 캡처를 위해 선택된 테이블을 변경](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)할 수 있습니다.  
  
 **제거**  
 목록에서 테이블을 선택하고 **제거**를 클릭하여 CDC 인스턴스에서 테이블을 제거할 수 있습니다.  
  
 올바른 대화 상자를 사용하여 [변경 내용을 캡처할 Oracle 테이블을 선택](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)하고 [변경 캡처를 위해 선택된 테이블을 변경](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)한 후에는 **다음**을 클릭하여 [보완 로깅 스크립트를 생성 및 실행](../../integration-services/change-data-capture/generate-and-run-the-supplemental-logging-script.md)합니다.  
  
## 관련 항목:  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [테이블 편집](../../integration-services/change-data-capture/edit-tables.md)   
 [CDC 인스턴스에 테이블 추가](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)   
 [테이블 속성 편집](../../integration-services/change-data-capture/edit-the-table-properties.md)  
  
  