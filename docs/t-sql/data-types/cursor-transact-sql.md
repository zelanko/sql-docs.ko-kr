---
title: "커서 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b0b96a3bc147f51102fa10f2dff96b7f1761759
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-transact-sql"></a>SET(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

커서에 대한 참조가 들어 있는 변수 또는 저장 프로시저 OUTPUT 매개 변수의 데이터 형식입니다.
  
## <a name="remarks"></a>주의  
변수 및 매개 변수를 참조할 수 있는 작업을 **커서** 데이터 형식:
-   DECLARE  *@local_variable*  설정 및  *@local_variable*  문.  
-   OPEN, FETCH, CLOSE 및 DEALLOCATE 커서 문  
-   저장 프로시저 출력 매개 변수  
-   CURSOR_STATUS 함수  
-   **sp_cursor_list**, **sp_describe_cursor**, **sp_describe_cursor_tables**, 및 **sp_describe_cursor_columns** 시스템 저장 프로시저입니다.  
  
**cursor_name** 의 출력 열 **sp_cursor_list** 및 **sp_describe_cursor** 은 커서 변수의 이름을 반환 합니다.
  
으로 만들어진 모든 변수는 **커서** 데이터 형식에는 null을 허용 합니다.
  
**커서** CREATE TABLE 문에서 열에 대 한 데이터 형식을 사용할 수 없습니다.
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40; Transact SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[커서 &#40; 선언 Transact SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

