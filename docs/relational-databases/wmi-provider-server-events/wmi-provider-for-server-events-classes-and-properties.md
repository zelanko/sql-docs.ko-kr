---
description: 서버 이벤트용 WMI 공급자 클래스 및 속성
title: 서버 이벤트용 WMI 공급자 클래스 및 속성
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: be17f5425d66956028fce13144b6bb908230fca9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542735"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>서버 이벤트용 WMI 공급자 클래스 및 속성
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  서버 이벤트용 WMI 공급자의 프로그래밍 모델을 구성하는 서버 이벤트에는 공급자에 대해 WQL 쿼리를 실행하여 쿼리할 수 있는 두 가지 주요 범주의 이벤트인 DDL(데이터 정의 언어) 이벤트와 추적 이벤트가 있습니다. QUEUE_ACTIVATION 및 BROKER_QUEUE_DISABLED Service Broker 이벤트도 쿼리할 수 있습니다. 다음 트리 다이어그램의 포함 특성에 유의하십시오. 예를 들어 DDL_ASSEMBLY_EVENTS 이벤트는 모든 ALTER_ASSEMBLY, CREATE_ASSEMBLY 및 DROP_ASSEMBLY 이벤트를 포함합니다. 마찬가지로 TRC_FULL_TEXT 이벤트는 모든 FT_CRAWL_ABORTED, FT_CRAWL_STARTED 및 FT_CRAWL_STOPPED 이벤트를 포함합니다. ALL_EVENTS는 모든 DDL 이벤트, 추적 이벤트, QUEUE_ACTIVATION 및 BROKER_QUEUE_DISABLED를 포함합니다.  
  
 이벤트나 이벤트 그룹에서 쿼리할 수 있는 속성에 대해서는 이벤트 스키마를 참조하십시오. 기본적으로 이벤트 스키마는 다음 디렉터리에 설치 됩니다. [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
 또는에 게시 된 이벤트 스키마를 참조할 수 있습니다 [https://schemas.microsoft.com/sqlserver](https://go.microsoft.com/fwlink/?linkid=43100) .  
  
 예를 들어 ALTER_DATABASE 이벤트를 참조 하 여 부모 이벤트를 DDL_SERVER_LEVEL_EVENTS 하 고 해당 속성이 **Tsqlcommand** 및 **DatabaseName**임을 알게 됩니다. 또한이 이벤트는 **SQLInstance**, **posttime**, **ComputerName**, **SPID**및 **LoginName**속성을 상속 합니다. 자식 이벤트가 없습니다.  
  
> [!NOTE]  
>  DDL과 같은 작업을 수행하는 시스템 저장 프로시저에서 이벤트 알림을 발생시킬 수도 있습니다. 이벤트 알림을 테스트하여 실행된 시스템 저장 프로시저에 대한 응답을 확인합니다. 예를 들어 CREATE TYPE 문과 **sp_addtype** 저장 프로시저는 모두 CREATE_TYPE 이벤트에 대해 생성 되는 이벤트 알림을 발생 시킵니다. 자세한 내용은 [DDL Events](../../relational-databases/triggers/ddl-events.md)를 참조 하십시오.  
  
 **데이터 정의 언어 이벤트 및 이벤트 그룹**  
  
 ![서버 이벤트용 WMI 공급자의 이벤트 트리](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "서버 이벤트용 WMI 공급자의 이벤트 트리")  
  
 **추적 이벤트 및 이벤트 그룹**  
  
 ![추적 이벤트 및 이벤트 그룹](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "추적 이벤트 및 이벤트 그룹")  
  
## <a name="see-also"></a>참고 항목  
 [서버 이벤트 용 WMI 공급자 개념](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [서버 이벤트용 WMI 공급자에 WQL 사용](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
