---
title: 업그레이드 후 새롭게 예약 된 키워드 식별자로 사용할 수 없는 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 177c36aaeca8e6cc9d84aae21e1f99fe0bb96867
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181958"
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
  
-   구분 기호로 구분 식별자를 사용하여 개체를 참조합니다. 예를 들어 문을 `CREATE TABLE [MERGE] ([MERGE] int);` 대괄호를 사용 하 여 개체 이름 MERGE를 구분 합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 [예약 된 키워드 &#40;Transact SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE&#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [구분된 식별자 (데이터베이스 엔진)](http://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
