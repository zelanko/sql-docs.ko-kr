---
title: 고유하게 컴파일된 저장 프로시저의 마이그레이션 문제 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f43faad4-2182-4b43-a76a-0e3b405816d1
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 028f1776a41600146bd94114bfb54e9bd5f90420
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715511"
---
# <a name="migration-issues-for-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저의 마이그레이션 문제
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 섹션에서는 고유하게 컴파일된 저장 프로시저 만들기와 관련된 여러 문제를 설명합니다.  
  
 고유하게 컴파일된 저장 프로시저에 대한 자세한 내용은 [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.  
  
-   [고유하게 컴파일된 저장 프로시저의 TempDB에서 테이블 만들기 및 액세스](../../relational-databases/in-memory-oltp/create-and-access-tables-in-tempdb-from-stored-procedures.md)  
  
-   [IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문](../../relational-databases/in-memory-oltp/simulating-an-if-while-exists-statement-in-a-natively-compiled-module.md)  
  
-   [고유하게 컴파일된 저장 프로시저에서 MERGE 기능 구현](../../relational-databases/in-memory-oltp/implementing-merge-functionality-in-a-natively-compiled-stored-procedure.md)  
  
-   [고유하게 컴파일된 저장 프로시저에서 CASE 식 구현](../../relational-databases/in-memory-oltp/implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md)  
  
-   [FROM 또는 하위 쿼리를 사용하여 UPDATE 구현](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md)  
  
-   [외부 조인 구현](../../relational-databases/in-memory-oltp/implementing-an-outer-join.md)  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
