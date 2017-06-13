---
title: "임시 테이블 고려 사항 및 제한 사항 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8a21481-0f0e-41e3-a1ad-49a84091b422
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 30791ad9733446f664db1592b95d1ffec5fc9a1b
ms.openlocfilehash: 5ee3aa9223ae8ab832eff23a1da1755278e86d0b
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017

---
# <a name="temporal-table-considerations-and-limitations"></a>임시 테이블 고려 사항 및 제한 사항
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  시스템 버전 관리의 특성으로 인해 임시 테이블을 사용하는 경우 고려해야 할 몇 가지 고려 사항 및 제한 사항이 있습니다.  
  
 임시 테이블 관련 작업을 수행할 때는 다음 사항을 고려해야 합니다.  
  
-   임시 테이블에는 기본 키가 정의되어야 현재 테이블과 기록 테이블 사이에서 레코드를 연결할 수 있고 기록 테이블에는 기본 키를 정의할 수 없습니다.  
  
-   SYSTEM_TIME 기간 열은 **SysStartTime** 을 기록하기 위해 사용되고 **SysEndTime** 값은 datetime2 데이터 형식으로 정의되어야 합니다.  
  
-   기록 테이블 생성 도중 기록 테이블의 이름을 지정하는 경우 스키마와 테이블 이름을 지정해야 합니다.  
  
-   기본적으로 기록 테이블은 **PAGE** (으)로 압축됩니다.  
  
-   구성 분할은 현재 테이블에서 기록 테이블로 자동 복제를 수행하지 않기 때문에 현재 테이블이 분할된 경우 기록 테이블은 기본 파일 그룹에 생성됩니다.  
  
-   임시 및 기록 테이블은 **FILETABLE** 이 될 수 없고 **FILESTREAM** 을 제외한 지원되는 모든 데이터 형식의 열을 포함할 수 있습니다. 그 이유는 **FILETABLE** 및 **FILESTREAM** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부에서의 데이터 조작을 허용하여 시스템 버전 관리가 보장되지 않기 때문입니다.  
  
-   **(n)varchar(max)**, **varbinary(max)**, **(n)text** 및 **image**등의 임시 테이블은 BLOB 데이터 형식을 지원하는 반면 크기로 인해 상당한 저장소 비용이 부과되고 성능이 저하됩니다. 따라서 이러한 데이터 유형을 사용하는 경우 시스템 설계 시 유의해야 합니다.  
  
-   기록 테이블은 현재 테이블과 동일한 데이터베이스에 만들어야 합니다. **Linked Server** 에서의 임시 쿼리는 지원되지 않습니다.  
  
-   기록 테이블은 제약 조건(기본 키, 외래 키, 테이블 또는 열 제약 조건)을 가질 수 없습니다.  
  
-   인덱싱된 뷰는 임시 쿼리를 기반으로 사용할 수 없습니다( **FOR SYSTEM_TIME** 절을 사용하는 쿼리).  
  
-   시스템 버전 관리 임시 테이블에서는 Online 옵션 (**WITH (ONLINE = ON**)이 **ALTER TABLE ALTER COLUMN** 에 영향을 주지 않습니다. ONLINE 옵션에 지정된 값과 관계없이 열 변경은 온라인으로 수행되지 않습니다.  
  
-   **INSERT** 및 **UPDATE** 문은 SYSTEM_TIME 기간 열을 참조할 수 없습니다. 이러한 열에 직접 값을 삽입하려는 시도는 차단됩니다.  
  
-   **TRUNCATE TABLE** is not supported while **SYSTEM_VERSIONING** is **ON**  
  
-   기록 테이블의 데이터를 직접 수정하는 것은 허용되지 않습니다.  
  
-   **ON DELETE CASCADE** 및 **ON UPDATE CASCADE** 은 현재 테이블에서 허용되지 않습니다. 즉, 임시 테이블이 외래 키 관계(sys.foreign_keys의 *parent_object_id* 에 해당)인 경우 CASCADE 옵션은 허용되지 않습니다. 이러한 제약 조건으로 작업하려면 응용 프로그램 논리를 사용하거나 트리거 후에 기본 키 테이블(sys.foreign_keys의  *referenced_object_id* 에 해당)에서 삭제 시 일관성을 유지하세요. 기본 키 테이블이 임시이고 참조 테이블이 비임시인 경우 그러한 제한 사항이 없습니다. 

    **참고:** 이 제한 사항은 SQL Server 2016에만 적용 합니다. CASCADE 옵션에서 사용할 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 및 SQL Server 2017 CTP 2.0에서 시작 합니다.  
  
-   DML 논리 무효화를 방지하기 위해**INSTEAD OF** 트리거가 현재 또는 기록 테이블에서 허용되지 않습니다. **AFTER** 트리거는 현재 테이블에서만 허용됩니다. DML 논리 무효화를 방지하기 위해 기록 테이블에서 차단됩니다.  
  
-   복제 기술은 제한적으로 사용됩니다.  
  
    -   **항상 사용 가능:** 모두 지원  
  
    -   **변경 데이터 캡처 및 변경 데이터 추적:** 현재 테이블에서만 지원  
  
    -   **스냅숏 및 트랜잭션 복제**: 임시로 활성화되지 않은 단일 게시자 및 임시로 활성화된 한 구독자에서만 지원됩니다. 이 경우, 게시자는 OLTP 작업에서 사용되고 구독자는 오프로딩 보고서(‘AS OF’ 쿼리 포함)에서 사용됩니다.    
        각 구독자가 로컬 시스템 시계에 의존하여 임시 데이터가 일치하지 않을 수 있으므로 다중 구독자를 사용할 수 없습니다.  
  
    -   **병합 복제:** 임시 테이블에서 지원되지 않습니다.  
  
-   일반 쿼리는 현재 테이블의 데이터에만 영향을 줍니다. 기록 테이블에서 데이터를 쿼리하려면 임시 쿼리를 사용해야 합니다. 이것에 대한 설명은 이 문서의 임시 데이터 쿼리 섹션에서 차후에 설명됩니다.  
  
-   최적의 인덱싱 전략은 현재 테이블에 클러스터형 열 저장소 인덱스 및/또는 B-트리 rowstore 인덱스를 포함하고 기록 테이블에 클러스터형 columnstore 인덱스를 포함하여 최적의 저장소 크기와 성능을 획득하는 것입니다. 자체 기록 테이블을 생성/사용하는 경우 기간 열의 마지막에서 시작하는 기간 열로 구성되는 유형의 인덱스를 만들어 임시 쿼리 속도를 향상시키고 데이터 일관성 확인의 일부인 쿼리의 속도를 향상시키는 것이 좋습니다. 기본 기록 테이블은 기간 열(끝, 시작)을 기반으로 생성된 클러스터형 rowstore 인덱스를 가질 수 있습니다. 최소한 비클러스터형 rowstore 인덱스를 사용하는 것이 좋습니다.  
  
-   기록 테이블을 만들 때 다음 개체/속성은 현재 테이블에서 기록 테이블로 복제되지 않습니다.  
  
    -   기간 정의  
  
    -   ID 정의  
  
    -   인덱스  
  
    -   통계  
  
    -   CHECK 제약 조건  
  
    -   트리거  
  
    -   분할 구성  
  
    -   사용 권한  
  
    -   행 수준 보안 조건자  
  
-   일련의 기록 테이블에서 기록 테이블은 현재 테이블로 구성될 수 있습니다.  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20Considerations%20and%20Limitations%20page)  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

