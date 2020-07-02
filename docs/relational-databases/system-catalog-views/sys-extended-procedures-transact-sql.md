---
title: sys. extended_procedures (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- extended_procedures
- sys.extended_procedures
- sys.extended_procedures_TSQL
- extended_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.extended_procedures catalog view
ms.assetid: 310e0f87-0044-4fdf-bd12-51a723a74ce6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bcc9d30d457e9042f2a667a7a71f846f6e07eb63
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738762"
---
# <a name="sysextended_procedures-transact-sql"></a>sys.extended_procedures(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  확장 저장 프로시저 인 각 개체에 대 한 행을 포함 합니다. 여기에는 **sys. type** = X가 있습니다. 확장 저장 프로시저는 **master** 데이터베이스에 설치 되기 때문에 해당 데이터베이스 컨텍스트에서만 볼 수 있습니다. 다른 데이터베이스 컨텍스트의 **sys. extended_procedures** 뷰에서 선택 하면 빈 결과 집합이 반환 됩니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**dll_name**|**nvarchar(260)**|이 확장 저장 프로시저에 대한 DLL의 경로를 포함한 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
