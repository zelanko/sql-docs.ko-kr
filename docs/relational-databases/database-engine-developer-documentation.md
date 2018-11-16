---
title: 데이터베이스 엔진 개발자 설명서 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server Database Engine]
- Database Engine [SQL Server], development
ms.assetid: 7638f46c-9e66-48e6-9a9b-425e0b788311
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 500281b84c84e84507660e3961b3d512b939e582
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668603"
---
# <a name="database-engine-developer-documentation"></a>데이터베이스 엔진 개발자 설명서
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 데이터베이스 응용 프로그램 개발, 관리 및 제어를 위한 풍부한 도구 집합을 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]에 통합된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Windows용 .NET Framework의 CLR(공용 언어 런타임) 구성 요소에 대해 설명합니다. 이를 통해 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic .NET 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#을 포함한 모든 .NET Framework 언어를 사용하여 저장 프로시저, 트리거, 사용자 정의 형식, 사용자 정의 함수, 사용자 정의 집계 및 스트리밍 테이블 반환 함수를 작성할 수 있습니다.  
  
 [SQL Server Native Client 프로그래밍](../relational-databases/native-client/sql-server-native-client-programming.md)  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client에서 MARS(Multiple Active Result Set), UDT(사용자 정의 데이터 형식), 쿼리 알림, 스냅숏 격리 및 XML 데이터 형식 지원과 같은 새로운 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능을 활용하는 응용 프로그램을 새로 작성하거나 기존 응용 프로그램을 개선하는 방법에 대해 설명합니다.  
  
 [SQLXML 4.0 프로그래밍 개념](../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에 새로 추가된 기능(예: XML 데이터 형식)을 지원하는 추가 업데이트 및 SQLXML 3.0과 동일한 기능을 제공하는 최신 버전의 SQLXML에 대해 설명합니다.  
  
 [구성 관리용 WMI 공급자 개념](../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
 MMC(Microsoft Management Console)용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자 스냅인 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자에서 사용되는 게시된 계층에 대해 설명합니다. 이 계층은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자에서 요청하는 레지스트리 작업을 관리하는 통합 API 호출 상호 작용 방법과 선택한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스에 대한 향상된 제어 및 조작을 제공합니다.  
  
 [서버 이벤트용 WMI 공급자 개념](../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
 WMI(Windows Management Instrumentation)를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 이벤트를 모니터링하는 방법을 설명합니다.  
  
 [SMO&#40;SQL Server 관리 개체&#41; 프로그래밍 가이드](../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리의 모든 측면을 프로그래밍하기 위해 설계된 개체 컬렉션인 SMO([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects)에 대한 정보가 포함되어 있습니다.  
  
 [데이터베이스 엔진 확장 저장 프로시저 프로그래밍](../relational-databases/database-engine-extended-stored-procedure-programming.md)  
 확장 저장 프로시저를 사용하여 C와 같은 프로그래밍 언어로 고유한 외부 루틴을 만드는 방법을 설명합니다.  
  
 [데이터 수집기 프로그래밍](https://msdn.microsoft.com/library/53b4752b-055d-4716-b2bc-75b4cce84101)  
 데이터 수집기 개체 모델에 대해 설명합니다.  
  
 [예외 메시지 상자 프로그래밍](https://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)  
 응용 프로그램에서 예외 메시지 상자 프로그래밍 인터페이스를 사용하여 메시징 환경에 대한 추가적인 제어를 제공하고, 사용자에게 나중에 참조할 수 있도록 오류 메시지 내용을 저장하는 옵션을 제공하고, 메시지를 통해 도움을 받을 수 있는 기회를 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 프로그래밍](../analysis-services/data-mining-programming.md)   
 [Analysis Services 개발자 설명서](../analysis-services/analysis-services-developer-documentation.md)   
 [Integration Services 개발자 설명서](../integration-services/integration-services-developer-documentation.md)   
 [복제 개발자 설명서](../relational-databases/replication/concepts/replication-developer-documentation.md)   
 [Reporting Services 개발자 설명서](../reporting-services/reporting-services-developer-documentation.md)  
  
  
