---
title: SQLXML이 SQL Server에 설치 되지 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fc997b5230d86a12169ee1ca8fd8c294ad09a048
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092815"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML이 SQL Server에 설치되지 않음
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전에 SQLXML 4.0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외한 모든 버전의 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 기본 설치에 포함되었습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 최신 버전의 SQLXML(SQLXML 4.0 SP1)이 더 이상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되지 않습니다. 파일을 사용할 수 있는 SQLXML 4.0 s p 1을 설치 하려면 사이트에서 다운로드할 [SQLXML SP1 설치 위치](http://www.microsoft.com/download/details.aspx?id=3522)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행 중인 응용 프로그램에 SQLXML 4.0이 필요하고 컴퓨터에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]가 설치되어 있지 않으면 SQLXML 4.0 SP1을 다운로드하고 설치해야 합니다.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>SQLOLEDB 및 SQL Server Native Client OLE DB 공급자를 사용하는 SQLXML 4.0 SP1의 새로운 데이터 형식 관련 동작  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서는 SQLXML을 사용하는 개발자들에게 필요한 다음과 같은 데이터 형식을 제공합니다.  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 Windows Data Access Components(이전의 Microsoft Data Access Components)에서 제공하는 SQLOLEDB를 통해 SQLXML 4.0 SP1을 사용하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Native Client OLE DB를 통해 SQLXML 4.0 SP1을 사용할 경우 이러한 새로운 형식은 개발자에게 문자열로 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0과 함께 SQLXML 4.0 SP1을 사용하는 경우 이러한 네 가지 데이터 형식이 기본 제공 스칼라 형식으로 사용됩니다. SQLXML 4.0 SP1을 다운로드하기 전에 이러한 형식을 문자열이 아닌 형식에 매핑하면 일부 데이터가 잘릴 수 있습니다. 예를 들어 매핑 `DateTime2` 를 `xsd:date` 하면 데이터가 잘릴 수는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] `DateTime` 3.33 밀리초의 전체 자릿수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLXML 4.0 프로그래밍 개념](sqlxml-4-0-programming-concepts.md)  
  
  