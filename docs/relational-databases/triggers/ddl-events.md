---
description: DDL 이벤트
title: DDL 이벤트 | Microsoft 문서
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25cdef293ced7b58ea41f71f78a1046c6b5dd0ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463805"
---
# <a name="ddl-events"></a>DDL 이벤트
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  다음 표에서는 DDL 트리거 또는 이벤트 알림을 실행하는 데 사용할 수 있는 DDL 이벤트를 나열합니다. 각 이벤트는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 저장 프로시저에 해당하며 키워드 사이에 밑줄(_)을 포함하도록 문 구문이 수정됩니다.  
  
> [!IMPORTANT]  
>  DDL과 같은 작업을 수행하는 시스템 저장 프로시저에서 DDL 트리거 및 이벤트 알림이 발생할 수도 있습니다. DDL 트리거와 이벤트 알림을 테스트하여 실행된 시스템 저장 프로시저에 대한 응답을 확인하십시오. 예를 들어 CREATE TYPE 문과 **sp_addtype** 저장 프로시저를 사용하면 CREATE_TYPE 이벤트에서 생성되는 DDL 트리거 또는 이벤트 알림이 발생합니다.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>서버 또는 데이터베이스 범위가 있는 DDL 문  
 DDL 트리거 또는 이벤트 알림은 트리거나 이벤트 알림이 생성된 데이터베이스 또는 서버 인스턴스에서 발생할 때 다음 이벤트에 대한 응답으로 실행되도록 생성될 수 있습니다.  
  
