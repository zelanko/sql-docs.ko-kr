---
description: sp_pdw_remove_network_credentials (Azure Synapse Analytics)
title: sp_pdw_remove_network_credentials
titleSuffix: Azure Synapse Analytics
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.subservice: design
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.custom: seo-dt-2019
ms.openlocfilehash: 2e69f8446bc7a98b6aa3bae68a169d5e88759ea2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461544"
---
# <a name="sp_pdw_remove_network_credentials-azure-synapse-analytics"></a>sp_pdw_remove_network_credentials (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  네트워크 파일 공유에 액세스 하기 위해에 저장 된 네트워크 자격 증명 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 을 제거 합니다. 예를 들어이 저장 프로시저를 사용 하 여에 대 한 사용 권한을 제거 하 여 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 자체 네트워크 내에 있는 서버에서 백업 및 복원 작업을 수행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>인수  
 '*target_server_name*'  
 대상 서버 호스트 이름 또는 IP 주소를 지정 합니다. 이 서버에 액세스 하기 위한 자격 증명은에서 제거 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . 이는 자신의 팀에서 관리 하는 실제 대상 서버에 대 한 사용 권한을 변경 하거나 제거 하지 않습니다.  
  
 *target_server_name* 은 nvarchar (337)로 정의 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 **ALTER SERVER STATE** 권한이 필요 합니다.  
  
## <a name="error-handling"></a>오류 처리  
 제어 노드와 모든 계산 노드에서 자격 증명 제거에 실패 하는 경우 오류가 발생 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 저장 프로시저는에 대 한 NetworkService 계정에서 네트워크 자격 증명을 제거 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다. NetworkService 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제어 노드와 계산 노드에서 SMP의 각 인스턴스를 실행 합니다. 예를 들어 백업 작업이 실행 될 때 제어 노드와 각 계산 노드는 NetworkService 계정 자격 증명을 사용 하 여 대상 서버에 액세스 합니다.  
  
## <a name="metadata"></a>메타데이터  
 모든 자격 증명을 나열 하 고 자격 증명이 제거 되었는지 확인 하려면 [transact-sql&#41;&#40;sys.dm_pdw_network_credentials ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)을 사용 합니다.  
  
 자격 증명을 추가 하려면 [Azure Synapse Analytics&#41;&#40;sp_pdw_add_network_credentials ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)을 사용 합니다.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. 데이터베이스 백업을 수행 하기 위한 자격 증명 제거  
 다음 예에서는 IP 주소가 10.192.147.63 인 대상 서버에 액세스 하기 위한 사용자 이름 및 암호 자격 증명을 제거 합니다.  
  
```sql  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

