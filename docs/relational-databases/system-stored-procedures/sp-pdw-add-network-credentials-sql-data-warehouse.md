---
title: sp_pdw_add_network_credentials
titleSuffix: Azure SQL Data Warehouse
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 88ddae78b3c866556edbd9e3026e3cb86c747f51
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844406"
---
# <a name="sp_pdw_add_network_credentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  그러면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에 네트워크 자격 증명이 저장 되 고 서버에 연결 됩니다. 예를 들어이 저장 프로시저를 사용 하 여 대상 서버에서 데이터베이스 백업 및 복원 작업을 수행 하거나 TDE에 사용 되는 인증서의 백업을 만들 수 있는 적절 한 읽기/쓰기 권한을 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 제공 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>인수  
 '*target_server_name*'  
 대상 서버 호스트 이름 또는 IP 주소를 지정 합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는이 저장 프로시저에 전달 된 사용자 이름 및 암호 자격 증명을 사용 하 여이 서버에 액세스 합니다.  
  
 InfiniBand 네트워크를 통해 연결 하려면 대상 서버의 InfiniBand IP 주소를 사용 합니다.  
  
 *target_server_name* 은 nvarchar (337)로 정의 됩니다.  
  
 '*user_name*'  
 대상 서버에 액세스할 수 있는 권한이 있는 user_name를 지정 합니다. 대상 서버에 대 한 자격 증명이 이미 있는 경우 새 자격 증명으로 업데이트 됩니다.  
  
 *user_name* 은 nvarchar (513)로 정의 됩니다.  
  
 '*password*ꞌ  
 *User_name*에 대 한 암호를 지정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 **ALTER SERVER STATE** 권한이 필요 합니다.  
  
## <a name="error-handling"></a>오류 처리  
 제어 노드와 모든 계산 노드에서 자격 증명 추가에 성공 하지 못하면 오류가 발생 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 저장 프로시저는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에 대 한 NetworkService 계정에 네트워크 자격 증명을 추가 합니다. NetworkService 계정은 제어 노드와 계산 노드에서 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 인스턴스를 실행 합니다. 예를 들어 백업 작업이 실행 되는 경우 제어 노드와 각 계산 노드는 NetworkService 계정 자격 증명을 사용 하 여 대상 서버에 대 한 읽기 및 쓰기 권한을 얻게 됩니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>1\. 데이터베이스 백업을 수행 하기 위한 자격 증명 추가  
 다음 예에서는 도메인 사용자 seattle\david의 사용자 이름 및 암호 자격 증명을 IP 주소가 10.172.63.255 인 대상 서버에 연결 합니다. 사용자 seattle\david에는 대상 서버에 대 한 읽기/쓰기 권한이 있습니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]은 이러한 자격 증명을 저장 하 고 백업 및 복원 작업을 수행 하는 데 필요한 대로 대상 서버에서 읽고 쓰는 데 사용 합니다.  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 Backup 명령을 사용 하려면 서버 이름을 IP 주소로 입력 해야 합니다.  
  
> [!NOTE]  
>  InfiniBand를 통해 데이터베이스 백업을 수행 하려면 백업 서버의 InfiniBand IP 주소를 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

