---
title: transform noise words 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5ddad15af74e45313d3e71b059fae36d166560
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808694"
---
# <a name="transform-noise-words-server-configuration-option"></a>transform noise words 서버 구성 옵션
  사용 된 `transform noise words` 오류 메시지를 표시 하지 않으려면 서버 구성 옵션 경우 의미 없는 단어, 즉 [중지 단어](../../relational-databases/search/full-text-search.md), 0 개 행을 반환 하는 전체 텍스트 쿼리에 대 한 부울 연산이 발생할. 이 옵션은 부울 연산 또는 NEAR 연산에 의미 없는 단어가 들어 있는 CONTAINS 조건자를 사용하는 전체 텍스트 쿼리에 유용합니다. 다음 표에서는 이 옵션에 사용할 수 있는 값을 설명합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|의미 없는 단어(또는 중지 단어)가 변환되지 않습니다. 전체 텍스트 쿼리에 의미 없는 단어가 들어 있으면 쿼리에서 행이 반환되지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 경고가 발생합니다. 이것이 기본 동작입니다.<br /><br /> 경고는 런타임 경고는 참고 합니다. 쿼리에 있는 전체 텍스트 절이 실행되지 않으면 경고가 발생하지 않습니다. 로컬 쿼리의 경우 여러 개의 전체 텍스트 쿼리 절이 있어도 경고는 하나만 발생합니다. 원격 쿼리의 경우 연결된 서버에서 오류를 릴레이하지 않을 수 있으므로 경고가 발생하지 않을 수도 있습니다.|  
|1|의미 없는 단어(또는 중지 단어)가 변환되지 않습니다. 이러한 단어는 무시되고 쿼리의 나머지가 평가됩니다.<br /><br /> 근접 단어에서 의미 없는 단어가 지정된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 의미 없는 단어를 제거합니다. 예를 들어 `is` 에서 의미 없는 단어 `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`가 제거되고 검색 쿼리가 `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`로 변환됩니다. `CONTAINS(<column_name>, 'NEAR(hello,is)')` 는 유효한 검색 단어가 하나만 있으므로 간단히 `CONTAINS(<column_name>, hello)` 로 변환됩니다.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>의미 없는 단어 변환 설정의 효과  
 이 섹션에서는 `transform noise words`의 설정별로 의미 없는 단어 "`the`"가 들어 있는 쿼리의 동작을 보여 줍니다.  예제 전체 텍스트 쿼리 문자열은 다음 데이터가 포함된 테이블 행에 대해 실행되는 것으로 가정합니다. `[1, "The black cat"]`.  
  
> [!NOTE]  
>  이러한 모든 시나리오에서 의미 없는 단어 경고가 생성될 수 있습니다.  
  
-   의미 없는 단어를 0으로 설정한 경우:  
  
    |쿼리 문자열|결과|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|결과가 없습니다. 이 동작은 "`the`" AND "`cat`"의 경우에도 동일합니다.|  
    |"`cat`" NEAR "`the`"|결과가 없습니다. 이 동작은 "`the`" NEAR "`cat`"의 경우에도 동일합니다.|  
    |"`the`" AND NOT "`black`"|결과 없음|  
    |"`black`" AND NOT "`the`"|결과 없음|  
  
-   의미 없는 단어를 1로 설정한 경우:  
  
    |쿼리 문자열|결과|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|ID가 1인 행|  
    |"`cat`" NEAR "`the`"|ID가 1인 행|  
    |"`the`" AND NOT "`black`"|결과 없음|  
    |"`black`" AND NOT "`the`"|ID가 1인 행|  
  
## <a name="example"></a>예제  
 다음 예에서는 `transform noise words`를 `1`로 설정합니다.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [CONTAINS&#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
