---
title: TRUSTWORTHY 데이터베이스 속성 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database property
ms.assetid: 64b2a53d-4416-4a19-acc0-664a61b45348
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: cb783b76e29ec77dd421fb3a73b34aa04dbb228d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850891"
---
# <a name="trustworthy-database-property"></a>TRUSTWORTHY 데이터베이스 속성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  TRUSTWORTHY 데이터베이스 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 데이터베이스 및 그 내용을 트러스트하는지 여부를 나타내는 데 사용됩니다. 기본적으로 이 설정은 OFF이지만 ALTER DATABASE 문을 사용하여 ON으로 설정할 수 있습니다. `ALTER DATABASE AdventureWorks2012 SET TRUSTWORTHY ON;`)을 입력합니다.  
  
> [!NOTE]  
>  이 옵션을 설정하려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
 이 속성을 사용하면 다음 개체 중 하나가 포함된 데이터베이스를 연결하여 발생할 수 있는 특정 위협을 줄여 줍니다.  
  
-   EXTERNAL_ACCESS 또는 UNSAFE 권한 설정이 포함된 악의적인 어셈블리. 자세한 내용은 [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)을 참조하세요.  
  
-   고급 권한 사용자로 실행하도록 정의된 악의적인 모듈. 자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.  
  
 이러한 경우 모두 특정 수준의 권한이 필요하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 이미 연결된 데이터베이스의 컨텍스트에 사용될 때 적합한 메커니즘에 의해 차단됩니다. 하지만 데이터베이스가 오프라인 상태인 경우 데이터베이스 파일에 액세스할 수 있는 사용자가 자신이 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 이를 연결하고 데이터베이스의 악의적인 내용을 추가할 가능성이 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스가 분리 및 연결된 경우 데이터베이스 파일에 대한 액세스를 제한하는 데이터 및 로그 파일에 특정 사용 권한이 설정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결된 데이터베이스는 즉시 트러스트될 수 없으므로 데이터베이스가 명시적으로 신뢰할 수 있는 것으로 표시되지 않는 한 데이터베이스가 해당 범위를 벗어나는 리소스에 액세스할 수 없습니다. 또한 데이터베이스 외부의 리소스를 액세스하도록 디자인된 모듈과 EXTERNAL_ACCESS 또는 UNSAFE 권한이 설정된 어셈블리에는 성공적인 실행을 위한 추가 요구 사항이 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
