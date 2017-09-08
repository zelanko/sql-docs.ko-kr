---
title: RECONFIGURE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32039a4077f028a078e9265c6d18f5cbb6187e3f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 구성 된 값을 업데이트 (고 **config_value** 열에는 **sp_configure** 결과 집합)의 구성 옵션을 사용 하 여 변경는 **sp_configure** 시스템 저장된 프로시저입니다. 일부 구성 옵션에는 서버를 중지 및 현재 실행 중인 값을 업데이트 하기 위해 다시 시작 필요, 때문에 RECONFIGURE 업데이트 되지 않는 항상 현재 실행 중인 값 (의 **run_value** 열에는 **sp_configure**  결과 집합) 변경 된 구성 값에 대 한 합니다.    
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>구문    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>인수    
 RECONFIGURE    
 구성 설정에서 서버를 중지하고 다시 시작하지 않아도 될 경우 현재 실행 중인 값이 업데이트되도록 지정합니다. RECONFIGURE는 또한 유효 하지 않은 값에 대 한 새 구성 값 확인 (예를 들어 한 정렬 순서 값에 존재 하지 않는 **syscharsets**) 또는 권장 되지 않는 값입니다. 서버를 중지하고 다시 시작할 필요가 없는 이런 구성 옵션을 사용하는 경우에는 RECONFIGURE를 지정한 후 구성 옵션의 현재 실행 중인 값과 현재 구성된 값이 같아야 합니다.    
    
 WITH OVERRIDE    
 구성 값 (유효 하지 않은 값 또는 권장 되지 않는 값)에 대 한 확인을 사용 하지 않도록 설정 된 **복구 간격** 고급 구성 옵션입니다.    
    
 그러나 일부 심각한 오류는 예방 WITH OVERRIDE 옵션을 사용 하 여 거의 모든 구성 옵션을 다시 구성할 수 있습니다. 예를 들어는 **최소 서버 메모리** 구성 옵션에 지정 된 값 보다 큰 값으로 구성할 수 없는 **최대 서버 메모리** 구성 옵션입니다.
      
## <a name="remarks"></a>주의    
 **sp_configure** 각 구성 옵션에 대 한 문서화 된 유효한 범위를 벗어나는 새 구성 옵션 값을 허용 하지 않습니다.    
    
 명시적 또는 암시적 트랜잭션에서는 RECONFIGURE가 허용되지 않습니다. 여러 개의 옵션을 동시에 다시 구성하는 경우 다시 구성 작업 중 하나가 실패하면 다시 구성 작업이 하나도 적용되지 않습니다.    
    
 리소스 관리자를 다시 구성 하는 경우 다시 구성 옵션을 참조 [ALTER RESOURCE governor&#40; Transact SQL &#41; ](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Permissions    
 RECONFIGURE 권한은 기본적으로 ALTER SETTINGS 권한의 피부여자로 설정됩니다. **sysadmin** 및 **serveradmin** 고정된 서버 역할에이 권한을 암시적으로 보유 합니다.    
    
## <a name="examples"></a>예    
 다음 예에서는 `recovery interval` 구성 옵션에 대한 상한값을 `75`분으로 설정하며 `RECONFIGURE WITH OVERRIDE`를 사용하여 설치합니다. 60분보다 긴 복구 간격은 권장되지 않으며 기본적으로 사용할 수 없습니다. 그러나 `WITH OVERRIDE` 옵션을 지정했기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지정한 값(`90`)이 `recovery interval` 구성 옵션에 유효한 값인지 여부를 확인하지 않습니다.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>관련 항목:    
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  

