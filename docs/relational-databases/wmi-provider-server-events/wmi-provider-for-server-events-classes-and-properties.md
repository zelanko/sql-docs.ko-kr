---
title: "서버 이벤트 용 WMI 공급자 클래스 및 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56bbed9164ef0f627cfeb19b4d5b38e3b88c37d3
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>서버 이벤트용 WMI 공급자 클래스 및 속성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
서버 이벤트용 WMI 공급자의 프로그래밍 모델을 구성하는 서버 이벤트에는 공급자에 대해 WQL 쿼리를 실행하여 쿼리할 수 있는 두 가지 주요 범주의 이벤트인 DDL(데이터 정의 언어) 이벤트와 추적 이벤트가 있습니다. QUEUE_ACTIVATION 및 BROKER_QUEUE_DISABLED Service Broker 이벤트도 쿼리할 수 있습니다. 다음 트리 다이어그램의 포함 특성에 유의하십시오. 예를 들어 DDL_ASSEMBLY_EVENTS 이벤트는 모든 ALTER_ASSEMBLY, CREATE_ASSEMBLY 및 DROP_ASSEMBLY 이벤트를 포함합니다. 마찬가지로 TRC_FULL_TEXT 이벤트는 모든 FT_CRAWL_ABORTED, FT_CRAWL_STARTED 및 FT_CRAWL_STOPPED 이벤트를 포함합니다. ALL_EVENTS는 모든 DDL 이벤트, 추적 이벤트, QUEUE_ACTIVATION 및 BROKER_QUEUE_DISABLED를 포함합니다.  
  
 이벤트나 이벤트 그룹에서 쿼리할 수 있는 속성에 대해서는 이벤트 스키마를 참조하십시오. 기본적으로 이벤트 스키마가 다음 디렉터리에 설치: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd 합니다.  
  
 게시 된 이벤트 스키마를 참조할 수 있습니다 또는 [http://schemas.microsoft.com/sqlserver](http://go.microsoft.com/fwlink/?linkid=43100)합니다.  
  
 예를 들어 ALTER_DATABASE 이벤트를 참조 하 여 배웁니다 부모 이벤트가 DDL_SERVER_LEVEL_EVENTS이 고 해당 속성은 **TSQLCommand** 및 **DatabaseName**합니다. 이벤트 속성을 상속 **SQLInstance**, **PostTime**, **ComputerName**, **SPID**, 및 **LoginName** . 자식 이벤트가 없습니다.  
  
> [!NOTE]  
>  DDL과 같은 작업을 수행하는 시스템 저장 프로시저에서 이벤트 알림을 발생시킬 수도 있습니다. 이벤트 알림을 테스트하여 실행된 시스템 저장 프로시저에 대한 응답을 확인합니다. 예를 들어 CREATE TYPE 문 및 **sp_addtype** 저장된 프로시저 모두 CREATE_TYPE 이벤트에서 생성 되는 이벤트 알림을 발생 합니다. 자세한 내용은 참조[DDL 이벤트](../../relational-databases/triggers/ddl-events.md)합니다.  
  
 **데이터 정의 언어 이벤트 및 이벤트 그룹**  
  
 ![서버 이벤트의 이벤트 트리 용 WMI 공급자](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "서버 이벤트의 이벤트 트리 용 WMI 공급자")  
  
 **추적 이벤트 및 이벤트 그룹**  
  
 ![추적 이벤트 및 이벤트 그룹](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "추적 이벤트 및 이벤트 그룹")  
  
## <a name="see-also"></a>관련 항목:  
 [서버 이벤트 개념에 대 한 WMI 공급자](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [서버 이벤트용 WMI 공급자에 WQL 사용](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
