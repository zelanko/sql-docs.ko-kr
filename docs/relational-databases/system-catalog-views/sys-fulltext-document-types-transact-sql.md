---
title: sys.fulltext_document_types (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 12ffa574d72bd2ee901015f5714eeb228524579c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33179479"
---
# <a name="sysfulltextdocumenttypes-transact-sql"></a>sys.fulltext_document_types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 인덱싱 작업에 사용할 수 있는 각 문서 유형에 대해 행을 반환합니다. 각 행은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 등록되는 IFilter 인터페이스를 나타냅니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|지원되는 문서 유형의 파일 확장명입니다.<br /><br /> 형식의 열에 전체 텍스트 인덱싱 동안 사용 되는 필터를 식별 하려면이 값을 사용할 수 있습니다 **varbinary (max)** 또는 **이미지**합니다.|  
|**class_id**|**uniqueidentifier**|파일 확장명을 지원하는 IFilter 클래스의 GUID입니다.|  
|**path**|**nvarchar(260)**|IFilter DLL의 경로입니다. 이 경로는 **serveradmin** 고정 서버 역할의 멤버만 볼 수 있습니다.|  
|**version**|**sysname**|IFilter DLL의 버전입니다.|  
|**manufacturer**|**sysname**|IFilter 제조업체의 이름입니다.<br /><br /> 참고:으로 제조업체 인 문서만 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서 지원 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
