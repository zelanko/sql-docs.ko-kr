---
title: sys. fulltext_document_types (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e60f977c220d14680499ca12a4884e912587b7b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133848"
---
# <a name="sysfulltext_document_types-transact-sql"></a>sys.fulltext_document_types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 인덱싱 작업에 사용할 수 있는 각 문서 유형에 대해 행을 반환합니다. 각 행은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 등록되는 IFilter 인터페이스를 나타냅니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|지원되는 문서 유형의 파일 확장명입니다.<br /><br /> 이 값은 **varbinary (max)** 또는 **image**유형의 열에 대 한 전체 텍스트 인덱싱을 수행 하는 동안 사용할 필터를 식별 하는 데 사용할 수 있습니다.|  
|**class_id**|**uniqueidentifier**|파일 확장명을 지원하는 IFilter 클래스의 GUID입니다.|  
|**경로**|**nvarchar(260)**|IFilter DLL의 경로입니다. 이 경로는 **serveradmin** 고정 서버 역할의 멤버만 볼 수 있습니다.|  
|**버전**|**sysname**|IFilter DLL의 버전입니다.|  
|**manufacturer**|**sysname**|IFilter 제조업체의 이름입니다.<br /><br /> 참고: 제조업체의 문서만에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]지원 됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
