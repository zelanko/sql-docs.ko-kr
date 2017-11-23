---
title: sys.remote_data_archive_databases (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cd9f8e2841bff4fe1ab1bbc61a8ea100207e205e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stretch-database-catalog-views---sysremotedataarchivedatabases"></a>스트레치 데이터베이스 카탈로그 뷰-sys.remote_data_archive_databases
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스트레치가 활성화 된 로컬 데이터베이스에서 데이터를 저장 하는 각 원격 데이터베이스에 대해 한 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|자동 생성 된 로컬 데이터베이스의 식별자는 원격 합니다.|  
|**remote_database_name**|**sysname**|원격 데이터베이스의 이름입니다.|  
|**data_source_id**|**int**|원격 서버에 연결 하는 데 사용 되는 데이터 원본|  
  
## <a name="see-also"></a>관련 항목:  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
