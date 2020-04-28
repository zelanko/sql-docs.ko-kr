---
title: sp_syscollector_update_collector_type (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 393b5622964ea3f240d31a2a90c555f7020c500d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68010546"
---
# <a name="sp_syscollector_update_collector_type-transact-sql"></a>sp_syscollector_update_collector_type(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 항목에 대한 수집기 형식을 업데이트합니다. 수집기 형식의 이름과 GUID가 지정되면 컬렉션 및 업로드 패키지, 매개 변수 스키마, 매개 변수 포맷터 스키마 등의 수집기 형식 구성을 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>인수  
`[ @collector_type_uid = ] 'collector_type_uid'`수집기 유형의 GUID입니다. *collector_type_uid* 은 **uniqueidentifier**이며 NULL 인 경우 자동으로 만들어지고 OUTPUT으로 반환 됩니다.  
  
`[ @name = ] 'name'`수집기 유형의 이름입니다. *name* 은 **sysname** 이며 반드시 지정 해야 합니다.  
  
`[ @parameter_schema = ] 'parameter_schema'`이 수집기 유형에 대 한 XML 스키마입니다. *parameter_schema* **xml** 이며 특정 수집기 형식에 필요할 수 있습니다. 필요하지 않은 경우 이 인수는 NULL일 수 있습니다.  
  
`[ @collection_package_id = ] collection_package_id`는 컬렉션 집합에 사용 되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 컬렉션 패키지를 가리키는 고유한 로컬 식별자입니다. *collection_package_id* **uniqueidentifer** 필요 합니다. *Collection_package_id*에 대 한 값을 가져오려면 msdb 데이터베이스의 dbo. syscollector_collector_types 시스템 뷰를 쿼리 합니다.  
  
`[ @upload_package_id = ] upload_package_id`는 컬렉션 집합에 사용 되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 업로드 패키지를 가리키는 고유한 로컬 식별자입니다. *upload_package_id* 은 **uniqueidentifier** 이며 필수입니다. *Upload_package_id*에 대 한 값을 가져오려면 msdb 데이터베이스의 dbo. syscollector_collector_types 시스템 뷰를 쿼리 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>사용 권한  
 **Dc_admin** (실행 권한 포함) 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 일반 T-SQL 쿼리 수집기 형식을 업데이트합니다. 일반 T-SQL 쿼리 수집기 형식의 기본 스키마가 사용됩니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
