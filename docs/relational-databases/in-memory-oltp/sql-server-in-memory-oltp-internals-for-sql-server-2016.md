---
title: SQL Server 메모리 내 OLTP 내부
description: 테이블을 메모리 최적화로 선언해 메모리 내 OLTP 기능을 사용할 수 있도록 하는 SQL Server 메모리 내 OLTP 기술 구현에 대해 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 09/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b14da361-a6b8-4d85-b196-7f2f13650f44
author: kevin-farlee
ms.author: kfarlee
ms.openlocfilehash: 1df603174fb4f17fef0f04ea41fa4b95154ab247
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175965"
---
# <a name="sql-server-in-memory-oltp-internals-for-sql-server-2016"></a>SQL Server 2016용 SQL Server 메모리 내 OLTP 내부
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**요약:** 흔히 코드명 "Hekaton"으로 불리는 메모리 내 OLTP는 SQL Server 2014에서 도입되었습니다.
이 강력한 기술을 사용하면 많은 양의 메모리와 수십 개의 코어를 활용하여 OLTP 작업의 성능을 30-40배까지 늘릴 수 있습니다. SQL Server 2016에서는 메모리 내 OLTP에 계속 투자하여 SQL Server 2014에 있던 여러 제한 사항을 없애고 내부 처리 알고리즘을 향상하고 있으므로 메모리 내 OLTP에서 훨씬 향상된 기능을 제공할 수 있습니다. 이 백서에서는 SQL Server 2016 RTM을 기준으로 SQL Server 2016의 메모리 내 OLTP 기술에 대한 구현을 설명합니다. 메모리 내 OLTP를 사용하면 메모리 내 OLTP 기능을 사용할 수 있도록 '메모리에 최적화된' 테이블을 선언할 수 있습니다. 메모리에 최적화된 테이블은 완전히 트랜잭션이 될 수 있고 Transact-SQL을 사용하여 액세스할 수 있습니다. Transact-SQL 저장 프로시저, 트리거 및 스칼라 UDF를 기계어 코드로 컴파일하여 메모리 최적화 테이블의 성능을 더 향상할 수 있습니다. 이 엔진은 동시성이 높고 차단이 없도록 설계되었습니다.    
  
**작성자:** Kalen Delaney  
  
**기술 검토자:** Sunil Agarwal 및 Jos de Bruijn  
  
**게시 날짜:** 2016년 6월  
  
**적용 대상:** SQL Server 2016  
  
문서를 검토하려면 [SQL Server 2016용 SQL Server 메모리 내 OLTP 내부](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf) 문서를 다운로드합니다.   
