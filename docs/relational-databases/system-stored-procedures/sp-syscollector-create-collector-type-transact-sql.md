---
title: sp_syscollector_create_collector_type (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4db22cb0d886a4b0ed1213998d334d4b20ce90f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725603"
---
# <a name="sp_syscollector_create_collector_type-transact-sql"></a>sp_syscollector_create_collector_type(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  데이터 수집기에 사용할 수집기 유형을 만듭니다. 수집기 형식은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터를 수집 하 고 관리 데이터 웨어하우스에 업로드 하는 실제 메커니즘을 제공 하는 패키지에 대 한 논리적 래퍼입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 수집기 유형의 GUID입니다. *collector_type_uid* 은 **uniqueidentifier** 이며 NULL 인 경우 자동으로 만들어지고 OUTPUT으로 반환 됩니다.  
  
 [ @name =] '*name*'  
 수집기 유형의 이름입니다. *name* 은 **sysname** 이며 반드시 지정 해야 합니다.  
  
 [ @parameter_schema =] '*parameter_schema*'  
 이 수집기 유형의 XML 스키마입니다. *parameter_schema* 은 **xml** 이며 기본값은 NULL입니다.  
  
 [ @parameter_formatter =] '*parameter_formatter*'  
 컬렉션 집합 속성 페이지에서 맞게 XML을 변환하는 데 사용하는 템플릿입니다. *parameter_formatter* 은 **xml** 이며 기본값은 NULL입니다.  
  
 [ @collection_package_id =] *collection_package_id*  
 컬렉션 집합에 사용되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 컬렉션 패키지를 가리키는 고유한 로컬 식별자입니다. *collection_package_id* **uniqueidentifer** 필요 합니다.  
  
 [ @upload_package_id =] *upload_package_id*  
 컬렉션 집합에 사용되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 업로드 패키지를 가리키는 고유한 로컬 식별자입니다. *upload_package_id* 은 **uniqueidentifier** 이며 필수입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>사용 권한  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
