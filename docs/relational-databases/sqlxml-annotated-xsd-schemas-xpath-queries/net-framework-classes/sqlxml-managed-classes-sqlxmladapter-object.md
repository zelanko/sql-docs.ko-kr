---
title: SqlXmlAdapter 개체 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f1361babe25e8546b120bed352e31c7fa87d133
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75251400"
---
# <a name="sqlxml-managed-classes---sqlxmladapter-object"></a>SQLXML 관리되는 클래스 - SqlXmlAdapter 개체
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework에서 데이터 세트과의 상호 작용을 돕는 메서드를 제공합니다. 작업 예제는 [.Net 환경에서 SQLXML 기능에 액세스](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)를 참조 하세요.  
  
 SqlXmlAdapter 개체는 다음 메서드를 지원 합니다.  
  
 void 채우기 (데이터 집합 ds)  
 .NET Framework의 데이터 세트을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 검색한 XML 데이터로 채웁니다.  
  
 void 업데이트 (데이터 집합 ds)  
 데이터 세트의 데이터에서 업데이트를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 레코드에 적용합니다.  
  
 SqlXmlAdapter 개체는 다음 생성자를 지원 합니다.  
  
```  
public SqlXmlAdapter(SqlXmlCommand  cmd)   
  
public SqlXmlAdapter(  
                     string commandText,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                      )   
  
public SqlXmlAdapter(  
                     Stream commandStream,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                     )   
```  
  
## <a name="see-also"></a>참고 항목  
 [SqlXmlCommand 개체 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [SqlXmlParameter 개체 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
