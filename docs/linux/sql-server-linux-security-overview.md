---
title: "Linux에서 SQL Server에 대 한 보안 관련 제한 사항이 | Microsoft Docs"
description: "이 항목에서는 Linux 제한 사항에 대 한 SQL Server를 설명 합니다."
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.openlocfilehash: 6564447c9b07bbf8147ca256d2898c535199c7f3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 보안 제한 사항

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

현재 Linux에서 SQL Server에는 다음과 같은 제한 사항이 있습니다.

* 표준 암호 정책이 제공 됩니다. MUST_CHANGE가 유일한 옵션을 구성할 수 있습니다.  
* 확장 가능 키 관리 지원 되지 않습니다. 
* Azure 키 자격 증명 모음에 저장 된 키를 사용 하는 것은 지원 되지 않습니다.
* SQL Server 연결 암호화에 대 한 자체 서명 된 인증서를 생성 합니다. 현재 SQL Server SSL 또는 TLS에 대 한 인증서를 제공 하는 사용자를 사용 하도록 구성할 수 없습니다. 

SQL Server에서 사용할 수 있는 보안 기능에 대 한 자세한 내용은 참조는 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대 한 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)합니다.

## <a name="next-steps"></a>다음 단계

일반적인 보안 작업에 대 한 참조 [Linux에서 SQL Server의 보안 기능을 시작](sql-server-linux-security-get-started.md)합니다.   
TCP를 변경 하는 스크립트에 대 한 포트 번호, SQL Server 디렉터리 및 traceflag 또는 데이터 정렬 구성, 참조 [mssql conf와 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.
