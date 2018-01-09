---
title: "SQLXML이 SQL Server에 설치 되지 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f45c7bfd04d974f661756fb06cacda3d34cb808d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML이 SQL Server에 설치되지 않음
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]하기 전에 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0과 함께 출시 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든의 기본 설치의 일부인 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 제외 하 고 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 최신 버전의 SQLXML(SQLXML 4.0 SP1)이 더 이상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되지 않습니다. SQLXML 4.0 s p 1을 설치 하려면 사이트에서 다운로드할 [SQLXML 4.0 SP1 설치 위치](https://www.microsoft.com/en-us/download/details.aspx?id=30403)합니다.  
  
 응용 프로그램에서 실행 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLXML 4.0이 필요 하 고 다운로드 하 고 SQLXML 4.0 s p 1을 설치 해야 합니다.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>SQLOLEDB 및 SQL Server Native Client OLE DB 공급자를 사용하는 SQLXML 4.0 SP1의 새로운 데이터 형식 관련 동작  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]SQLXML을 사용 하 여 개발자가 사용 하려는 경우가 다음 데이터 형식은 기능이 도입 되었습니다.  
  
-   **날짜**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 SQLOLEDB를 통해 SQLXML 4.0 s p 1을 사용 하는 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 이러한 종류는 개발자에 게 문자열로 표시 합니다. SQLXML 4.0 s p 1과 함께 사용할 경우 기본 제공 스칼라 형식으로는 이러한 4 가지 새로운 데이터 형식을 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 이상. SQLXML 4.0 SP1을 다운로드하기 전에 이러한 형식을 문자열이 아닌 형식에 매핑하면 일부 데이터가 잘릴 수 있습니다. 예를 들어 매핑 **DateTime2** 를 **xsd: date** 하면 데이터가 잘릴 수는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** 3.33 밀리초 전체 자릿수이 고 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLXML 4.0 프로그래밍 개념](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
