---
title: "수정된 기능(포함된 데이터베이스) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: contained database, modifications to DBs
ms.assetid: a2942509-39a2-4903-b504-ae80a300a9de
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b44e142fba4e81b90ab7de843bcd8d97ab4ea0c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="modified-features-contained-database"></a>수정된 기능(포함된 데이터베이스)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 다음 기능은 부분적으로 포함된 데이터베이스에서 지원하도록 수정되었습니다. 일반적으로 기능은 데이터베이스 경계를 넘지 않도록 수정됩니다.  
  
 자세한 내용은 [Contained Databases](../../relational-databases/databases/contained-databases.md)을 참조하세요.  
  
## <a name="alter-database"></a>ALTER DATABASE  
  
### <a name="application-level"></a>응용 프로그램 수준  
 포함된 데이터베이스 내부에서 ALTER DATABASE 문을 사용하는 경우 구문은 포함되지 않은 데이터베이스에 사용되는 구문과 다릅니다. 이러한 차이에는 데이터베이스를 넘어 인스턴스로 확장되는 문 요소의 제한 사항이 포함됩니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
### <a name="instance-level"></a>인스턴스 수준  
 포함된 데이터베이스 외부에서 사용되는 ALTER DATABASE의 구문은 포함되지 않은 데이터베이스에 사용될 때의 구문과 다릅니다. 이러한 변경 사항은 데이터베이스 경계를 넘는 문제를 방지합니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
## <a name="create-database"></a>CREATE DATABASE  
 포함된 데이터베이스에 대한 CREATE DATABASE 구문은 포함되지 않은 데이터베이스에 대한 CREATE DATABASE 구문과 다릅니다. 새 구문 요구 사항 및 허용 사항에 대한 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
## <a name="temporary-tables"></a>임시 테이블  
 로컬 임시 테이블은 포함된 데이터베이스 내에 허용되지만 해당 동작은 포함되지 않은 데이터베이스에서의 동작과 다릅니다. 포함되지 않은 데이터베이스에서 임시 테이블 데이터는 **tempdb**의 데이터 정렬에서 데이터 정렬됩니다. 포함된 데이터베이스에서 임시 테이블 데이터는 포함된 데이터베이스의 데이터 정렬에서 데이터 정렬됩니다.  
  
 임시 테이블과 연결된 모든 메타데이터(예: 테이블 및 열 이름, 인덱스 등)는 카탈로그 데이터 정렬에 배치됩니다.  
  
 명명된 제약 조건은 임시 테이블에서 사용할 수 없습니다.  
  
 임시 테이블은 사용자 정의 형식, XML 스키마 컬렉션 또는 사용자 정의 함수를 참조할 수 없습니다.  
  
## <a name="collation"></a>데이터 정렬  
 포함되지 않은 데이터베이스 모델에는 데이터베이스 데이터 정렬, 인스턴스 데이터 정렬 및 tempdb 데이터 정렬이라는 별도의 세 가지 데이터 정렬이 있습니다. 포함된 데이터베이스는 두 가지의 데이터 정렬인 데이터베이스 데이터 정렬과 새 카탈로그 데이터 정렬만 사용합니다. 포함된 데이터베이스 데이터 정렬에 대한 자세한 내용은 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md) 을 참조하십시오.  
  
## <a name="user-options"></a>사용자 옵션  
 포함된 데이터베이스를 사용하도록 설정할 경우 [인스턴스에 대해](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) user options 옵션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 0으로 설정해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)   
 [Contained Databases](../../relational-databases/databases/contained-databases.md)  
  
  
