---
title: SET FIPS_FLAGGER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c28fd5419aec8bf15745150288b6878fd65ac1f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FIPS 127-2 표준을 준수하는지 확인하도록 지정합니다. ISO 표준을 기반으로 합니다. SQL Server FIPS 규격에 대 한 정보를 참조 하십시오. [FIPS 140-2-규격 모드에서 SQL Server 2016을 사용 하는 방법을](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode)합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>인수  
 **'** *수준* **'**  
 모든 데이터베이스 작업이 확인되는 기준인 FIPS 127-2 표준에 대한 요건 충족 수준입니다. 선택한 ISO 표준 수준의 데이터베이스 작업이 충돌 하는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경고를 생성 합니다.  
  
 *수준* 다음 값 중 하나 여야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|ENTRY|ISO 초급 단계 요건 충족에 대해 표준 검사를 합니다.|  
|FULL|ISO 전체 요건 충족에 대해 표준 검사를 합니다.|  
|INTERMEDIATE|ISO 중간 수준 요건 충족에 대해 표준 검사를 합니다.|  
|OFF|표준 검사를 하지 않습니다.|  
  
## <a name="remarks"></a>주의  
 설정 `SET FIPS_FLAGGER` execute을 누르지 구문 분석 시 설정 되었거나 실행 시간입니다. 구문 분석 시에 설정 하는 일괄 처리 또는 저장된 프로시저에 SET 문이 있으면이 옵션이 적용 코드 실행에 해당 지점을 실제로 도달 했는지 여부에 관계 없이 의미 및 `SET` 문은 모든 문이 실행 되기 전에 적용 됩니다. 예를 들어 경우라도는 `SET` 문이 `IF...ELSE` 실행 중 도달한 적이 없는 문 블록의 `SET` 때문에 여전히 문에 적용 됩니다는 `IF...ELSE` 문 블록이 구문 분석 합니다.  
  
 경우 `SET FIPS_FLAGGER` 는 저장된 프로시저의 값에 설정 되어 `SET FIPS_FLAGGER` 저장된 프로시저에서 컨트롤이 반환 된 후 복원 됩니다. 따라서 한 `SET FIPS_FLAGGER` 동적 SQL에서 지정 된 문이 동적 SQL 문 다음에 오는 문에 아무 영향이 없습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

