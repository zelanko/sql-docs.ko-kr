---
title: sys. 파일 그룹 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filegroups_TSQL
- filegroups
- sys.filegroups
- filegroups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filegroups catalog view
ms.assetid: 9e851f72-1f8e-4515-a25d-152ebc12ed56
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 313c0b80a1bf1d2a094760198053e26426e99c36
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005177"
---
# <a name="sysfilegroups-transact-sql"></a>sys.filegroups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  파일 그룹인 각 데이터 공간당 하나의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<상속 된 열>**|--|이 뷰가 상속 하는 열 목록은 [data_spaces &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)을 참조 하십시오.|  
|**filegroup_guid**|**uniqueidentifier**|파일 그룹의 GUID입니다.<br /><br /> NULL = PRIMARY 파일 그룹|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 값은 NULL입니다.|  
|**is_read_only**|**bit**|1 = 읽기 전용 파일 그룹입니다.<br /><br /> 0 = 읽기/쓰기 파일 그룹입니다.|  
|**is_autogrow_all_files**|**bit**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> 1 = 파일 그룹의 파일이 자동 증가 임계값을 충족 하면 파일 그룹의 모든 파일이 증가 합니다.<br /><br /> 0 = 파일 그룹의 파일이 자동 증가 임계값을 충족 하면 해당 파일만 증가 합니다. 기본값입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [데이터 공간 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
