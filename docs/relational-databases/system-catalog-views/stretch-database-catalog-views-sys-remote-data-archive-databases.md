---
title: sys. remote_data_archive_databases (Transact-sql) | Microsoft Docs
description: 스트레치 사용 로컬 데이터베이스의 데이터를 저장 하는 각 원격 데이터베이스에 대해 한 행을 포함 하는 remote_data_archive_databases에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: e192a70c1d8f46b7ad89844a3b38019ab6364cc1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248152"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>Stretch Database 카탈로그 뷰-sys. remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  스트레치 사용 로컬 데이터베이스의 데이터를 저장 하는 각 원격 데이터베이스에 대해 한 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|원격 데이터베이스의 자동 생성 된 로컬 식별자입니다.|  
|**remote_database_name**|**sysname**|원격 데이터베이스의 이름입니다.|  
|**data_source_id**|**int**|원격 서버에 연결 하는 데 사용 되는 데이터 원본입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
