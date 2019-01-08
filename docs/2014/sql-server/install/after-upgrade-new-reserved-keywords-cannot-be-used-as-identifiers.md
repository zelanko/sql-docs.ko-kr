---
title: 업그레이드 후 새 예약된 키워드 식별자로 사용할 수 없습니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8db9bcef48b28594187aab34fb0049689d907a47
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376235"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>업그레이드 후 새 예약 키워드는 식별자로 사용할 수 없습니다.
  업그레이드 관리자가 예약 키워드 사용을 감지했습니다. 예약 키워드는 구분 기호로 구분하지 않는 한 식별자나 개체 이름으로 사용될 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 데이터베이스 엔진  
  
## <a name="description"></a>Description  
 호환성 수준 90 이하에서는 다음 단어가 예약 키워드가 아니며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에서 식별자나 개체 이름으로 사용될 수 없습니다. 호환성 수준 100에서는 다음 단어가 완전 예약 키워드며 식별자나 개체 이름으로 사용될 수 없습니다.  
  
-   EXTERNAL  
  
-   MERGE  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>수정 동작  
 개체의 이름을 바꾸는 것이 좋습니다. 업그레이드하기 전에 개체의 이름을 바꿀 수 없으면 이름을 바꿀 수 있을 때까지 다음 방법 중 하나를 사용합니다.  
  
-   90 이하의 데이터베이스 호환성 수준 설정을 유지합니다.  
  
-   구분 기호로 구분 식별자를 사용하여 개체를 참조합니다. 예를 들어, 다음 문 `CREATE TABLE [MERGE] ([MERGE] int);` 대괄호를 사용 하 여 개체 이름 MERGE를 구분 합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 [예약 된 키워드 &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE&#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [구분된 식별자 (데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
