---
title: "DDL 이벤트 | Microsoft 문서"
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: triggers
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9ab16db537c4033f0dd68ddd457e9e1a341a7449
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="ddl-events"></a>DDL 이벤트
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
다음 표에서는 DDL 트리거 또는 이벤트 알림을 실행하는 데 사용할 수 있는 DDL 이벤트를 나열합니다. 각 이벤트는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 저장 프로시저에 해당하며 키워드 사이에 밑줄(_)을 포함하도록 문 구문이 수정됩니다.  
  
> [!IMPORTANT]  
>  DDL과 같은 작업을 수행하는 시스템 저장 프로시저에서 DDL 트리거 및 이벤트 알림이 발생할 수도 있습니다. DDL 트리거와 이벤트 알림을 테스트하여 실행된 시스템 저장 프로시저에 대한 응답을 확인하십시오. 예를 들어 CREATE TYPE 문과 **sp_addtype** 저장 프로시저를 사용하면 CREATE_TYPE 이벤트에서 생성되는 DDL 트리거 또는 이벤트 알림이 발생합니다.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>서버 또는 데이터베이스 범위가 있는 DDL 문  
 DDL 트리거 또는 이벤트 알림은 트리거나 이벤트 알림이 생성된 데이터베이스 또는 서버 인스턴스에서 발생할 때 다음 이벤트에 대한 응답으로 실행되도록 생성될 수 있습니다.  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE(CREATE APPLICATION ROLE 문과 **sp_addapprole**에 적용됩니다. 새 스키마가 생성되면 이 이벤트는 CREATE_SCHEMA 이벤트도 트리거합니다.)|ALTER_APPLICATION_ROLE(ALTER APPLICATION ROLE 문과 **sp_approlepassword**에 적용됩니다.)|DROP_APPLICATION_ROLE(DROP APPLICATION ROLE 문과 **sp_dropapprole**에 적용됩니다.)|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE(ON DATABASE가 지정된 경우 ALTER AUTHORIZATION 문과 **sp_changedbowner**에 적용됩니다.)||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT( **sp_bindefault**에 적용됩니다.)|UNBIND_DEFAULT( **sp_unbindefault**에 적용됩니다.)||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY( **sp_addextendedproperty**에 적용됩니다.)|ALTER_EXTENDED_PROPERTY( **sp_updateextendedproperty**에 적용됩니다.)|DROP_EXTENDED_PROPERTY( **sp_dropextendedproperty**에 적용됩니다.)|  
