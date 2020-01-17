---
title: 스키마 변경 내용을 위해 사용자 지정 프로시저 다시 생성(트랜잭션)
description: 트랜잭션 복제의 스키마 변경 내용을 반영하기 위해 사용자 지정 트랜잭션 저장 프로시저를 다시 생성합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e6a71e6591781f61560e4c997963571a49f816e5
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321439"
---
# <a name="transactional-articles---regenerate-to-reflect-schema-changes"></a>트랜잭션 아티클 - 스키마 변경 반영을 위해 다시 생성
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  기본적으로 트랜잭션 복제는 게시의 각 테이블 아티클에 대해 내부 프로시저로 생성된 저장 프로시저를 통해 구독자에서 모든 데이터 변경 내용을 적용합니다. 3개의 프로시저(삽입, 업데이트 및 삭제에 대해 각각 하나씩)가 구독자에 복사되고 삽입, 업데이트 또는 삭제가 구독자에 복제되면 실행됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자의 테이블에서 스키마를 변경하면 복제는 새 프로시저가 새 스키마와 일치하도록 동일한 내부 스크립팅 프로시저 집합을 호출하여 이러한 프로시저를 자동으로 다시 생성합니다. Oracle 게시자의 경우 스키마 변경 내용의 복제는 지원되지 않습니다.  
  
 또한 사용자 지정 프로시저를 지정하여 기본 프로시저 중 하나 이상을 바꿀 수 있습니다. 스키마 변경으로 인해 프로시저가 영향을 받는 경우에는 사용자 지정 프로시저를 변경해야 합니다. 예를 들어 프로시저가 스키마 변경에서 삭제된 열을 참조하는 경우 해당 열에 대한 참조를 프로시저에서 제거해야 합니다. 복제가 새 사용자 지정 프로시저를 구독자에 전파하는 방법에는 두 가지가 있습니다.  
  
-   첫 번째 옵션은 사용자 지정 스크립팅 프로시저를 사용하여 복제에서 사용하는 기본값을 바꾸는 것입니다.  
  
    1.  [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행하는 경우 `@schema_option` 0x02비트를 **true**로 설정해야 합니다.  
  
    2.  `@type` 매개 변수에 ‘insert’, ‘update’ 또는 ‘delete’ 값, `@value` 매개 변수에 사용자 지정 스크립팅 프로시저의 이름을 지정하고 [sp_register_custom_scripting&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)을 실행합니다.  
  
     다음에 스키마를 변경하면 복제는 이 저장 프로시저를 호출하여 사용자가 새로 정의한 사용자 지정 저장 프로시저에 대한 정의를 스크립팅한 다음 프로시저를 각 구독자로 전파합니다.  
  
-   두 번째 옵션은 새 사용자 지정 프로시저 정의를 포함하는 스크립트를 사용하는 것입니다.  
  
    1.  [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행하는 경우, 복제는 구독자에서 사용자 지정 프로시저가 자동으로 생성되지 않도록 `@schema_option` 0x02비트를 **false**로 설정합니다.  
  
    2.  각 스키마 변경 전에 새 스크립트 파일을 만들고 [sp_register_custom_scripting&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)을 실행하여 이 스크립트를 복제에 등록합니다. `@type` 매개 변수에 ‘custom_script’ 값, `@value` 매개 변수에 게시자의 스크립트 경로를 지정합니다.  
  
     다음에 관련 스키마를 변경하면 이 스크립트는 동일한 트랜잭션 내 각 구독자에서 DDL 명령으로 실행됩니다. 스키마를 변경한 다음에는 스크립트 등록이 취소됩니다. 후속 스키마 변경 이후에 스크립트를 실행하려면 해당 스크립트를 다시 등록해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
