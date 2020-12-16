---
title: 메모리 내 OLTP에 대한 SSIS 지원
description: SQL Server Integration Services 패키지에서 고유하게 컴파일된 저장 프로시저를 원본 및 대상 구성 요소로 사용하는 방법을 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ea82a9b9-e9ed-4d6f-b3fd-917f6c687ae3
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f638de7d98cd8e322174172ce918152cbe4623a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485195"
---
# <a name="sql-server-integration-services-support-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 SQL Server Integration Services 지원
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  메모리 최적화 테이블, 메모리 최적화 테이블을 참조하는 뷰 또는 고유하게 컴파일된 저장 프로시저를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)](SSIS) 패키지의 원본이나 대상으로 사용할 수 있습니다. SSIS의 패키지의 데이터 흐름에서 [ADO NET 원본](../../integration-services/data-flow/ado-net-source.md), [OLE DB 원본](../../integration-services/data-flow/ole-db-source.md)또는 [ODBC 원본](../../integration-services/data-flow/odbc-source.md) 를 사용하고 메모리 최적화 테이블 또는 뷰에서 데이터를 검색하도록 원본 구성 요소를 구성하거나, 고유하게 컴파일된 저장 프로시저를 실행할 SQL 문을 지정할 수 있습니다. 마찬가지로 [ADO NET 대상](../../integration-services/data-flow/ado-net-destination.md), [OLE DB 대상](../../integration-services/data-flow/ole-db-destination.md)또는 [ODBC 대상](../../integration-services/data-flow/odbc-destination.md) 을 사용하여 데이터를 메모리 최적화 테이블에 로드하거나, 고유하게 컴파일된 저장 프로시저를 실행할 SQL 문을 지정할 수 있습니다.  
  
 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]테이블 및 뷰와 동일한 방법으로 메모리 최적화 테이블 및 뷰에서 읽고 쓰도록 SSIS 패키지에서 위에 언급한 원본 및 대상 구성 요소를 구성할 수 있습니다. 하지만 고유하게 컴파일된 저장 프로시저를 사용할 때는 다음 섹션에서 설명하는 중요한 점에 주의해야 합니다.  
  
## <a name="invoking-a-natively-compiled-stored-procedure-from-an-ssis-package"></a>SSIS 패키지에서 고유하게 컴파일된 저장 프로시저 호출  
 SSIS 패키지에서 고유하게 컴파일된 저장 프로시저를 호출하려면 ODBC 원본이나 ODBC 대상을 **EXEC** 키워드 없는 **\<procedure name>** 형식의 SQL 문으로 사용하는 것이 좋습니다. SQL 문에 EXEC 키워드를 사용하면 ODBC 연결 관리자가 SQL 명령 텍스트를 저장 프로시저 대신 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문으로 해석하고 고유하게 컴파일된 저장 프로시저의 실행에 지원되지 않는 커서를 사용하기 때문에 오류 메시지가 나타납니다. 연결 관리자는 EXEC 키워드 없는 SQL 문을 저장 프로시저 호출로 처리하고 커서를 사용하지 않습니다.  
  
 ADO .NET 원본과 OLE DB 원본을 사용하여 고유하게 컴파일된 저장 프로시저를 호출할 수도 있지만 ODBC 원본을 사용하는 것이 좋습니다. 고유하게 컴파일된 저장 프로시저를 실행하도록 ADO .NET 원본을 구성하는 경우, ADO .NET 원본이 기본적으로 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient)의 데이터 공급자가 고유하게 컴파일된 저장 프로시저의 실행을 지원하지 않기 때문에 오류 메시지가 나타납니다. ODBC 데이터 공급자, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하도록 ADO .NET 원본을 구성할 수 있습니다. 하지만 ODBC 데이터 공급자와 함께 ADO .NET 원본을 사용하는 것보다 ODBC 원본이 더 좋은 성능을 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP에 대한 SQL Server 지원](./transact-sql-support-for-in-memory-oltp.md)  
  
