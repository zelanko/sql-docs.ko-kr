---
title: 가용성 그룹에 대한 SQL Server 리소스 DLL 상태 진단 로그
description: SQL Server 리소스 DLL이 Always On 가용성 그룹의 상태를 모니터링하는 방법을 설명합니다.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a1703e24458e21bf267c4b33ce458e7fedbead1d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207762"
---
# <a name="sql-server-resource-dll-health-diagnostic-logs-for-availability-groups"></a>가용성 그룹에 대한 SQL Server 리소스 DLL 상태 진단 로그
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  주 가용성 복제본의 상태를 모니터링하기 위해 WSFC(Windows Server 장애 조치(failover) 클러스터링)에서 실행되는 SQL Server 리소스 DLL은 [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)라는 SQL Server 인스턴스에 저장된 프로시저를 사용합니다.  
  
 SQL Server 리소스 DLL은 자세한 상태 진단을 SQL Server 리소스 DLL에 정기적으로 보내는 SQL Server 인스턴스를 통해 SQL Server 인스턴스와 전용 열린 연결을 유지 관리합니다. 클러스터의 가용성 그룹 리소스에서 구성된 장애 조치(failover) 정책으로 결합된 상태 진단은(FailoverConditionLevel 속성) 클러스터에서 가용성 그룹 리소스를 다시 시작하거나 장애 조치(failover)할지 여부를 결정하는 데 사용됩니다. 이 저장 프로시저는 인스턴스에 대한 정기적 연결이 `SELECT @@SERVERNAME` 쿼리로 만들어지는 SQL Server 2008 R2 이하보다 더 세분화되고 신뢰할 수 있는 WSFC 클러스터에 대한 SQL Server 2012 이상 인스턴스 "하트비트"입니다. 그런 다음, 가용성 그룹 FailureConditonLevel 속성을 설정하여 장애 조치(failover)를 트리거하는 조건을 제어할 수 있습니다.  
  
 **SQL Server 장애 조치(failover) 클러스터 진단 로그 사용**
 
 sp_server_diagnostics에서 받는 모든 상태 진단 SQL Server 리소스 DLL은 SQL Server 인스턴스의 기본 로그 디렉터리에 자동으로 저장됩니다(%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log). 이러한 로그는 SQLDIAG 로그라고 하며 XEL(확장 이벤트) 파일 형식으로 저장됩니다. SQL Server 로그 디렉터리에 있는 이러한 파일의 형식은 다음과 같습니다. \<HOSTNAME>_\<INSTANCENAME>_SQLDIAG_X_XXXXXXXXX.xel. SQLDIAG 로그를 확인하여 가용성 그룹 리소스 오류 또는 장애 조치(failover) 이벤트의 근본 원인을 확인할 수 있습니다.  
  
 SQLDIAG 로그를 보려면 .xel 파일을 SQL Server Management Studio로 끕니다.  
  
  
