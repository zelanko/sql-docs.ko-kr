---
title: SQLXML은 SQL Server에 설치 되지 않음 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4dcf2cf4de62b4f63d37bf7bfd74def6b98cd2f6
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982285"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML이 SQL Server에 설치되지 않음
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전에 SQLXML 4.0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외한 모든 버전의 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 기본 설치에 포함되었습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 최신 버전의 SQLXML(SQLXML 4.0 SP1)이 더 이상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되지 않습니다. SQLXML 4.0 SP1을 설치 하려면 사이트에서 다운로드할 [SQLXML 4.0 SP1 설치 위치](https://www.microsoft.com/en-us/download/details.aspx?id=30403)합니다.  
  
 응용 프로그램 실행 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLXML 4.0이 필요 하 고 다운로드 하 여 SQLXML 4.0 SP1을 설치 해야 합니다.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>SQLOLEDB 및 SQL Server Native Client OLE DB 공급자를 사용하는 SQLXML 4.0 SP1의 새로운 데이터 형식 관련 동작  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SQLXML을 사용 하는 개발자는 데 사용할 수 있습니다 다음 데이터 형식을 도입 되었습니다.  
  
-   **날짜**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 제공 하는 SQLOLEDB를 사용 하 여 SQLXML 4.0 SP1을 사용 하는 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 이러한 형식은 개발자에 게 문자열로 표시 됩니다. SQLXML 4.0 SP1과 함께 사용할 경우 기본 제공 스칼라 형식으로 이러한 네 가지 새로운 데이터 형식을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 이상. SQLXML 4.0 SP1을 다운로드하기 전에 이러한 형식을 문자열이 아닌 형식에 매핑하면 일부 데이터가 잘릴 수 있습니다. 예를 들어 **DateTime2** 하 **xsd: date** 에 매핑하면 데이터가 잘릴 수를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** 전체 자릿수인 3.33 밀리초.  
  
## <a name="see-also"></a>관련 항목  
 [SQLXML 4.0 프로그래밍 개념](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
