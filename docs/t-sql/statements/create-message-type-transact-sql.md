---
title: "메시지 유형 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MESSAGE_TSQL
- MESSAGE_TSQL
- MESSAGE
- CREATE MESSAGE
- CREATE_MESSAGE_TYPE_TSQL
- MESSAGE TYPE
- MESSAGE_TYPE_TSQL
- CREATE MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- XML [Service Broker]
- validation [Service Broker]
- message types [Service Broker], creating
- empty messages [SQL Server]
- binary [SQL Server], message types
- CREATE MESSAGE TYPE statement
ms.assetid: 98fe0fff-1a2e-4ca2-b37f-83a06fdf098e
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8869a53cf18a58ba58b02e6faf8a42231e971e5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-message-type-transact-sql"></a>CREATE MESSAGE TYPE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 메시지 유형을 만듭니다. 메시지 유형은 메시지의 이름과 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 해당 이름을 가진 메시지에서 수행하는 유효성 검사를 정의합니다. 대화의 양 측면에 동일한 메시지 유형을 정의해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE MESSAGE TYPE message_type_name  
    [ AUTHORIZATION owner_name ]  
    [ VALIDATION = {  NONE  
                    | EMPTY   
                    | WELL_FORMED_XML  
                    | VALID_XML WITH SCHEMA COLLECTION schema_collection_name  
                   } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *message_type_name*  
 생성할 메시지 유형의 이름입니다. 새 메시지 유형은 현재 데이터베이스에 생성되고 AUTHORIZATION 절에서 지정한 보안 주체가 소유합니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다. *message_type_name* 최대 128 자를 사용할 수 있습니다.  
  
 권한 부여 *owner_name*  
 메시지 유형의 소유자를 지정한 데이터베이스 사용자 또는 역할로 설정합니다. 현재 사용자가 **dbo** 또는 **sa**, *owner_name* 유효한 사용자 또는 역할의 이름일 수 있습니다. 그렇지 않으면 *owner_name* 현재 사용자의 이름, 현재 사용자에 게에 대 한 IMPERSONATE 권한이 있는 사용자의 이름 또는 현재 사용자가 속해 있는 역할의 이름 이어야 합니다. 이 절을 생략하면 메시지 유형이 현재 사용자에 속합니다.  
  
 VALIDATION  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 이 유형의 메시지 본문 유효성을 검사하는 방법을 지정합니다. 이 절을 지정하지 않으면 유효성 검사는 기본적으로 NONE으로 설정됩니다.  
  
 없음  
 유효성 검사가 수행되지 않도록 지정합니다. 메시지 본문은 데이터를 포함할 수도 있고 NULL일 수 있습니다.  
  
 EMPTY  
 메시지 본문이 NULL이 되도록 지정합니다.  
  
 WELL_FORMED_XML  
 메시지 본문에 올바른 형식의 XML이 포함되도록 지정합니다.  
  
 VALID_XML WITH SCHEMA COLLECTION *schema_collection_name*  
 메시지 본문의 지정 된 스키마 컬렉션의에서 스키마를 준수 하는 XML에 포함 되도록 지정 된 *schema_collection_name* 기존 XML 스키마 컬렉션의 이름 이어야 합니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 들어오는 메시지의 유효성을 검사합니다. 메시지에 지정된 유효성 검사 유형을 준수하지 않는 메시지 본문이 있으면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 잘못된 메시지를 삭제하고 메시지를 보낸 서비스로 오류 메시지를 반환합니다.  
  
 대화의 양 측면에 동일한 메시지 유형 이름을 정의해야 합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 대화의 양 측면에서 같은 유효성 검사를 사용하도록 요구하지는 않지만 일반적으로 문제 해결에 도움을 주기 위해 대화의 양 측면에서 메시지 유형에 대해 동일한 유효성 검사를 지정합니다.  
  
 메시지 유형은 임시 개체가 아닐 수 있습니다. 메시지 유형 이름은 부터는  **#**  수 있지만 영구 개체입니다.  
  
## <a name="permissions"></a>Permissions  
 기본값의 구성원에 게 메시지 유형 생성 권한은 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 및 **sysadmin** 고정된 서버 역할입니다.  
  
 메시지 유형에 대 한 REFERENCES 권한은 기본적으로 멤버의 메시지 유형의 소유자는 **db_owner** 고정 데이터베이스 역할의 멤버는 **sysadmin** 고정된 서버 역할입니다.  
  
 CREATE MESSAGE TYPE 문에서 스키마 컬렉션을 지정하면 이 문을 실행하는 사용자는 지정된 스키마 컬렉션에 대해 REFERENCES 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-message-type-containing-well-formed-xml"></a>1. 올바른 형식의 XML을 포함하는 메시지 유형 만들기  
 다음 예에서는 올바른 형식의 XML을 포함하는 새로운 메시지 유형을 만듭니다.  
  
```  
CREATE MESSAGE TYPE  
  [//Adventure-Works.com/Expenses/SubmitExpense]  
  VALIDATION = WELL_FORMED_XML ;     
```  
  
### <a name="b-creating-a-message-type-containing-typed-xml"></a>2. XML 유형을 포함하는 메시지 유형 만들기  
 다음 예에서는 XML로 인코딩된 경비 보고서에 대한 메시지 유형을 만듭니다. 이 예에서는 간단한 경비 보고서에 대한 스키마를 보유하는 XML 스키마 컬렉션을 만듭니다. 그런 다음 스키마에 대해 메시지의 유효성을 검사하는 새로운 메시지 유형을 만듭니다.  
  
```  
CREATE XML SCHEMA COLLECTION ExpenseReportSchema AS  
N'<?xml version="1.0" encoding="UTF-16" ?>  
  <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     targetNamespace="http://Adventure-Works.com/schemas/expenseReport"  
     xmlns:expense="http://Adventure-Works.com/schemas/expenseReport"  
     elementFormDefault="qualified"  
   >   
    <xsd:complexType name="expenseReportType">  
       <xsd:sequence>  
         <xsd:element name="EmployeeName" type="xsd:string"/>  
         <xsd:element name="EmployeeID" type="xsd:string"/>  
         <xsd:element name="ItemDetail"  
           type="expense:ItemDetailType" maxOccurs="unbounded"/>  
      </xsd:sequence>  
    </xsd:complexType>  
  
    <xsd:complexType name="ItemDetailType">  
      <xsd:sequence>  
        <xsd:element name="Date" type="xsd:date"/>  
        <xsd:element name="CostCenter" type="xsd:string"/>  
        <xsd:element name="Total" type="xsd:decimal"/>  
        <xsd:element name="Currency" type="xsd:string"/>  
        <xsd:element name="Description" type="xsd:string"/>  
      </xsd:sequence>  
    </xsd:complexType>  
  
    <xsd:element name="ExpenseReport" type="expense:expenseReportType"/>  
  
  </xsd:schema>' ;  
  
  CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = VALID_XML WITH SCHEMA COLLECTION ExpenseReportSchema ;  
```  
  
### <a name="c-creating-a-message-type-for-an-empty-message"></a>3. 빈 메시지에 대한 메시지 유형 만들기  
 다음 예에서는 빈 인코딩으로 새로운 메시지 유형을 만듭니다.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = EMPTY ;  
```  
  
### <a name="d-creating-a-message-type-containing-binary-data"></a>4. 이진 데이터를 포함하는 메시지 유형 만들기  
 다음 예에서는 이진 데이터를 보유하는 새로운 메시지 유형을 만듭니다. 메시지에는 XML이 아닌 데이터가 포함되므로 메시지 유형은 유효성 검사 유형을 `NONE`으로 지정합니다. 이런 경우 이 유형의 메시지를 받는 응용 프로그램은 메시지에 데이터가 있는지, 데이터가 예상된 유형인지를 확인해야 합니다.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ReceiptImage]  
    VALIDATION = NONE ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER MESSAGE type&#40; Transact SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [DROP MESSAGE type&#40; Transact SQL &#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

