---
title: sp_resetsnapshotdeliveryprogress (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc6205eb5487b89db55488bcdf36fbb036595d57
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129646"
---
# <a name="sp_resetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  스냅샷 배달을 다시 시작할 수 있도록 끌어오기 구독에 대한 스냅샷 배달 프로세스를 다시 설정합니다. 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @verbose_level = ] verbose_level`반환 되는 정보의 양을 지정 합니다. *verbose_level*은 **int**이며 기본값은 **1**입니다. 값 **1** 은 **MSsnapshotdeliveryprogress** 테이블에서 필요한 잠금을 얻을 수 없는 경우 오류가 반환 됨을 의미 하 고 **0** 은 반환 된 오류가 없음을 의미 합니다.  
  
`[ @drop_table = ] 'drop_table'`스냅숏의 진행에 대 한 정보를 포함 하는 테이블을 삭제 하거나 잘라낼 지 여부입니다. *drop_table* 은 **nvarchar (5)** 이며 기본값은 **FALSE**입니다. FALSE는 테이블을 잘라내며 TRUE는 테이블을 삭제합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **Sp_resetsnapshotdeliveryprogress** **MSsnapshotdeliveryprogress** 테이블의 모든 행을 제거 합니다. 결과적으로 스냅샷 배달 프로세스의 이전 과정에 의해 구독 데이터베이스에 남겨진 모든 메타데이터도 함께 제거됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_resetsnapshotdeliveryprogress**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
