---
title: cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 245d11af0b97bf668b11c1872affae1cb188b2b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cursor-transact-sql"></a>SET(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

커서에 대한 참조가 들어 있는 변수 또는 저장 프로시저 OUTPUT 매개 변수의 데이터 형식입니다.
  
## <a name="remarks"></a>Remarks  
**cursor** 데이터 형식을 가진 변수와 매개 변수를 참조할 수 있는 작업은 다음과 같습니다.
-   DECLARE *@local_variable* 및 SET *@local_variable* 문.  
-   OPEN, FETCH, CLOSE 및 DEALLOCATE 커서 문  
-   저장 프로시저 출력 매개 변수  
-   CURSOR_STATUS 함수  
-   **sp_cursor_list**, **sp_describe_cursor**, **sp_describe_cursor_tables** 및 **sp_describe_cursor_columns** 시스템 저장 프로시저.  
  
**sp_cursor_list** 및 **sp_describe_cursor**의 **cursor_name** 출력 열은 커서 변수의 이름을 반환합니다.
  
**cursor** 데이터 형식으로 만들어진 모든 변수는 Null을 허용합니다.
  
**cursor** 데이터 형식은 CREATE TABLE 문에 있는 열에서 사용할 수 없습니다.
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
