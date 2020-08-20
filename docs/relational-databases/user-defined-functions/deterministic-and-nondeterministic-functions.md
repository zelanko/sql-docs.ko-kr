---
description: 결정적 함수 및 비결정적 함수
title: 결정적 함수 및 비결정적 함수 | Microsoft 문서
ms.custom: ''
ms.date: 08/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2665ab9b5a30209a123056664921334ce3c8367
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485312"
---
# <a name="deterministic-and-nondeterministic-functions"></a>결정적 함수 및 비결정적 함수
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  결정적 함수는 데이터베이스의 상태가 같을 경우 특정 입력 값 집합으로 호출될 때마다 항상 동일한 결과를 반환합니다. 비결정적 함수는 액세스하는 데이터베이스의 상태가 동일하게 유지되더라도 특정 입력 값 집합으로 호출될 때마다 다른 결과를 반환할 수 있습니다. 예를 들어 AVG 함수는 항상 위에서 설명된 조건에 따라 동일한 결과를 반환하지만 현재 날짜/시간 값을 반환하는 GETDATE 함수는 항상 다른 결과를 반환합니다.  
  
 사용자 정의 함수에는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 함수를 호출하는 계산 열의 인덱스를 통해 또는 함수를 참조하는 인덱싱된 뷰를 통해 함수의 결과를 인덱싱할 수 있는지 여부를 결정하는 여러 가지 속성이 있습니다. 함수의 결정성이 이러한 속성 중 하나입니다. 예를 들어 뷰에서 비결정적 함수를 참조하면 뷰에 클러스터형 인덱스를 만들 수 없습니다. 결정성을 비롯한 함수 속성에 대한 자세한 내용은 [사용자 정의 함수](../../relational-databases/user-defined-functions/user-defined-functions.md)를 참조하세요.  
  
 이 항목에서는 기본 제공 시스템 함수의 결정성을 확인하고 확장 저장 프로시저 호출이 포함될 경우 사용자 정의 함수의 결정적 속성에 주는 효과를 설명합니다.  
  
## <a name="built-in-function-determinism"></a>기본 제공 함수 결정성  
 기본 제공 함수의 결정성에는 영향을 줄 수 없습니다. 각 기본 제공 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 함수를 구현하는 방식에 따라 결정적이거나 비결정적입니다. 예를 들어 쿼리에서 ORDER BY 절을 지정하는 경우 해당 쿼리에서 사용된 함수의 결정성이 변경되지 않습니다.  
  
 [FORMAT](../../t-sql/functions/format-transact-sql.md)을 제외한 모든 기본 제공 문자열 함수는 결정적입니다. 이러한 함수 목록은 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)를 참조하세요.  
  
 문자열 함수 이외의 기본 제공 함수 범주에 속하는 다음 기본 제공 함수는 항상 결정적입니다.  
  
:::row:::
    :::column:::
        ABS
    :::column-end:::
    :::column:::
        DATEDIFF
    :::column-end:::
    :::column:::
        POWER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ACOS
    :::column-end:::
    :::column:::
        DAY
    :::column-end:::
    :::column:::
        RADIANS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ASIN
    :::column-end:::
    :::column:::
        DEGREES
    :::column-end:::
    :::column:::
        ROUND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATAN
    :::column-end:::
    :::column:::
        EXP
    :::column-end:::
    :::column:::
        SIGN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATN2
    :::column-end:::
    :::column:::
        FLOOR
    :::column-end:::
    :::column:::
        SIN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CEILING
    :::column-end:::
    :::column:::
        ISNULL
    :::column-end:::
    :::column:::
        SQUARE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COALESCE
    :::column-end:::
    :::column:::
        ISNUMERIC
    :::column-end:::
    :::column:::
        SQRT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COS
    :::column-end:::
    :::column:::
        LOG
    :::column-end:::
    :::column:::
        TAN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COT
    :::column-end:::
    :::column:::
        LOG10
    :::column-end:::
    :::column:::
        YEAR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATALENGTH
    :::column-end:::
    :::column:::
        MONTH
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATEADD
    :::column-end:::
    :::column:::
        NULLIF
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
 다음 함수는 항상 결정적이지는 않지만 함수를 결정적인 방식으로 지정하면 인덱싱된 뷰 또는 계산 열의 인덱스에서 사용할 수 있습니다.  
  
