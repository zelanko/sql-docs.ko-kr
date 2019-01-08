---
title: sys.dm_os_cluster_properties (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff0854e1252b4adc38c2c3d5f2022762fb3bd0f8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544120"
---
# <a name="sysdmosclusterproperties-transact-sql"></a>sys.dm_os_cluster_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에 나오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터 리소스 속성의 현재 설정이 포함된 하나의 행을 반환합니다. 이 뷰를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에서 실행하는 경우에는 데이터가 반환되지 않습니다.  
  
 이러한 속성은 실패 감지, 실패 응답 시간 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 상태를 모니터링하기 위한 로깅에 영향을 주는 값을 설정하는 데 사용됩니다.  
  

|열 이름|속성|Description|  
|-----------------|--------------|-----------------|  
|VerboseLogging|BIGINT|SQL Server 장애 조치(failover) 클러스터에 대한 로깅 수준입니다. 자세한 로깅을 설정하여 오류 로그에 문제 해결을 위한 추가 정보를 제공할 수 있습니다. 다음 값 중 하나입니다.<br /><br /> 0 - 로깅이 해제됩니다(기본값).<br /><br /> 1  -  오류만 로깅됩니다.<br /><br /> 2 - 오류 및 경고가 로깅됩니다.<br /><br /> 자세한 내용은 [ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)합니다.|  
|SqlDumperDumpFlags|BIGINT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성되는 덤프 파일의 형식을 결정하는 SQLDumper 덤프 플래그입니다. 기본 설정은 0입니다.|  
|SqlDumperDumpPath|nvarchar(260)|SQLDumper 유틸리티에서 덤프 파일을 생성하는 위치입니다.|  
|SqlDumperDumpTimeOut|BIGINT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 시 SQLDumper 유틸리티에서 덤프를 생성하기 위한 제한 시간 값(밀리초)입니다. 기본값은 0입니다.|  
|FailureConditionLevel|BIGINT|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터가 실패하거나 다시 시작되는 조건을 설정합니다. 기본값은 3입니다. 자세한 내용은 또는 속성 설정을 변경 하려면 참조 [Configure FailureConditionLevel Property Settings](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)합니다.|  
|HealthCheckTimeout|BIGINT|SQL  Server  데이터베이스 엔진 리소스 DLL이 SQL  Server  인스턴스가 응답하지 않는 것으로 간주하기 전에 서버 상태 정보를 기다려야 하는 제한 시간 값입니다. 제한 시간 값은 밀리초로 표시됩니다. 기본값은 60000입니다. 자세한 내용을 보거나이 속성 설정을 변경 하려면를 참조 하세요 [Configure HealthCheckTimeout Property Settings](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 sys.dm_os_cluster_properties를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 리소스에 대한 속성 설정을 반환합니다.  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULL|0|3|60000|  
  
  
