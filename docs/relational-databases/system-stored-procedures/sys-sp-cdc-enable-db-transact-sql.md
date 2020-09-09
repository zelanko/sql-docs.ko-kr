---
description: sys.sp_cdc_enable_db(Transact-SQL)
title: sys. sp_cdc_enable_db (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c40d3904737c7740c3658eda12e2f9c9df340b0a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534754"
---
# <a name="syssp_cdc_enable_db-transact-sql"></a>sys.sp_cdc_enable_db(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에 대해 변경 데이터 캡처를 활성화합니다. 데이터베이스의 테이블에서 변경 데이터 캡처를 사용할 수 있도록 설정하려면 먼저 해당 데이터베이스에 대해 이 프로시저를 실행해야 합니다. 변경 데이터 캡처는 설정된 테이블에 적용된 삽입, 업데이트 및 삭제 작업을 기록하고 변경 내용의 세부 정보를 쉽게 사용할 수 있는 관계형 형식으로 만듭니다. 추적된 원본 테이블의 열 구조를 미러하는 열 정보가 대상 환경에 변경 내용을 적용하는 데 필요한 메타데이터와 함께 수정된 행에 대해 캡처됩니다.  
  
> [!IMPORTANT]
>  변경 데이터 캡처는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 [시스템 데이터베이스](../../relational-databases/databases/system-databases.md) 또는 배포 데이터베이스에서는 변경 데이터 캡처를 사용 하도록 설정할 수 없습니다.  
  
 sys.sp_cdc_enable_db는 메타데이터 테이블 및 DDL 트리거를 포함하여 데이터베이스 차원 범위의 변경 데이터 캡처 개체를 만듭니다. 또한 cdc 스키마와 cdc 데이터베이스 사용자를 만들고, 데이터베이스 항목에 대 한 is_cdc_enabled 열을 [sys. 데이터베이스](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에서 1로 설정 합니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 변경 데이터 캡처를 활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_cdc_disable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
