---
title: "SqlXmlAdapter 개체 (SQLXML 관리 되는 클래스) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffcb07f177c4384dfe781d56ca3a95eeca738743
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="sqlxml-managed-classes---sqlxmladapter-object"></a>SQLXML 관리 되는 클래스-SqlXmlAdapter 개체
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
이 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework에서 데이터 집합과의 상호 작용을 돕는 메서드를 제공합니다. 작업 예제를 참조 하십시오. [.NET 환경에서 SQLXML 기능 액세스](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)합니다.  
  
 SqlXmlAdapter 개체에는 이러한 방법을 지원합니다.  
  
 void Fill (DataSet ds)  
 .NET Framework의 데이터 집합을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 검색한 XML 데이터로 채웁니다.  
  
 void Update (DataSet ds)  
 데이터 집합의 데이터에서 업데이트를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 레코드에 적용합니다.  
  
 SqlXmlAdapter 개체는 이러한 생성자를 지원합니다.  
  
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
 [SqlXmlCommand 개체 &#40; SQLXML 관리 되는 클래스 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [SqlXmlParameter 개체 &#40; SQLXML 관리 되는 클래스 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
