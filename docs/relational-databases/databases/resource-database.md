---
title: Resource 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system objects [SQL Server]
- read-only databases
- mssqlsystemresource.mdf file
- Resource database [SQL Server]
ms.assetid: d592b2b4-bc36-4eb9-9385-8fe4dff0dced
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f6b63e0ff79f44b2900fb0f727436ed36401ee2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68127456"
---
# <a name="resource-database"></a>Resource 데이터베이스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Resource 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 시스템 개체가 모두 들어 있는 읽기 전용 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 개체(예: sys.objects)는 실제로는 Resource 데이터베이스에 저장되지만 논리적으로는 모든 데이터베이스의 sys 스키마에 나타납니다. Resource 데이터베이스에는 사용자 데이터 또는 사용자 메타데이터가 없습니다.  
  
 Resource 데이터베이스를 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 빠르고 쉽게 업그레이드합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드를 수행하려면 시스템 개체를 삭제한 다음 만들어야 합니다. 이제 Resource 데이터베이스 파일에 모든 시스템 개체가 들어 있으므로 단일 Resource 데이터베이스 파일을 로컬 서버에 복사하면 업그레이드할 수 있습니다.  
  
## <a name="physical-properties-of-resource"></a>Resource의 물리적 속성  
 Resource 데이터베이스의 물리적 파일 이름은 mssqlsystemresource.mdf 및 mssqlsystemresource.ldf입니다. 이러한 파일은 \<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\에 있으며 이동할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 각 인스턴스에는 관련된 mssqlsystemresource.mdf 파일이 하나만 있으며 인스턴스에서 이 파일을 공유하지 않습니다.  
  
> [!WARNING]  
>  업그레이드와 서비스 팩은 BINN 폴더에 설치되는 새 리소스 데이터베이스를 제공합니다. 리소스 데이터베이스의 위치 변경은 지원되지 않거나 사용하지 않는 것이 좋습니다.  
  
## <a name="backing-up-and-restoring-the-resource-database"></a>Resource 데이터베이스 백업 및 복원  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 Resource 데이터베이스를 백업할 수 없습니다. mssqlsystemresource.mdf 파일을 데이터베이스 파일이 아닌 이진(.EXE) 파일인 것처럼 처리하여 자체 파일 기반 또는 디스크 기반 백업을 수행할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 백업을 복원할 수는 없습니다. 수동으로만 mssqlsystemresource.mdf 백업 복사본을 복원할 수 있으며 현재 Resource 데이터베이스를 오래된 버전이나 안전하지 않은 버전으로 덮어쓰지 않도록 주의해야 합니다.  
  
> [!IMPORTANT]  
>  mssqlsystemresource.mdf 백업을 복원한 후에 후속 업데이트를 다시 적용해야 합니다.  
  
## <a name="accessing-the-resource-database"></a>Resource 데이터베이스 액세스  
 Resource 데이터베이스는 Microsoft CSS(고객 지원 서비스) 전문가가 직접 수정하거나 전문가의 지도를 받아 수정해야 합니다. Resource 데이터베이스의 ID는 항상 32767입니다. Resource 데이터베이스와 관련된 다른 중요한 값은 버전 번호 및 데이터베이스가 마지막으로 업데이트된 시간입니다.  
  
 Resource **데이터베이스의 버전 번호를** **확인하려면 다음 문을 사용합니다**.  
  
```  
SELECT SERVERPROPERTY('ResourceVersion');  
GO  
```  
  
 Resource **데이터베이스가 마지막으로 업데이트된** **시기를 확인하려면 다음 문을 사용합니다**.  
  
```  
SELECT SERVERPROPERTY('ResourceLastUpdateDateTime');  
GO  
```  
  
 **시스템 개체의 SQL 정의에 액세스하려면 OBJECT_DEFINITION 함수를 사용합니다.**  
  
```  
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.objects'));  
GO  
```  
  
## <a name="related-content"></a>관련 내용  
 [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)  
  
 [데이터베이스 관리자를 위한 진단 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
 [단일 사용자 모드로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
