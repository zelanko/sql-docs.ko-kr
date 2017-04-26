---
title: "임시 테이블 보안 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 60e5d6f6-a26d-4bba-aada-42e382bbcd38
caps.latest.revision: 9
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f73cdc0f3a240e3d4c795fd67c2913b99748de4a
ms.lasthandoff: 04/11/2017

---
# <a name="temporal-table-security"></a>임시 테이블 보안
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  임시 테이블에 보안이 적용되는 방식을 이해하려면 임시 테이블에 적용되는 보안 원칙을 이해하는 것이 중요합니다. 이러한 보안 원칙을 이해한 이후에 **CREATE TABLE**, **ALTER TABLE**, **SELECT** 문에 대한 보안을 자세히 파악할 수 있습니다.  
  
## <a name="security-principles"></a>보안 원칙  
 다음 표는 임시 테이블에 적용되는 보안 원칙에 대해 설명합니다.  
  
|원칙|설명|  
|---------------|-----------------|  
|system-versioning을 설정/해제하려면 영향을 받는 개체에 대해 가장 높은 권한이 있어야 함|SYSTEM_VERSIONING을 설정 및 해제하려면 현재 및 기록 테이블에 대해 CONTROL 권한이 있어야 합니다.|  
|기록 데이터는 직접 수정할 수 없음|SYSTEM_VERSIONING이 ON일 경우 사용자가 현재 또는 기록 테이블에 대해 가지고 있는 실제 권한과 상관없이 기록 데이터를 수정할 수 없습니다. 여기에는 데이터 및 스미카 수정이 포함됩니다.|  
|기록 데이터를 쿼리하려면 기록 테이블에 대해 **SELECT** 권한이 있어야 함|현재 테이블에 대해 **SELECT** 권한이 있는 사용자가 반드시 기록 테이블에 대해 **SELECT** 권한이 있는 것이 아닙니다.|  
|감사를 수행할 경우 기록 테이블에 특정 방식으로 영향을 미치는 작업이 표시됩니다.|기록 테이블을 정기적으로 감사할 경우 직접적인 데이터 액세스 시도를 모두 캡처할 수 있습니다(성공 여부와 무관).<br /><br /> 임시 쿼리 확장이 포함된**SELECT** 는 기록 테이블이 해당 작업으로 영향을 받았음을 표시합니다.<br /><br /> **CREATE/ALTER** 임시 테이블에 기록 테이블에서도 사용 권한 검사가 실행된다는 정보가 표시됩니다. 감사 파일에는 기록 테이블에 대한 추가 기록이 포함됩니다.<br /><br /> 현재 테이블에 DML 작업을 적용할 경우 기록 테이블이 영향을 받았다는 내용이 표시되지만 additional_info가 필요한 컨텍스트를 제공합니다(DML은 system_versioning의 결과임).|  
  
## <a name="performing-schema-operations"></a>스키마 작업 수행  
 SYSTEM_VERSIONING이 ON으로 설정된 경우에는 스키마 수정 작업이 제한됩니다.  
  
### <a name="disallowed-alter-schema-operations"></a>허용되지 않는 ALTER 스키마 작업  
  
|연산|현재 테이블|기록 테이블|  
|---------------|-------------------|-------------------|  
|**DROP TABLE**|허용되지 않음|허용되지 않음|  
|**ALTER TABLE...SWITCH PARTITION**|SWITCH IN만( [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)참조)|SWITCH OUT만( [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)참조)|  
|**ALTER TABLE...DROP PERIOD**|허용되지 않음|-|  
|**ALTER TABLE...ADD PERIOD**|-|허용되지 않음|  
  
## <a name="allowed-alter-table-operations"></a>허용되는 ALTER TABLE 작업  
  
|연산|현재|기록|  
|---------------|-------------|-------------|  
|**ALTER TABLE...REBUILD**|허용됨(독립적)|허용됨(독립적)|  
|**CREATE  INDEX**|허용됨(독립적)|허용됨(독립적)|  
|**CREATE STATISTICS**|허용됨(독립적)|허용됨(독립적)|  
  
## <a name="security-of-the-create-temporal-table-statement"></a>CREATE Temporal TABLE 문의 보안  
  
||새 기록 테이블 만들기|기존 기록 테이블 재사용|  
|-|------------------------------|----------------------------------|  
|필요 권한|데이터베이스의**CREATE TABLE** 권한<br /><br /> 현재 및 기록 테이블을 만들고 있는 대상 스키마에 대한**ALTER** 권한|데이터베이스의**CREATE TABLE** 권한<br /><br /> 현재 테이블을 만들 대상 스키마에 대한**ALTER** 권한<br /><br /> 임시 테이블을 만드는**CONTROL** 문의 일부로 지정된 기록 테이블에 대한 **CONTROL** 권한|  
|감사|감사를 실행할 경우 사용자가 두 개의 개체를 만들려는 시도를 했음이 표시됩니다. 데이터베이스에 테이블을 만들 수 있는 권한이 없거나 각 테이블의 스키마를 수정할 수 있는 권한이 없는 경우 작업이 실패할 수 있습니다.|감사를 실행할 경우 임시 테이블이 생성되었음이 표시됩니다. 데이터베이스에 테이블을 만들 권한이 없거나 임시 테이블에 대한 스키마를 수정할 권한이 없거나 기록 테이블에 대한 권한이 없는 경우 작업이 실패할 수 있습니다.|  
  
## <a name="security-of-the-alter-temporal-table-set-systemversioning-onoff-statement"></a>ALTER Temporal TABLE SET(SYSTEM_VERSIONING ON/OFF) 문의 보안  
  
||새 기록 테이블 만들기|기존 기록 테이블 재사용|  
|-|------------------------------|----------------------------------|  
|필요 권한|데이터베이스의**CONTROL** 권한<br /><br /> 데이터베이스의**CREATE TABLE** 권한<br /><br /> 기록 테이블을 만들고 있는 대상 스키마에 대한**ALTER** 권한|수정된 원본 테이블에 대한**CONTROL** 권한<br /><br /> **ALTER TABLE** 문의 일부로 지정된 기록 테이블에 대한 **CONTROL** 권한|  
|감사|감사 시 임시 테이블이 수정되었으며 그와 동시에 기록 테이블이 생성되었다는 내용이 표시됩니다. 데이터베이스에 테이블을 만들 권한이 없거나 기록 테이블의 스키마를 수정할 권한이 없거나 임시 테이블을 수정할 권한이 없는 경우 작업이 실패할 수 있습니다.|감사 시 임시 테이블이 수정되었지만 해당 작업에서 기록 테이블에 대한 액세스가 필요하다는 내용이 표시됩니다. 기록 테이블에 대한 권한이 없거나 현재 테이블에 대한 권한이 없는 경우 작업이 실패할 수 있습니다.|  
  
## <a name="security-of-select-statement"></a>SELECT 문의 보안  
 기록 테이블에 영향을 미치지 않는**SELECT** 문에 대한 **SELECT** 권한은 변경되지 않습니다. 기록 테이블에 영향을 미치는 **SELECT** 문의 경우 현재 테이블과 기록 테이블에 대한 **SELECT** 권한이 필요합니다.  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20Security%20page)  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

