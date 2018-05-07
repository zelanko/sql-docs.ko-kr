---
title: sp_syscollector_create_collector_type (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collector_type
- sp_syscollector_create_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 568e9119-b9b0-4284-9cef-3878c691de5f
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b65f9ccc2c68fffd8137dfc7a6d289e7c4f38e13
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spsyscollectorcreatecollectortype-transact-sql"></a>sp_syscollector_create_collector_type(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터 수집기에 사용할 수집기 유형을 만듭니다. 수집기 형식은 논리적 래퍼입니다는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터를 수집 하 고 관리 데이터 웨어하우스에 업로드 하는 중에 실제 메커니즘을 제공 하는 패키지입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_create_collector_type   
    [ [@collector_type_uid = ] 'collector_type_uid' OUTPUT ]  
    , [ @name = ] 'name'  
    , [ [ @parameter_schema = ] 'parameter_schema' ]  
    , [ [ @parameter_formatter = ] 'parameter_formatter' ]  
    , [ @collection_package_id = ] 'collection_package_id'  
    , [ @upload_package_id = ] 'upload_package_id'  
```  
  
## <a name="arguments"></a>인수  
 [ @collector_type_uid =] '*collector_type_uid*'  
 수집기 유형의 GUID입니다. *collector_type_uid* 은 **uniqueidentifier** 것은 자동으로 만들어지고 OUTPUT으로 반환 하는 NULL입니다.  
  
 [ @name =] '*이름*'  
 수집기 유형의 이름입니다. *이름* 은 **sysname** 반드시 지정 해야 합니다.  
  
 [ @parameter_schema =] '*parameter_schema*'  
 이 수집기 유형의 XML 스키마입니다. *parameter_schema* 은 **xml** 기본값은 NULL입니다.  
  
 [ @parameter_formatter =] '*parameter_formatter*'  
 컬렉션 집합 속성 페이지에서 맞게 XML을 변환하는 데 사용하는 템플릿입니다. *parameter_formatter* 은 **xml** 기본값은 NULL입니다.  
  
 [@collection_package_id = ] *collection_package_id*  
 컬렉션 집합에 사용되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 컬렉션 패키지를 가리키는 고유한 로컬 식별자입니다. *collection_package_id* 은 **uniqueidentifer** 필요 합니다.  
  
 [@upload_package_id = ] *upload_package_id*  
 컬렉션 집합에 사용되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 업로드 패키지를 가리키는 고유한 로컬 식별자입니다. *upload_package_id* 은 **uniqueidentifier** 필요 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="example"></a>예제  
 이렇게 하면 일반 T-SQL 쿼리 수집기 유형이 만들어집니다.  
  
```  
EXEC sp_syscollector_create_collector_type  
@collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
  <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
    <xs:element name="TSQLQueryCollector">  
      <xs:complexType>  
        <xs:sequence>  
          <xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
            <xs:complexType>  
              <xs:sequence>  
                <xs:element name="Value" type="xs:string" />  
                <xs:element name="OutputTable" type="xs:string" />  
              </xs:sequence>  
            </xs:complexType>  
          </xs:element>  
          <xs:element name="Databases" minOccurs="0" maxOccurs="1">  
            <xs:complexType>  
              <xs:sequence>  
                <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
              </xs:sequence>  
              <xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
              <xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
            </xs:complexType>  
          </xs:element>  
        </xs:sequence>  
      </xs:complexType>  
    </xs:element>  
  </xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
