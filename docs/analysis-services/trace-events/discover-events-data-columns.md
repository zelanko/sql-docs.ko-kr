---
title: Discover Events 데이터 열 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 608c64072132fc8894105fb990986c039e70e55b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="discover-events-data-columns"></a>Discover Events 데이터 열
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Discover Events 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
-   Discover Begin 클래스  
  
-   Discover End 클래스  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="discover-begin-classdata-columns"></a>Discover Begin 클래스 - 데이터 열  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.  다음 **하위 클래스 ID**/**하위 클래스 이름** 값 쌍이 유효합니다.<br /><br /> 0: DBSCHEMA_CATALOGS<br /><br /> 1: DBSCHEMA_TABLES<br /><br /> 2: DBSCHEMA_COLUMNS<br /><br /> 3: DBSCHEMA_PROVIDER_TYPES<br /><br /> 4: MDSCHEMA_CUBES<br /><br /> 5: MDSCHEMA_DIMENSIONS<br /><br /> 6: MDSCHEMA_HIERARCHIES<br /><br /> 7: MDSCHEMA_LEVELS<br /><br /> 8: MDSCHEMA_MEASURES<br /><br /> 9: MDSCHEMA_PROPERTIES<br /><br /> 10: MDSCHEMA_MEMBERS<br /><br /> 11: MDSCHEMA_FUNCTIONS<br /><br /> 12: MDSCHEMA_ACTIONS<br /><br /> 13: MDSCHEMA_SETS<br /><br /> 14: DISCOVER_INSTANCES<br /><br /> 15: MDSCHEMA_KPIS<br /><br /> 16: MDSCHEMA_MEASUREGROUPS<br /><br /> 17: MDSCHEMA_COMMANDS<br /><br /> 18: DMSCHEMA_MINING_SERVICES<br /><br /> 19: DMSCHEMA_MINING_SERVICE_PARAMETERS<br /><br /> 20: DMSCHEMA_MINING_FUNCTIONS<br /><br /> 21: DMSCHEMA_MINING_MODEL_CONTENT<br /><br /> 22: DMSCHEMA_MINING_MODEL_XML<br /><br /> 23: DMSCHEMA_MINING_MODELS<br /><br /> 24: DMSCHEMA_MINING_COLUMNS<br /><br /> 25: DISCOVER_DATASOURCES<br /><br /> 26: DISCOVER_PROPERTIES<br /><br /> 27: DISCOVER_SCHEMA_ROWSETS<br /><br /> 28: DISCOVER_ENUMERATORS<br /><br /> 29: DISCOVER_KEYWORDS<br /><br /> 30: DISCOVER_LITERALS<br /><br /> 31: DISCOVER_XML_METADATA<br /><br /> 32: DISCOVER_TRACES<br /><br /> 33: DISCOVER_TRACE_DEFINITION_PROVIDERINFO<br /><br /> 34: DISCOVER_TRACE_COLUMNS<br /><br /> 35: DISCOVER_TRACE_EVENT_CATEGORIES<br /><br /> 36: DMSCHEMA_MINING_STRUCTURES<br /><br /> 37: DMSCHEMA_MINING_STRUCTURE_COLUMNS<br /><br /> 38: DISCOVER_MASTER_KEY<br /><br /> 39: MDSCHEMA_INPUT_DATASOURCES<br /><br /> 40: DISCOVER_LOCATIONS<br /><br /> 41: DISCOVER_PARTITION_DIMENSION_STAT<br /><br /> 42: DISCOVER_PARTITION_STAT<br /><br /> 43: DISCOVER_DIMENSION_STAT<br /><br /> 44: MDSCHEMA_MEASUREGROUP_DIMENSIONS<br /><br /> 49: DISCOVER_XEVENT_TRACE_DEFINITION|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|검색 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTUserName|32|8|검색 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|NTDomainName|33|8|검색 이벤트와 연결된 Windows 도메인을 포함합니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID를 포함합니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|검색 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|검색 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|검색 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|검색 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|RequestProperties|45|9|검색 이벤트와 연결된 XMLA(XML for Analysis) 요청 속성을 포함합니다.|  
  
## <a name="discover-end-classdata-columns"></a>Discover End 클래스 - 데이터 열  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스를 포함하며, 이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다. 다음 **하위 클래스 ID**/**하위 클래스 이름** 값 쌍이 유효합니다.<br /><br /> 0: DBSCHEMA_CATALOGS<br /><br /> 1: DBSCHEMA_TABLES<br /><br /> 2: DBSCHEMA_COLUMNS<br /><br /> 3: DBSCHEMA_PROVIDER_TYPES<br /><br /> 4: MDSCHEMA_CUBES<br /><br /> 5: MDSCHEMA_DIMENSIONS<br /><br /> 6: MDSCHEMA_HIERARCHIES<br /><br /> 7: MDSCHEMA_LEVELS<br /><br /> 8: MDSCHEMA_MEASURES<br /><br /> 9: MDSCHEMA_PROPERTIES<br /><br /> 10: MDSCHEMA_MEMBERS<br /><br /> 11: MDSCHEMA_FUNCTIONS<br /><br /> 12: MDSCHEMA_ACTIONS<br /><br /> 13: MDSCHEMA_SETS<br /><br /> 14: DISCOVER_INSTANCES<br /><br /> 15: MDSCHEMA_KPIS<br /><br /> 16: MDSCHEMA_MEASUREGROUPS<br /><br /> 17: MDSCHEMA_COMMANDS<br /><br /> 18: DMSCHEMA_MINING_SERVICES<br /><br /> 19: DMSCHEMA_MINING_SERVICE_PARAMETERS<br /><br /> 20: DMSCHEMA_MINING_FUNCTIONS<br /><br /> 21: DMSCHEMA_MINING_MODEL_CONTENT<br /><br /> 22: DMSCHEMA_MINING_MODEL_XML<br /><br /> 23: DMSCHEMA_MINING_MODELS<br /><br /> 24: DMSCHEMA_MINING_COLUMNS<br /><br /> 25: DISCOVER_DATASOURCES<br /><br /> 26: DISCOVER_PROPERTIES<br /><br /> 27: DISCOVER_SCHEMA_ROWSETS<br /><br /> 28: DISCOVER_ENUMERATORS<br /><br /> 29: DISCOVER_KEYWORDS<br /><br /> 30: DISCOVER_LITERALS<br /><br /> 31: DISCOVER_XML_METADATA<br /><br /> 32: DISCOVER_TRACES<br /><br /> 33: DISCOVER_TRACE_DEFINITION_PROVIDERINFO<br /><br /> 34: DISCOVER_TRACE_COLUMNS<br /><br /> 35: DISCOVER_TRACE_EVENT_CATEGORIES<br /><br /> 36: DMSCHEMA_MINING_STRUCTURES<br /><br /> 37: DMSCHEMA_MINING_STRUCTURE_COLUMNS<br /><br /> 38: DISCOVER_MASTER_KEY<br /><br /> 39: MDSCHEMA_INPUT_DATASOURCES<br /><br /> 40: DISCOVER_LOCATIONS<br /><br /> 41: DISCOVER_PARTITION_DIMENSION_STAT<br /><br /> 42: DISCOVER_PARTITION_STAT<br /><br /> 43: DISCOVER_DIMENSION_STAT<br /><br /> 44: MDSCHEMA_MEASUREGROUP_DIMENSIONS<br /><br /> 49: DISCOVER_XEVENT_TRACE_DEFINITION|  
|CurrentTime|2|5|검색 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|검색 종료 이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간을 포함합니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|검색 이벤트에 소요된 대략적인 시간(밀리초)을 포함합니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)을 포함합니다.|  
|Severity|22|1.|예외의 심각도를 포함합니다.|  
|성공|23|1.|검색 이벤트의 성공 또는 실패를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 실패<br /><br /> 1 = 성공|  
|오류|24|1.|검색 이벤트와 연결된 모든 오류의 오류 번호를 포함합니다.|  
|ConnectionID|25|1.|검색 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|검색 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|개체 사용 권한 이벤트와 연결된 Windows 사용자 이름을 포함합니다.|  
|NTDomainName|33|8|검색 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|36|1.|이벤트를 시작한 응용 프로그램의 클라이언트 프로세스 ID를 포함합니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름을 포함합니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|검색 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|개체 사용 권한 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|검색 종료 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|검색 이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|RequestProperties|45|9|XMLA 요청의 속성을 포함합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Discover Events 이벤트 범주](../../analysis-services/trace-events/discover-events-event-category.md)  
  
  