|CREATE_FULLTEXT_CATALOG( **create** 가 지정된 경우 CREATE FULLTEXT CATALOG 문과 *sp_fulltextcatalog* 에 적용됩니다.)|ALTER_FULLTEXT_CATALOG( **start_incremental** , *start_full*, *Stop*또는 *Rebuild*가 지정된 경우 ALTER FULLTEXT CATALOG 문과 *sp_fulltextcatalog* 에 적용되고, **enable** 이 지정된 경우 *sp_fulltext_database* 에 적용됩니다.)|DROP_FULLTEXT_CATALOG( **drop** 이 지정된 경우 DROP FULLTEXT CATALOG 문과 *sp_fulltextcatalog* 에 적용됩니다.)|  
|CREATE_FULLTEXT_INDEX( **create** 가 지정된 경우 CREATE FULLTEXT INDEX 문과 *sp_fulltexttable* 에 적용됩니다.)|ALTER_FULLTEXT_INDEX( **start_full** , *start_incremental*또는 *stop*이 지정된 경우 ALTER FULLTEXT INDEX 문과 *sp_fulltextcatalog* 에 적용되고, **create**또는 **drop** 외에 다른 동작이 지정된 경우 *sp_fulltext_column* 과 *sp_fulltext_table* 에 적용됩니다.)|DROP_FULLTEXT_INDEX( **drop** 이 지정된 경우 DROP FULLTEXT INDEX 문과 *sp_fulltexttable* 에 적용됩니다.)|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX(ALTER INDEX 문과 **sp_indexoption**에 적용됩니다.)|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE( **sp_create_plan_guide**에 적용됩니다.)|ALTER_PLAN_GUIDE(ENABLE, ENABLE ALL, DISABLE 또는 DISABLE ALL이 지정된 경우 **sp_control_plan_guide** 에 적용됩니다.)|DROP_PLAN_GUIDE(DROP 또는 DROP ALL이 지정된 경우 **sp_control_plan_guide** 에 적용됩니다.)|  
|CREATE_PROCEDURE|ALTER_PROCEDURE(ALTER PROCEDURE 문과 **sp_procoption**에 적용됩니다.)|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME( **sp_rename**에 적용됩니다.)|||  
|CREATE_ROLE(CREATE ROLE 문, **sp_addrole**및 **sp_addgroup**에 적용됩니다.)|ALTER_ROLE|DROP_ROLE(DROP ROLE 문, **sp_droprole**및 **sp_dropgroup**에 적용됩니다.)|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE( **sp_bindrule**에 적용됩니다.)|UNBIND_RULE( **sp_unbindrule**에 적용됩니다.)||  
|CREATE_SCHEMA(CREATE SCHEMA 문, **sp_addrole**, **sp_adduser**, **sp_addgroup**및 **sp_grantdbaccess**에 적용됩니다.)|ALTER_SCHEMA(ALTER SCHEMA 문과 **sp_changeobjectowner**에 적용됩니다.)|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE(데이터베이스, 어셈블리, 트리거와 같은 비스키마 범위 개체에 대한 서명 작업용)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT(저장 프로시저, 함수와 같은 스키마 범위 개체용)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX는 공간 인덱스에 사용할 수 있습니다.|DROP_INDEX는 공간 인덱스에 사용할 수 있습니다.|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE(ALTER TABLE 문과 **sp_tableoption**에 적용됩니다.)|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER(ALTER TRIGGER 문과 **sp_settriggerorder**에 적용됩니다.)|DROP_TRIGGER|  
|CREATE_TYPE(CREATE TYPE 문과 **sp_addtype**에 적용됩니다.)|DROP_TYPE(DROP TYPE 문과 **sp_droptype**에 적용됩니다.)||  
|CREATE_USER(CREATE USER 문, **sp_adduser**및 **sp_grantdbaccess**에 적용됩니다.)|ALTER_USER(ALTER USER 문 및 **sp_change_users_login**에 적용됩니다.)|DROP_USER(DROP USER 문, **sp_dropuser**및 **sp_revokedbaccess**에 적용됩니다.)|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX는 XML 인덱스에 사용할 수 있습니다.|DROP_INDEX는 XML 인덱스에 사용할 수 있습니다.|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>서버 범위가 있는 DDL 문  
 DDL 트리거 또는 이벤트 알림이 서버 인스턴스에서 발생할 때 다음 이벤트에 대한 응답으로 시작되도록 생성될 수 있습니다.  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE(로컬 서버 인스턴스가 지정된 경우 **sp_configure** 및 **sp_addserver** 에 적용됩니다.)|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE(ALTER DATABASE 문과 **sp_fulltext_database**에 적용됩니다.)|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE( **sp_addextendedproc**에 적용됩니다.)|DROP_EXTENDED_PROCEDURE( **sp_dropextendedproc**에 적용됩니다.)||  
|CREATE_LINKED_SERVER( **sp_addlinkedserver**에 적용됩니다.)|ALTER_LINKED_SERVER( **sp_serveroption**에 적용됩니다.)|DROP_LINKED_SERVER(연결된 서버가 지정된 경우 **sp_dropserver** 에 적용됩니다.)|  
|CREATE_LINKED_SERVER_LOGIN( **sp_addlinkedsrvlogin**에 적용됩니다.)|DROP_LINKED_SERVER_LOGIN( **sp_droplinkedsrvlogin**에 적용됩니다.)||  
|CREATE_LOGIN(암시적으로 만들어야 하는 존재하지 않는 로그인이 사용된 경우 CREATE LOGIN 문, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**및 **sp_denylogin** 에 적용됩니다.)|ALTER_LOGIN( **Auto_Fix**가 지정된 경우 ALTER LOGIN 문, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password** 및 *sp_change_users_login* 에 적용됩니다.)|DROP_LOGIN(DROP LOGIN 문, **sp_droplogin**, **sp_revokelogin**및 **xp_revokelogin**에 적용됩니다.)|  
|CREATE_MESSAGE( **sp_addmessage**에 적용됩니다.)|ALTER_MESSAGE( **sp_altermessage**에 적용됩니다.)|DROP_MESSAGE( **sp_dropmessage**에 적용됩니다.)|  
|CREATE_REMOTE_SERVER( **sp_addserver**에 적용됩니다.)|ALTER_REMOTE_SERVER( **sp_setnetname**에 적용됩니다.)|DROP_REMOTE_SERVER(원격 서버가 지정된 경우 **sp_dropserver** 에 적용됩니다.)|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|ALTER_WORKLOAD_GROUP|DROP_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>참고 항목  
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)   
 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)   
 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
