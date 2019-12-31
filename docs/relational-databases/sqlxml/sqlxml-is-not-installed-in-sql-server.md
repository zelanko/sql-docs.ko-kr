---
title: SQLXML이 SQL Server에 설치되지 않음
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c666d02449190ca6a88ac43c96ab7aee9676be4d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242654"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML이 SQL Server에 설치되지 않음
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전에 SQLXML 4.0은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외한 모든 버전의 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 기본 설치에 포함되었습니다. 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 최신 버전의 SQLXML(SQLXML 4.0 SP1)이 더 이상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되지 않습니다. SQLXML 4.0 s p 1을 설치 하려면 SQLXML 4.0 s p 1 [의 설치 위치](https://www.microsoft.com/download/details.aspx?id=30403)에서 다운로드 합니다.  
  
 응용 프로그램이에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되며 sqlxml 4.0이 필요한 경우 sqlxml 4.0 s p 1을 다운로드 하 여 설치 해야 합니다.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>SQLOLEDB 및 SQL Server Native Client OLE DB 공급자를 사용하는 SQLXML 4.0 SP1의 새로운 데이터 형식 관련 동작  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에는 SQLXML을 사용 하는 개발자가 사용할 수 있는 다음 데이터 형식이 도입 되었습니다.  
  
-   **날**  
  
-   **시간**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]SQLOLEDB 또는 Native Client OLE DB를 사용 하 여 SQLXML 4.0 s p 1을 사용 하는 경우 이러한 형식은 개발자에 게 문자열로 표시 됩니다. SQLXML 4.0 s p 1은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 이상에서 사용할 때 이러한 4 가지 새 데이터 형식을 기본 제공 스칼라 형식으로 사용 하도록 설정 합니다. SQLXML 4.0 SP1을 다운로드하기 전에 이러한 형식을 문자열이 아닌 형식에 매핑하면 일부 데이터가 잘릴 수 있습니다. 예를 들어, **DateTime2** 를 **xsd: date** 로 매핑하면 데이터가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** 정밀도 3.33 밀리초로 잘립니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLXML 4.0 프로그래밍 개념](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
