---
title: RECONFIGURE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab210494680fdff64289b90e18cdcea3b39058a9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33061630"
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **sp_configure** 시스템 저장 프로시저로 변경한 구성 옵션의 현재 구성 값(**sp_configure** 결과 집합의 **sp_configure** 열)을 업데이트합니다. 구성 옵션에 따라 현재 실행 중인 값을 업데이트하려면 서버를 중지하고 다시 시작해야 하기 때문에 RECONFIGURE에서는 변경된 구성 값에 대해 현재 실행 중인 값(**sp_configure** 결과 집합의 **sp_configure** 열)을 항상 업데이트하지는 않습니다.    
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>구문    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>인수    
 RECONFIGURE    
 구성 설정에서 서버를 중지하고 다시 시작하지 않아도 될 경우 현재 실행 중인 값이 업데이트되도록 지정합니다. 또한 RECONFIGURE는 새 구성 값에서 유효하지 않은 값(예: **syscharsets**에 없는 정렬 순서 값)이나 권장되지 않는 값을 확인합니다. 서버를 중지하고 다시 시작할 필요가 없는 이런 구성 옵션을 사용하는 경우에는 RECONFIGURE를 지정한 후 구성 옵션의 현재 실행 중인 값과 현재 구성된 값이 같아야 합니다.    
    
 WITH OVERRIDE    
 **recovery interval** 고급 구성 옵션에 대해 유효하지 않은 값 또는 권장되지 않는 값의 구성 값 확인을 해제합니다.    
    
 거의 모든 구성 옵션은 WITH OVERRIDE 옵션을 사용하여 재구성할 수 있지만 일부 치명적인 오류는 여전히 방지됩니다. 예를 들어 **min server memory** 구성 옵션은 **max server memory** 구성 옵션에서 지정한 값보다 큰 값으로 구성할 수 있습니다.
      
## <a name="remarks"></a>Remarks    
 **sp_configure**에서는 각 구성 옵션에 대해 설명한 유효한 범위를 벗어난 새 구성 옵션 값을 허용하지 않습니다.    
    
 명시적 또는 암시적 트랜잭션에서는 RECONFIGURE가 허용되지 않습니다. 여러 개의 옵션을 동시에 다시 구성하는 경우 다시 구성 작업 중 하나가 실패하면 다시 구성 작업이 하나도 적용되지 않습니다.    
    
 리소스 관리자(resource governor)를 재구성하는 경우 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)의 RECONFIGURE 옵션을 참조하세요.    
    
## <a name="permissions"></a>사용 권한    
 RECONFIGURE 권한은 기본적으로 ALTER SETTINGS 권한의 피부여자로 설정됩니다. **sysadmin** 및 **serveradmin** 고정 서버 역할이 암시적으로 이 권한을 보유합니다.    
    
## <a name="examples"></a>예    
 다음 예에서는 `recovery interval` 구성 옵션에 대한 상한값을 `75`분으로 설정하며 `RECONFIGURE WITH OVERRIDE`를 사용하여 설치합니다. 60분보다 긴 복구 간격은 권장되지 않으며 기본적으로 사용할 수 없습니다. 그러나 `WITH OVERRIDE` 옵션을 지정했기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정한 값(`90`)이 `recovery interval` 구성 옵션에 유효한 값인지 여부를 확인하지 않습니다.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>참고 항목    
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
