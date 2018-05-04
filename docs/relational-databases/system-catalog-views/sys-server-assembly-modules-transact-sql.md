---
title: sys.server_assembly_modules (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_assembly_modules_TSQL
- sys.server_assembly_modules
- server_assembly_modules
- sys.server_assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_assembly_modules catalog view
ms.assetid: af799e38-2d16-49b2-bcf5-6f9199af899e
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1985c31345e377f796ef9ee77fdce6714ddb7766
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysserverassemblymodules-transact-sql"></a>sys.server_assembly_modules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  TA 유형의 서버 수준 트리거에 대한 어셈블리 모듈마다 한 행씩 포함합니다. 이 뷰에서는 어셈블리 트리거를 기본 CLR 구현으로 매핑합니다. 이 관계를 조인할 수 **sys.server_triggers**합니다. 어셈블리에 로드 해야는 **마스터** 데이터베이스입니다. 튜플(object_id)은 관계에 대한 키입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 어셈블리 모듈이 정의되는 개체에 대한 FOREIGN KEY 역참조입니다.|  
|**assembly_id**|**int**|이 모듈이 생성된 어셈블리의 ID입니다. 어셈블리는 master 데이터베이스에 로드되어야 합니다.|  
|**assembly_class**|**sysname**|이 모듈을 정의하는 어셈블리 내 클래스의 이름입니다.|  
|**assembly_method**|**sysname**|이 모듈을 정의하는 클래스 내 메서드의 이름입니다. AF(집계 함수)의 경우 NULL입니다.|  
|**execute_as_principal_id**|**int**|EXECUTE AS 서버 보안 주체의 ID입니다.<br /><br /> 기본값은 NULL이며 EXECUTE AS CALLER인 경우에도 NULL입니다.<br /><br /> 경우 지정한 보안 주체의 ID AS SELF EXECUTE AS 실행 \<주 > 합니다.<br /><br /> -2 = EXECUTE AS OWNER|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
