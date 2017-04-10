---
title: "임시 테이블을 사용하여 분할 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
caps.latest.revision: 11
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 11
---
# 임시 테이블을 사용하여 분할
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  현재 및 기록 테이블에서 모두 독립적으로 분할을 사용할 수 있습니다. 그러나 분할은 시스템 버전 관리 없이 데이터의 내용을 변경하는 데 사용할 수 없습니다.  
  
> [!NOTE]  
>  분할은 Enterprise Edition 기능입니다.  
  
-   **현재 테이블:**  
  
    -   현재 테이블에 대한 **SWITCH IN**은 **SYSTEM_VERSIONING**이 **ON**인 동안 데이터 로드 및 쿼리를 용이하게 하는 데 사용할 수 있습니다.  
  
    -   **SYSTEM_VERSIONING**이 **ON**인 동안 **SWITCH OUT**은 허용되지 않습니다.  
  
-   **기록 테이블:**  
  
    -   **SYSTEM_VERSIONING**이 **ON**인 동안 기록 테이블에서 **SWITCH OUT**을 수행하여 더 이상 관련이 없는 기록 데이터 부분을 제거할 수 있습니다.  
  
    -   **SWITCH IN**은 임시 데이터 일관성을 무효화할 수 있으므로 **SYSTEM_VERSIONING**이 **ON**인 동안 허용되지 않습니다.  
  
## 이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Partitioning%20with%20Temporal%20Tables%20page)으로 보내 주세요.  
  
## 참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  