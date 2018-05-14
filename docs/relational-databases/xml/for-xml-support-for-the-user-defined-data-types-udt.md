---
title: UDT(사용자 정의 데이터 형식)에 대한 FOR XML 지원 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ee20338ce4cbcd36346fa999c65bd69219a22327
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>사용자 정의 데이터 형식(UDT)에 대한 FOR XML 지원
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML은 CLR(공용 언어 런타임) UDT(사용자 정의 데이터 형식)를 지원하지 않습니다.  
  
 CLR 사용자 정의 데이터 형식으로 FOR XML을 사용하려면 데이터 형식에 XML 직렬화가 있는지 확인하고 FOR XML 선택 절의 XML로의 명시적 캐스트를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [다양한 SQL Server 데이터 형식에 대한 FOR XML 지원](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
