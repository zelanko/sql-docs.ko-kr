---
title: 특정 작업 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SQL Server Management Objects, tasks
- SMO [SQL Server], programming
- SMO [SQL Server], tasks
ms.assetid: a15949ef-88d9-4205-892e-0b66588b4fcc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f23b7844bcff234594db87875e89a89f0f073be9
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148394"
---
# <a name="programming-specific-tasks"></a>프로그래밍 관련 태스크
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO 개체를 사용하는 프로그래밍 관련 태스크에는 백업, 통계 모니터링, 복제, 인스턴스 개체 관리, 구성 옵션 설정 등 특정 기능이 있는 프로그램에만 필요한 복잡한 작업이 포함됩니다.  
  
|항목|설명|  
|-----------|-----------------|  
|[SMO에서 연결된 서버 사용](../../../relational-databases/server-management-objects-smo/tasks/using-linked-servers-in-smo.md)|SMO가 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체를 사용하여 OLE-DB 서버에 연결하는 방법에 대해 설명합니다.|  
|[SMO에서 SQL Server 구성](../../../relational-databases/server-management-objects-smo/tasks/configuring-sql-server-in-smo.md)|SMO에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 구성 설정을 보고 수정하는 방법에 대해 설명합니다.|  
|[테이블 및 인덱스 분할 사용](../../../relational-databases/server-management-objects-smo/tasks/using-table-and-index-partitioning.md)|SMO에서 인덱스 및 테이블 분할을 사용하는 방법에 대해 설명합니다.|  
|[파일 그룹 및 파일을 사용하여 데이터 저장](../../../relational-databases/server-management-objects-smo/tasks/using-filegroups-and-files-to-store-data.md)|SMO에서 파일 그룹을 사용하는 방법에 대해 설명합니다.|  
|[WMI 공급자를 사용하여 서비스 및 네트워크 설정 관리](../../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)|구성 관리용 WMI 공급자를 나타내는 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 추적하는 여러 가지 방법에 대해 설명합니다.|  
|[데이터베이스 개체 작업](../../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-database-objects.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 개체를 나타내는 인스턴스 클래스를 만드는 방법에 대해 설명합니다.|  
|[사용자, 역할 및 로그인 관리](../../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)|SMO에서 보안 역할을 사용하는 방법에 대해 설명합니다.|  
|[권한 부여, 취소 및 거부](../../../relational-databases/server-management-objects-smo/tasks/granting-revoking-and-denying-permissions.md)|SMO를 사용하여 사용자 또는 역할 멤버에게 권한을 부여하고 취소하고 거부하는 방법에 대해 설명합니다.|  
|[암호화 사용](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)|SMO에서 암호화를 사용하여 데이터를 보호하는 방법에 대해 설명합니다.|  
|[SQL Server 에이전트에서 자동 관리 태스크 예약](../../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 사용하여 SMO에서 작업을 모니터링하고 보고하고 예약하는 방법에 대해 설명합니다.|  
|[데이터베이스 및 트랜잭션 로그 백업 및 복원](../../../relational-databases/server-management-objects-smo/tasks/backing-up-and-restoring-databases-and-transaction-logs.md)|SMO에서 데이터베이스 및 트랜잭션 로그를 백업하고 복원하는 방법에 대해 설명합니다.|  
|[스크립팅](../../../relational-databases/server-management-objects-smo/tasks/scripting.md)|SMO에서 개체를 스크립팅하고 개체 간 종속성을 검색하는 방법에 대해 설명합니다.|  
|[데이터 전송](../../../relational-databases/server-management-objects-smo/tasks/transferring-data.md)|SMO에서 데이터를 전송하는 방법에 대해 설명합니다.|  
|[데이터베이스 메일 사용](../../../relational-databases/server-management-objects-smo/tasks/using-database-mail.md)|SMO에서 전자 메일 서비스를 사용하는 방법에 대해 설명합니다.|  
|[Service Broker 관리](../../../relational-databases/server-management-objects-smo/tasks/managing-service-broker.md)|SMO를 사용하여 Service Broker를 설정하는 방법에 대해 설명합니다.|  
|[XML 스키마 사용](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)|SMO에서 XML 데이터 형식을 사용하는 방법에 대해 설명합니다.|  
|[동의어 사용](../../../relational-databases/server-management-objects-smo/tasks/using-synonyms.md)|SMO에서 동의어를 만드는 방법에 대해 설명합니다.|  
|[메시지 사용](../../../relational-databases/server-management-objects-smo/tasks/using-messages.md)|시스템 메시지를 사용하는 방법과 고유의 사용자 정의 메시지를 정의하는 방법에 대해 설명합니다.|  
|[전체 텍스트 검색 구현](../../../relational-databases/server-management-objects-smo/tasks/implementing-full-text-search.md)|SMO에서 전체 텍스트 검색 카탈로그와 인덱스를 구현하는 방법에 대해 설명합니다.|  
|[엔드포인트 구현](../../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md)|데이터베이스 미러링, SOAP 요청 및 Service Broker에 대한 페이로드를 처리하는 엔드포인트를 만드는 방법에 대해 설명합니다.|  
|[통계 생성 및 업데이트](../../../relational-databases/server-management-objects-smo/tasks/creating-and-updating-statistics.md)|SMO에서 데이터베이스에 통계를 설정하고 이를 모니터링하는 방법에 대해 설명합니다.|  
|[이벤트 추적 및 재생](../../../relational-databases/server-management-objects-smo/tasks/tracing-and-replaying-events.md)|SMO에서 **추적** 및 **재생** 개체를 사용 하 여 이벤트를 추적 하 고 재생 하는 방법을 설명 합니다.|  
  
  