:::row:::
    :::column:::
        CREATE_APPLICATION_ROLE(CREATE APPLICATION ROLE 문과 **sp_addapprole**에 적용됩니다. 새 스키마가 생성되면 이 이벤트는 CREATE_SCHEMA 이벤트도 트리거합니다.)
    :::column-end:::
    :::column:::
        ALTER_APPLICATION_ROLE(ALTER APPLICATION ROLE 문과 **sp_approlepassword**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_APPLICATION_ROLE(DROP APPLICATION ROLE 문과 **sp_dropapprole**에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASSEMBLY
    :::column-end:::
    :::column:::
        ALTER_ASSEMBLY
    :::column-end:::
    :::column:::
        DROP_ASSEMBLY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_ASYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION
    :::column-end:::
    :::column:::
        ALTER_AUTHORIZATION_DATABASE(ON DATABASE가 지정된 경우 ALTER AUTHORIZATION 문과 **sp_changedbowner**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CERTIFICATE
    :::column-end:::
    :::column:::
        ALTER_CERTIFICATE
    :::column-end:::
    :::column:::
        DROP_CERTIFICATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CONTRACT
    :::column-end:::
    :::column:::
        DROP_CONTRACT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_DATABASE
    :::column-end:::
    :::column:::
        DENY_DATABASE
    :::column-end:::
    :::column:::
        REVOKE_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        ALTER_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        DENY_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        ALTER_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        DROP_DATABASE_ENCRYPTION_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DEFAULT
    :::column-end:::
    :::column:::
        DROP_DEFAULT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_DEFAULT( **sp_bindefault**에 적용됩니다.)
    :::column-end:::
    :::column:::
        UNBIND_DEFAULT( **sp_unbindefault**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
        DROP_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROPERTY( **sp_addextendedproperty**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_EXTENDED_PROPERTY( **sp_updateextendedproperty**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROPERTY( **sp_dropextendedproperty**에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_CATALOG( **create** 가 지정된 경우 CREATE FULLTEXT CATALOG 문과 *sp_fulltextcatalog* 에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_CATALOG( **start_incremental** , *start_full*, *Stop*또는 *Rebuild*가 지정된 경우 ALTER FULLTEXT CATALOG 문과 *sp_fulltextcatalog* 에 적용되고, **enable** 이 지정된 경우 *sp_fulltext_database* 에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_CATALOG( **drop** 이 지정된 경우 DROP FULLTEXT CATALOG 문과 *sp_fulltextcatalog* 에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_INDEX( **create** 가 지정된 경우 CREATE FULLTEXT INDEX 문과 *sp_fulltexttable* 에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_INDEX( **start_full** , *start_incremental*또는 *stop*이 지정된 경우 ALTER FULLTEXT INDEX 문과 *sp_fulltextcatalog* 에 적용되고, **create**또는 **drop** 외에 다른 동작이 지정된 경우 *sp_fulltext_column* 과 *sp_fulltext_table* 에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_INDEX( **drop** 이 지정된 경우 DROP FULLTEXT INDEX 문과 *sp_fulltexttable* 에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_STOPLIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_FUNCTION
    :::column-end:::
    :::column:::
        DROP_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX(ALTER INDEX 문과 **sp_indexoption**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MASTER_KEY
    :::column-end:::
    :::column:::
        ALTER_MASTER_KEY
    :::column-end:::
    :::column:::
        DROP_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        ALTER_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        DROP_MESSAGE_TYPE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        DROP_PARTITION_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        ALTER_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        DROP_PARTITION_SCHEME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PLAN_GUIDE( **sp_create_plan_guide**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_PLAN_GUIDE(ENABLE, ENABLE ALL, DISABLE 또는 DISABLE ALL이 지정된 경우 **sp_control_plan_guide** 에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_PLAN_GUIDE(DROP 또는 DROP ALL이 지정된 경우 **sp_control_plan_guide** 에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PROCEDURE
    :::column-end:::
    :::column:::
        ALTER_PROCEDURE(ALTER PROCEDURE 문과 **sp_procoption**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_PROCEDURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_QUEUE
    :::column-end:::
    :::column:::
        ALTER_QUEUE
    :::column-end:::
    :::column:::
        DROP_QUEUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVICE_BINDING
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        RENAME( **sp_rename**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROLE(CREATE ROLE 문, **sp_addrole**및 **sp_addgroup**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_ROLE
    :::column-end:::
    :::column:::
        DROP_ROLE(DROP ROLE 문, **sp_droprole**및 **sp_dropgroup**에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROUTE
    :::column-end:::
    :::column:::
        ALTER_ROUTE
    :::column-end:::
    :::column:::
        DROP_ROUTE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RULE
    :::column-end:::
    :::column:::
        DROP_RULE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_RULE( **sp_bindrule**에 적용됩니다.)
    :::column-end:::
    :::column:::
        UNBIND_RULE( **sp_unbindrule**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SCHEMA(CREATE SCHEMA 문, **sp_addrole**, **sp_adduser**, **sp_addgroup**및 **sp_grantdbaccess**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_SCHEMA(ALTER SCHEMA 문과 **sp_changeobjectowner**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_SCHEMA
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        ALTER_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        DROP_SEARCH_PROPERTY_LIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_ROLE
    :::column-end:::
    :::column:::
        ALTER_SERVER_ROLE
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVICE
    :::column-end:::
    :::column:::
        ALTER_SERVICE
    :::column-end:::
    :::column:::
        DROP_SERVICE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        BACKUP_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        RESTORE_SERVICE_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE(데이터베이스, 어셈블리, 트리거와 같은 비스키마 범위 개체에 대한 서명 작업용)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE_SCHEMA_OBJECT(저장 프로시저, 함수와 같은 스키마 범위 개체용)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE_SCHEMA_OBJECT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX는 공간 인덱스에 사용할 수 있습니다.
    :::column-end:::
    :::column:::
        DROP_INDEX는 공간 인덱스에 사용할 수 있습니다.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_STATISTICS
    :::column-end:::
    :::column:::
        DROP_STATISTICS
    :::column-end:::
    :::column:::
        UPDATE_STATISTICS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_SYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYNONYM
    :::column-end:::
    :::column:::
        DROP_SYNONYM
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TABLE
    :::column-end:::
    :::column:::
        ALTER_TABLE(ALTER TABLE 문과 **sp_tableoption**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TRIGGER
    :::column-end:::
    :::column:::
        ALTER_TRIGGER(ALTER TRIGGER 문과 **sp_settriggerorder**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_TRIGGER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TYPE(CREATE TYPE 문과 **sp_addtype**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_TYPE(DROP TYPE 문과 **sp_droptype**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_USER(CREATE USER 문, **sp_adduser**및 **sp_grantdbaccess**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_USER(ALTER USER 문 및 **sp_change_users_login**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_USER(DROP USER 문, **sp_dropuser**및 **sp_revokedbaccess**에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_VIEW
    :::column-end:::
    :::column:::
        ALTER_VIEW
    :::column-end:::
    :::column:::
        DROP_VIEW
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX는 XML 인덱스에 사용할 수 있습니다.
    :::column-end:::
    :::column:::
        DROP_INDEX는 XML 인덱스에 사용할 수 있습니다.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        ALTER_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        DROP_XML_SCHEMA_COLLECTION
    :::column-end:::
:::row-end:::
 
## <a name="ddl-statements-that-have-server-scope"></a>서버 범위가 있는 DDL 문  
 DDL 트리거 또는 이벤트 알림이 서버 인스턴스에서 발생할 때 다음 이벤트에 대한 응답으로 시작되도록 생성될 수 있습니다.  
  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION_SERVER
    :::column-end:::
    :::column:::
        ALTER_SERVER_CONFIGURATION
    :::column-end:::
    :::column:::
        ALTER_INSTANCE(로컬 서버 인스턴스가 지정된 경우 **sp_configure** 및 **sp_addserver** 에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        ALTER_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        DROP_AVAILABILITY_GROUP
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        ALTER_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        DROP_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE
    :::column-end:::
    :::column:::
        ALTER_DATABASE(ALTER DATABASE 문과 **sp_fulltext_database**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ENDPOINT
    :::column-end:::
    :::column:::
        ALTER_ENDPOINT
    :::column-end:::
    :::column:::
        DROP_ENDPOINT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_SESSION
    :::column-end:::
    :::column:::
        ALTER_EVENT_SESSION
    :::column-end:::
    :::column:::
        DROP_EVENT_SESSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROCEDURE( **sp_addextendedproc**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROCEDURE( **sp_dropextendedproc**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER( **sp_addlinkedserver**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_LINKED_SERVER( **sp_serveroption**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER(연결된 서버가 지정된 경우 **sp_dropserver** 에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER_LOGIN( **sp_addlinkedsrvlogin**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER_LOGIN( **sp_droplinkedsrvlogin**에 적용됩니다.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LOGIN(암시적으로 만들어야 하는 존재하지 않는 로그인이 사용된 경우 CREATE LOGIN 문, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**및 **sp_denylogin** 에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_LOGIN( **Auto_Fix**가 지정된 경우 ALTER LOGIN 문, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password** 및 *sp_change_users_login* 에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_LOGIN(DROP LOGIN 문, **sp_droplogin**, **sp_revokelogin**및 **xp_revokelogin**에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE( **sp_addmessage**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_MESSAGE( **sp_altermessage**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_MESSAGE( **sp_dropmessage**에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVER( **sp_addserver**에 적용됩니다.)
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVER( **sp_setnetname**에 적용됩니다.)
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVER(원격 서버가 지정된 경우 **sp_dropserver** 에 적용됩니다.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RESOURCE_POOL
    :::column-end:::
    :::column:::
        ALTER_RESOURCE_POOL
    :::column-end:::
    :::column:::
        DROP_RESOURCE_POOL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_SERVER
    :::column-end:::
    :::column:::
        DENY_SERVER
    :::column-end:::
    :::column:::
        REVOKE_SERVER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        ALTER_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        DROP_WORKLOAD_GROUP
    :::column-end:::
:::row-end:::
 
## <a name="see-also"></a>참고 항목  
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)   
 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)   
 [DDL 이벤트 그룹](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
