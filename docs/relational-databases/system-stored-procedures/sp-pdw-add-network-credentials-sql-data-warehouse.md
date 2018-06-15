---
title: sp_pdw_add_network_credentials (SQL 데이터 웨어하우스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
caps.latest.revision: 10
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 181e40128ec2f8f347039d60409577d25694ea39
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33701434"
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  네트워크 자격 증명 저장 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 는 서버에 연결 합니다. 예를 들어이 저장된 프로시저를 사용 하 여 부여할 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 적절 한 읽기/쓰기 사용 권한과 데이터베이스 백업 및 복원 작업 대상 서버에서 수행 하거나 TDE에 사용 되는 인증서의 백업을 만들 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>인수  
 '*target_server_name*'  
 대상 서버 호스트 이름 또는 IP 주소를 지정합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 이 저장된 프로시저에 전달 된 사용자 이름 및 암호 자격 증명을 사용 하 여이 서버에 액세스 합니다.  
  
 InfiniBand 네트워크를 통해 연결할 대상 서버의 InfiniBand IP 주소를 사용 합니다.  
  
 *target_server_name* nvarchar(337)로 정의 됩니다.  
  
 '*user_name*'  
 대상 서버에 액세스할 수 있는 권한을 지닌 user_name을 지정 합니다. 대상 서버에 대 한 자격 증명이 이미 있는 경우 새 자격 증명으로 업데이트 됩니다.  
  
 *user_name* nvarchar (513)로 정의 됩니다.  
  
 '*암호*ꞌ  
 암호를 지정 *user_name*합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>Permissions  
 필요한 **ALTER SERVER STATE** 권한.  
  
## <a name="error-handling"></a>오류 처리  
 컨트롤 노드 및 모든 계산 노드에 하지 못하면 자격 증명을 추가 하는 경우 오류가 발생 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 저장된 프로시저에 대 한 NetworkService 계정에 네트워크 자격 증명을 추가 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다. SMP의 각 인스턴스를 실행 하는 NetworkService 계정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제어 노드 및 계산 노드에 있습니다. 예를 들어 백업 작업이 실행 될 때 컨트롤 노드와 각 계산 노드가 사용 NetworkService 계정 자격 증명을 읽기 위해 대상 서버에 대 한 쓰기 합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>1. 데이터베이스 백업을 수행 하기 위한 자격 증명 추가  
 다음 예제에서는 10.172.63.255의 IP 주소가 대상 서버를 도메인 사용자 seattle\david에 대 한 사용자 이름 및 암호 자격 증명을 연결 합니다. 사용자 seattle\david에 대상 서버에 대 한 읽기/쓰기 권한이 있습니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 이러한 자격 증명을 저장 하 고 하 고 백업에 대 한 필요에 따라 대상 서버에서 선택한 작업을 복원 하는 데 사용할 됩니다.  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 Backup 명령에서 IP 주소로 서버 이름을 입력 하 필요 합니다.  
  
> [!NOTE]  
>  데이터베이스 백업 InfiniBand 조치를 수행 하려면 백업 서버의 InfiniBand IP 주소를 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_pdw_remove_network_credentials &#40;SQL 데이터 웨어하우스&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

