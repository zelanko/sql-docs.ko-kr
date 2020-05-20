---
title: sp_prepexecrpc (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 26f298a102c69c8bc75721db531275379080005a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830983"
---
# <a name="sp_prepexecrpc-transact-sql"></a>sp_prepexecrpc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  RPC 식별자를 사용하여 지정된 매개 변수가 있는 저장 프로시저 호출을 준비 및 실행합니다. sp_prepexecrpc은 TDS (tabular data stream) 패킷에서 ID = 14에 의해 호출 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>인수  
 *처리*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성하는 준비된 핸들 식별자입니다. *handle* 은 **int** 반환 값을 포함 하는 필수 매개 변수입니다.  
  
 *RPCCall*  
 ODBC 정식 구문을 사용하여 저장 프로시저를 정의합니다. *Rpccall* 은 **ntext** 문자열 입력 값을 호출 하는 필수 매개 변수입니다.  
  
 *bound_param*  
 추가 매개 변수의 선택적 사용을 나타냅니다. *bound_param* 는 모든 데이터 형식의 입력 값을 호출 하 여 사용 중인 추가 매개 변수를 지정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
