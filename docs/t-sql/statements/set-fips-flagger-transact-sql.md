---
title: SET FIPS_FLAGGER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f666a327db29468c5bbd91bf7106d7c6e4f61f64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929043"
---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FIPS 127-2 표준을 준수하는지 확인하도록 지정합니다. ISO 표준을 기반으로 합니다. SQL Server FIPS 규격에 대한 자세한 내용은 [FIPS 140-2-규격 모드에서 SQL Server 2016을 사용하는 방법](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode)을 참조합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>인수  
 **'** *level* **'**  
 모든 데이터베이스 작업이 확인되는 기준인 FIPS 127-2 표준에 대한 요건 충족 수준입니다. 선택한 ISO 표준 수준과 데이터베이스 작업이 충돌하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 경고를 생성합니다.  
  
 *level*은 다음 값 중 하나여야 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|ENTRY|ISO 초급 단계 요건 충족에 대해 표준 검사를 합니다.|  
|FULL|ISO 전체 요건 충족에 대해 표준 검사를 합니다.|  
|INTERMEDIATE|ISO 중간 수준 요건 충족에 대해 표준 검사를 합니다.|  
|OFF|표준 검사를 하지 않습니다.|  
  
## <a name="remarks"></a>Remarks  
 `SET FIPS_FLAGGER`의 설정은 구문 분석 시 설정되며 실행 또는 런타임에는 설정되지 않습니다. 구문 분석 시에 설정되면 코드 실행이 실제로 해당 지점에 이르렀는지에 상관 없이 SET 문이 일괄 처리나 저장 프로시저에 있으면 이 옵션이 적용되고 문이 실행되기 전에 `SET` 문이 적용됩니다. 예를 들어, `SET` 문이 실행 중 도달한 적이 없는 `IF...ELSE` 문 블록에 있어도, `IF...ELSE` 문 블록이 구문 분석되기 때문에 `SET` 문이 적용됩니다.  
  
 `SET FIPS_FLAGGER`이 저장 프로시저에 설정되면 저장 프로시저에서 컨트롤이 반환된 후 `SET FIPS_FLAGGER`의 값이 복원됩니다. 따라서 동적 SQL에 지정한 `SET FIPS_FLAGGER` 문은 동적 SQL 문 다음에 오는 문에는 아무런 영향을 주지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
