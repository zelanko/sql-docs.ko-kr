---
title: xp_sscanf (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_sscanf_TSQL
- xp_sscanf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 315612c728140f575ed78e94f5643e795951a9fe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="xpsscanf-transact-sql"></a>xp_sscanf(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  문자열에서 각 포맷 인수가 지정한 인수 위치로 데이터를 읽습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>인수  
 **문자열**  
 인수 값을 읽을 문자열입니다.  
  
 OUTPUT  
 를 지정 하는 경우의 값을 넣습니다 *인수* 에서 출력 매개 변수입니다.  
  
 *format*  
 서식이 지정 된 문자열은 C 언어에 지원 되는 기능 비슷합니다 **sscanf** 함수입니다. 현재 % 포맷 인수만 지원됩니다.  
  
 *argument*  
 이 **varchar** 변수가 해당 값으로 설정 *형식* 인수입니다.  
  
 *n*  
 최대 50개의 인수를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **xp_sscanf** 다음 메시지를 반환 합니다.  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `xp_sscanf`를 사용하여 원본 문자열 포맷의 해당 위치를 기반으로 한 원본 문자열에서 두 값을 추출합니다.  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [일반 확장 저장된 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sprintf &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
