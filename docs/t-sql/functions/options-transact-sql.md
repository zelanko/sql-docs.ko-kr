---
title: '@@OPTIONS (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 9480ffeffa83650b5cf44ad51547c36d5563b13b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40options-transact-sql"></a>& #x 40; & #x 40; 옵션 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 SET 옵션에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 옵션의 사용에서 가져올 수 있습니다는 **설정** 명령 또는 **sp_configure 사용자 옵션** 값입니다. 세션 값을 사용 하 여 구성 된 **설정** 명령 재정의 **sp_configure** 옵션입니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]와 같은 많은 도구가 집합 옵션을 자동으로 구성합니다. 각 사용자에 게는 @@OPTIONS 구성을 나타내는 함수입니다.  
  
 SET 문을 사용하여 특정 사용자 세션에 대한 언어와 쿼리 처리 옵션을 변경할 수 있습니다. **@@OPTIONS ** 옵션을 ON으로 설정 되는 검색할 수 있습니다 또는 OFF입니다.  
  
 **@@OPTIONS ** 함수 기본 10 진수 정수로 변환할 옵션의 비트맵을 반환 합니다. 비트 설정은 항목의 테이블에 설명 된 위치에 저장 됩니다 [user options 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)합니다.  
  
 디코딩하는 **@@OPTIONS ** 반환한 정수를 변환, 값 **@@OPTIONS ** 를 이진으로 다음의 테이블에 값을 조회 하 고 [user options 서버 구성 구성 옵션](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)합니다. 예를 들어 경우 `SELECT @@OPTIONS;` 값을 반환 `5496`, Windows 프로그래머 계산기를 사용 하 여 (**calc.exe**) 10 진수 변환 하려면 `5496` 이진입니다. 결과는 `1010101111000`입니다. 가장 오른쪽 문자 (이진 1, 2 및 4)는 0으로, 테이블의 처음 세 항목은 해제 하는지 여부를 나타내는입니다. 테이블을 참조 하는, 표시 하는 것은 **DISABLE_DEF_CNST_CHK** 및 **IMPLICIT_TRANSACTIONS**, 및 **CURSOR_CLOSE_ON_COMMIT**합니다. 다음 항목 (**ANSI_WARNINGS** 에 `1000` 위치)에 있습니다. 비트맵을 하지만 작업 왼쪽을 계속 하 및 옵션의 목록에서 아래쪽 합니다. 맨 왼쪽 옵션은 0, 형식 변환으로 잘립니다. 비트맵 `1010101111000`은 실제로 `001010101111000`으로 모두 15개의 옵션을 나타냅니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>1. 변경이 동작에 미치는 영향 설명  
 다음 예제에서는 두 개의 서로 다른 설정으로 연결 동작의 차이 **CONCAT_NULL_YIELDS_NULL** 옵션입니다.  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>2. 클라이언트 NOCOUNT 설정 테스트  
 다음 예제에서는 `NOCOUNT``ON` 다음의 값을 테스트 하 고 `@@OPTIONS`합니다. `NOCOUNT``ON` 옵션 세션의 모든 문에 대해 요청 하는 클라이언트를 다시 보내는 것에 영향을 받는 행 수에 대 한 메시지를 방지 합니다. `@@OPTIONS`의 값은 `512`(0x0200)로 설정되며 이는 NOCOUNT 옵션을 나타냅니다. 이 예에서는 클라이언트에서 NOCOUNT 옵션을 사용할 수 있는지 테스트합니다. 이러한 방법은 예를 들어 클라이언트에서 성능 차이를 추적하는 데 도움이 될 수 있습니다.  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [사용자 옵션 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  

