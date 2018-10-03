---
title: Linux의 SQL Server에 대 한 보안 제한 사항 | Microsoft Docs
description: 이 문서에서는 Linux 제한에서 SQL Server를 설명합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 9c58592568ca841df270190970fb76fefe43d96d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711721"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Linux의 SQL Server에 대 한 보안 제한 사항

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux의 SQL Server는 현재 다음과 같은 제한 사항이 있습니다.

* 표준 암호 정책을 제공 됩니다. MUST_CHANGE가 유일한 옵션을 구성할 수 있습니다.  
* 확장 가능 키 관리는 지원 되지 않습니다. 
* Azure Key Vault에 저장 된 키를 사용 하는 것은 지원 되지 않습니다.
* SQL Server 연결 암호화에 대 한 고유한 자체 서명 된 인증서를 생성 합니다. TLS에 대 한 인증서를 제공 하는 사용자를 사용 하려면 SQL Server는 구성할 수 있습니다. 

SQL Server에서 사용 가능한 보안 기능에 대 한 자세한 내용은 참조는 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대 한 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)합니다.

## <a name="next-steps"></a>다음 단계

보안의 일반적인 작업을 참조 하세요 [Linux의 SQL Server의 보안 기능을 사용 하 여 시작](sql-server-linux-security-get-started.md)합니다. TCP를 변경 하는 스크립트에 대 한 포트 번호를 SQL Server 디렉터리 및 추적 플래그 또는 데이터 정렬 구성, 참조 [mssql conf를 사용 하 여 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)합니다.