|함수|주석|  
|--------------|--------------|  
|모든 집계 함수|모든 집계 함수는 OVER 및 ORDER BY 절로 지정되지 않는 한 결정적입니다. 이러한 함수 목록은 [집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)를 참조하세요.|  
|CAST|**datetime**, **smalldatetime**또는 **sql_variant**와 함께 사용하지 않을 경우 결정적입니다.|  
|CONVERT|다음과 같은 경우를 제외하고 결정적입니다.<br /><br /> <br /><br /> 원본 유형이 **sql_variant**인 경우<br /><br /> 대상 유형이 **sql_variant** 이고 해당 원본 유형이 비결정적인 경우<br /><br /> 원본 또는 대상 유형이 **datetime** 이거나 **smalldatetime**이고 다른 원본 또는 대상 유형이 문자열이며 비결정적 스타일을 지정한 경우 결정적이려면 스타일 매개 변수가 상수여야 합니다. 또한 100 이하의 스타일(스타일 20 및 21 제외)은 비결정적입니다. 100보다 큰 스타일(스타일 106, 107, 109, 113 제외)은 결정적입니다.|  
|CHECKSUM|CHECKSUM(*)을 제외하고 모두 결정적입니다.|  
|ISDATE|CONVERT 함수와 함께 사용하고 CONVERT 스타일 매개 변수가 지정되고 스타일이 0, 100, 9 또는 109가 아닌 경우에만 결정적입니다.|  
|RAND|RAND는 *seed* 매개 변수가 지정된 경우에만 결정적입니다.|  
  
 구성, 커서, 메타데이터, 보안 및 시스템 통계 함수는 모두 비결정적입니다. 이러한 함수 목록은 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md), [커서 함수&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md), [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md), [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md) 및 [시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)를 참조하세요.  
  
 그 밖의 범주에 속하는 다음 기본 제공 함수는 항상 비결정적입니다.  
  
:::row:::
    :::column:::
        @@CONNECTIONS
    :::column-end:::
    :::column:::
        GETDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@CPU_BUSY
    :::column-end:::
    :::column:::
        GETUTCDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@DBTS
    :::column-end:::
    :::column:::
        GET_TRANSMISSION_STATUS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IDLE
    :::column-end:::
    :::column:::
        LAG
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IO_BUSY
    :::column-end:::
    :::column:::
        LAST_VALUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@MAX_CONNECTIONS
    :::column-end:::
    :::column:::
        LEAD
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_RECEIVED
    :::column-end:::
    :::column:::
        MIN_ACTIVE_ROWVERSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_SENT
    :::column-end:::
    :::column:::
        NEWID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACKET_ERRORS
    :::column-end:::
    :::column:::
        NEWSEQUENTIALID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TIMETICKS
    :::column-end:::
    :::column:::
        NEXT VALUE FOR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_ERRORS
    :::column-end:::
    :::column:::
        NTILE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_READ
    :::column-end:::
    :::column:::
        PARSENAME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_WRITE
    :::column-end:::
    :::column:::
        PERCENTILE_CONT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        AT TIME ZONE
    :::column-end:::
    :::column:::
        PERCENTILE_DISC
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CUME_DIST
    :::column-end:::
    :::column:::
        PERCENT_RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CURRENT_TIMESTAMP
    :::column-end:::
    :::column:::
        RAND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DENSE_RANK
    :::column-end:::
    :::column:::
        RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        FIRST_VALUE
    :::column-end:::
    :::column:::
        ROW_NUMBER
    :::column-end:::
:::row-end:::   
:::row:::
    :::column:::
        FORMAT
    :::column-end:::
    :::column:::
        TEXTPTR
    :::column-end:::
:::row-end:::
 
## <a name="calling-extended-stored-procedures-from-functions"></a>함수에서 확장 저장 프로시저 호출  
 확장 저장 프로시저는 데이터베이스에 의도하지 않은 영향을 줄 수 있기 때문에 확장 저장 프로시저를 호출하는 함수는 비결정적입니다. 의도하지 않은 영향으로는 테이블 업데이트와 같은 데이터베이스의 전역 상태 변경이나 파일 수정 또는 전자 메일 메시지 보내기와 같은 파일 또는 네트워크 등의 외부 리소스 변경이 있습니다. 사용자 정의 함수에서 확장 저장 프로시저를 실행할 때 일관된 결과 집합이 반환되는 것에 의존하지 마세요. 데이터베이스에 의도하지 않은 영향을 주는 사용자 정의 함수는 권장되지 않습니다.  
  
 함수 내부에서 확장 저장 프로시저를 호출하면 확장 저장 프로시저가 클라이언트에 결과 집합을 반환할 수 없습니다. 클라이언트에 결과 집합을 반환하는 모든 개방형 데이터 서비스 API는 FAIL 반환 코드를 포함합니다.  
  
 확장 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 다시 연결할 수 있지만 확장 저장 프로시저를 호출한 원래 함수와 동일한 트랜잭션을 조인할 수는 없습니다.  
  
 일괄 처리 또는 저장 프로시저에서 호출하는 경우와 마찬가지로 확장 저장 프로시저는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 가 실행되고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 계정 컨텍스트에서 실행됩니다. 확장 저장 프로시저의 소유자는 다른 사용자에게 프로시저를 실행하는 권한을 부여할 때 이 보안 컨텍스트의 권한을 고려해야 합니다.  
  
  
