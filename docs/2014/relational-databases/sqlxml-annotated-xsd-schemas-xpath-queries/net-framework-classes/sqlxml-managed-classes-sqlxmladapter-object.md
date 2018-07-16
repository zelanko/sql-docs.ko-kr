---
title: SqlXmlAdapter 개체 (SQLXML 관리 되는 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 192f356052289725043ae2b3dc748931aedb11fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37331413"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>SqlXmlAdapter 개체(SQLXML 관리되는 클래스)
  이 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework에서 데이터 집합과의 상호 작용을 돕는 메서드를 제공합니다. 작업 샘플을 보려면 [.NET 환경에서 SQLXML 기능 액세스](accessing-sqlxml-functionality-in-the-net-environment.md)합니다.  
  
 SqlXmlAdapter 개체는 이러한 메서드를 지원합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [SqlXmlCommand 개체 &#40;SQLXML 관리 되는 클래스&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [SqlXmlParameter 개체 &#40;SQLXML 관리 되는 클래스&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
