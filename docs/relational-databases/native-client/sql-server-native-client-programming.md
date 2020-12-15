---
title: 프로그래밍
description: 이러한 리소스를 사용 하 여 OLE DB와 ODBC 모두에 사용 되는 독립 실행형 데이터 액세스 API SQL Server Native Client를 이해할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, about SQL Server Native Client
- SQL Server Native Client, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
- data access [SQL Server Native Client]
- SQL Server Native Client
- SQLNCLI
- native data access [SQL Server Native Client]
ms.assetid: 14ba2cb1-a424-4e4d-b224-0bf1015ab801
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 918094d0bbc5739ed00827cc239723379abe3cf1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463294"
---
# <a name="sql-server-native-client-programming"></a>SQL Server Native Client 프로그래밍
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 기술로, OLE DB 및 ODBC 모두에서 사용되는 독립 실행형 데이터 액세스 API(응용 프로그래밍 인터페이스)입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에는 SQL OLE DB 공급자와 SQL ODBC 드라이버가 하나의 네이티브 DLL(동적 연결 라이브러리)로 결합되어 있습니다. 또한 Windows Data Access Components(Windows DAC, 이전의 Microsoft Data Access Components 또는 MDAC)에서 제공하는 것보다 뛰어난 새로운 기능을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 MARS(Multiple Active Result Sets), UDT(사용자 정의 데이터 형식), 쿼리 알림, 스냅샷 격리, XML 데이터 형식 지원 등 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 기능을 활용해야 하는 새 애플리케이션을 작성하거나 기존 애플리케이션을 개선할 수 있습니다.  
  
> [!NOTE]  
>  Native Client와 Windows DAC 간의 차이점에 대 한 목록과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WINDOWS dac 응용 프로그램을 Native client로 업데이트 하기 전에 고려해 야 할 문제에 대 한 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [MDAC에서 SQL Server Native Client 응용 프로그램 업데이트](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)를 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 항상 Windows DAC와 함께 공급된 ODBC 드라이버 관리자와 연동하여 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 Windows DAC와 함께 공급된 OLE DB 핵심 서비스와 연동하여 사용할 수 있지만 반드시 그래야 하는 것은 아니며 개별 애플리케이션 요구 사항(예를 들어 연결 풀링이 필요한지 여부)에 따라 핵심 서비스를 사용할지 여부를 선택할 수 있습니다.  
  
 ADO (ActiveX Data Object) 응용 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용할 수 있지만 **DataTypeCompatibility** 연결 문자열 키워드 (또는 해당 **DataSource** 속성)와 함께 ado를 사용 하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하는 경우 ADO 애플리케이션에서 연결 문자열 키워드 또는 OLE DB 속성 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에 제공되는 새로운 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능을 이용할 수 있습니다. ADO에서 이러한 기능을 사용 하는 방법에 대 한 자세한 내용은 [SQL SERVER NATIVE CLIENT Ado 사용](../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)을 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 OLE DB 또는 ODBC를 사용하여 SQL Server의 네이티브 데이터에 액세스하는 간단한 방법을 제공하도록 디자인되었습니다. 또한 OLE DB 및 ODBC 기술을 한 라이브러리에 결합하고 현재 Microsoft Windows 플랫폼의 일부인 Windows DAC 구성 요소를 변경하지 않고 데이터에 액세스할 수 있는 혁신적이고 발전된 새 기능을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client는 WINDOWS dac의 구성 요소를 사용 하지만 특정 버전의 WINDOWS dac에 명시적으로 종속 되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 지원하는 운영 체제에 설치된 Windows DAC 버전을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 함께 사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 새로운 주요 기능을 나열합니다.  
  
 [SQL Server Native Client를 사용하는 경우](../../relational-databases/native-client/when-to-use-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 Microsoft 데이터 액세스 기술과 연동하는 방법, Windows DAC 및 ADO.NET과 비교되는 특징을 설명하고, 사용할 데이터 액세스 기술을 결정하는 데 도움이 되는 팁을 제공합니다.  
  
 [SQL Server Native Client 기능](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 지원하는 기능을 설명합니다.  
  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 Windows DAC와 다른 점, 사용되는 구성 요소, ADO와 연동하는 방법 등 개발에 대한 개요를 제공합니다.  
  
 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 설치 및 배포에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 라이브러리를 재배포하는 방법을 포함하여 설명합니다.  
  
 [SQL Server Native Client의 시스템 요구 사항](../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하는 데 필요한 시스템 리소스를 설명합니다.  
  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 사용에 대한 정보를 제공합니다.  
  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 사용에 대한 정보를 제공합니다.  
  
 [SQL Server Native Client 추가 정보 찾기](../../relational-databases/native-client/finding-more-sql-server-native-client-information.md)  
 외부 리소스에 대한 링크, 전문가의 지원 받기 등 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에 대한 추가 리소스를 제공합니다.  
  
 [SQL Server Native Client 오류](./sql-server-native-client-error-mssqlserver-50000.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 연결된 런타임 오류에 대한 항목을 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2005 Native Client에서 응용 프로그램 업데이트](../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)   
 [ODBC 방법 도움말 항목](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 방법 도움말 항목](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
