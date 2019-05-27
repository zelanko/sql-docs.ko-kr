---
title: 클라이언트 쪽 및 서버 쪽 XML 서식 지정 (SQLXML 4.0) 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03601c4d36a3e11de4df35bc32237ac554ca93fd
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014437"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>클라이언트 쪽 및 서버 쪽 XML 서식 지정 아키텍처(SQLXML 4.0)
  다음 그림에서는 서버 쪽 XML 서식 지정 아키텍처를 보여 줍니다.  
  
 ![서버 쪽 XML 서식 지정의 아키텍처입니다. ](../../../database-engine/dev-guide/media/serversidexml.gif "아키텍처의 XML 서버 쪽 서식 지정 합니다.")  
  
 이 예에서는 클라이언트에서 지정한 명령이 서버로 전송됩니다. 서버는 XML 문서를 생성하여 클라이언트로 반환합니다. 이 경우 서버 인스턴스가 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 서버 쪽 XML 서식 지정을 사용하면 SQLXMLOLEDB 공급자나 SQLOLEDB 공급자를 사용할 수 있습니다.  SQLXMLOLEDB 공급자는 SQLXML 4.0에 포함된 Sqlxml4.dll을 사용합니다. SQLOLEDB 공급자를 사용하면 기본적으로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 또는 MDAC(Microsoft Data Access Components) 2.6 이상 버전에 포함된 Sqlxmlx.dll에서 제공되는 SQLXML 기능을 가져옵니다. SQLOLEDB로 Sqlxml4.dll을 사용 하려면 SQLOLEDB 연결 개체에서 "SQLXML.4.0" SQLXML Version 속성을 설정 해야 합니다. 두 경우 모두, 서버는 XML 문서를 생성하여 클라이언트로 보냅니다.  
  
> [!NOTE]  
>  XPath 쿼리 및 Updategram은 클라이언트에서 구문 분석됩니다. SQLXML 4.0의 XPath 템플릿이나 Updategram 기능을 가져오려면 Sqlxml4.dll을 사용합니다.  
  
 다음 그림에서는 클라이언트 쪽 XML 서식 지정 아키텍처를 보여 줍니다.  
  
 ![클라이언트 쪽 XML 서식 지정의 아키텍처입니다. ](../../../database-engine/dev-guide/media/clientsidexml.gif "아키텍처의 XML 클라이언트 쪽 서식 지정 합니다.")  
  
 이 예에서 클라이언트는 SQLXMLOLEDB 공급자를 사용합니다. 연결 문자열에서 데이터 공급자 속성은 SQLOLEDB로 설정 되어야 합니다. (SQLXML 4.0에서 허용 되는 유일한 값입니다.) 클라이언트에서 실행 되는 명령이 서버로 전송 됩니다. 서버에서 생성된 행 집합은 클라이언트로 전송됩니다. 행 집합의 XML 문서 서식은 클라이언트에서 지정됩니다.  
  
 SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client(SQLNCLI11) 또는 SQLOLEDB 공급자를 데이터 공급자로 사용할 수 있습니다. 잠재적으로 모든 데이터 원본에 액세스할 수 있습니다. 쿼리에서 단일 행 집합을 반환하는 경우 클라이언트에 XML 변환을 적용할 수 있습니다.  
  
  
