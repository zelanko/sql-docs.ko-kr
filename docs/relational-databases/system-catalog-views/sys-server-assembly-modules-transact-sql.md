---
title: sys. server_assembly_modules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 714d0ca36bc48206ee7431454a61b51d2c31afb0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060557"
---
# <a name="sysserver_assembly_modules-transact-sql"></a>sys.server_assembly_modules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  TA 유형의 서버 수준 트리거에 대한 어셈블리 모듈마다 한 행씩 포함합니다. 이 뷰에서는 어셈블리 트리거를 기본 CLR 구현으로 매핑합니다. 이 관계를 **sys. server_triggers**에 조인할 수 있습니다. 어셈블리는 **master** 데이터베이스에 로드 되어야 합니다. 튜플(object_id)은 관계에 대한 키입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 어셈블리 모듈이 정의되는 개체에 대한 FOREIGN KEY 역참조입니다.|  
|**assembly_id**|**int**|이 모듈이 생성된 어셈블리의 ID입니다. 어셈블리는 master 데이터베이스에 로드되어야 합니다.|  
|**assembly_class**|**sysname**|이 모듈을 정의하는 어셈블리 내 클래스의 이름입니다.|  
|**assembly_method**|**sysname**|이 모듈을 정의하는 클래스 내 메서드의 이름입니다. AF(집계 함수)의 경우 NULL입니다.|  
|**execute_as_principal_id**|**int**|EXECUTE AS 서버 보안 주체의 ID입니다.<br /><br /> 기본값은 NULL이며 EXECUTE AS CALLER인 경우에도 NULL입니다.<br /><br /> EXECUTE AS SELF as SELF as \<principal> 경우 지정 된 보안 주체의 ID입니다.<br /><br /> -2 = EXECUTE AS OWNER|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
